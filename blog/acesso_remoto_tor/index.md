# Acessando o Raspberry Pi fora de casa via Tor

Usar o Raspberry Pi como um servidor é forma extremamente conveniente e simples de aprender a utilizar o [software livre](/blog/bem_vindo_ao_raspberrypi_brasil/). Com seu baixo consumo de energia, hardware e armazenamento baratos, e baixa necessidade de arrefecimento, modelos como o [Raspberry Pi 3](https://amzn.to/3qlUOqH) funcionam como ótimos servidores de pequeno a médio porte na sua rede caseira. Quando queremos acessá-lo de fora da nossa rede caseira, geralmente podemos fazê-lo através de uma técnica chamada [Port Forwarding](/blog/tornando_seu_raspberry_pi_visivel_internet/), que envolve colocar o Raspberry Pi numa posição privilegiada na rede e ser enxergado da própria internet. 

Porém, algumas vezes esta combinação pode não ser completamente possível, por conta de fatores associados ao seu roteador ou até mesmo se o seu provedor de internet não expõe endereços individuais na internet. Quando isto acontece, felizmente ainda temos uma alternativa para acessar nossos arquivos remotamente: a rede [Tor](https://torproject.org). Famosa (ou infame) por proporcionar privacidade e anonimato nas atividades da internet, há um uso menos conhecido do Tor que permite você acessar um computador atrás de um roteador através de uma ferramenta chamada *Hidden Services*. Vejamos como fazer isso neste post.

## Como os Tor Hidden Services funcionam

O Tor foi criado em 2002 pela Marinha Americana como uma forma de se anonimizar tráfego na internet e dificultar sua análise. Desde sua concepção, o projeto primeiramente foca na proteção da privacidade dos usuários, a qual é alcançada através da utilização de três camadas criptografadas de tráfego, que tornam virtualmente impossível qualquer ponto na rede de descobrir quem está acessando o quê.

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/d/dc/Tor-onion-network.png" alt="Descrição de como a rede Tor funciona" />
    <figcaption>
        O Tor anonimiza a sua conexão com a internet fazendo-a passar por três "pontos intermediários," que impossibilitam identificar quem está falando com quem. Crédito: Wikimedia.org
    </figcaption>
</figure>

Com o tempo, o Tor Project expandiu o seu escopo para incluir também a funcionalidade *Hidden Service* que permite você hospedar um site ou serviço dentro do Tor sem ser possível identificar quem são os seus visitantes, e nem seus visitantes quem você é. Esta implementação é bastante controversa, pois pode habilitar alguém a hospedar conteúdo de legalidade duvidosa, mas vem com outra ótima função: se tornar acessível mesmo atrás de um firewall ou roteador.

Por esta razão, podemos utilizar Hidden Services como uma forma de acesso remoto da internet ao nosso Raspberry Pi de forma segura combinando-o com o [Protocolo SSH](/blog/acesso_remoto_seguro_raspberrypi_ssh/). Assim, caso não seja possível acessar o seu Raspberry Pi via port forwarding, podemos ainda acessá-lo provado que: 

 1. Ele possua alguma conexão à internet.
 2. O sistema Tor e o SSH estejam instalados e operando nele. 
 3. O seu dispositivo cliente também possua Tor instalado. 

Trataremos a seguir sobre os pontos #2 e #3. 

## Criando um Hidden Service de SSH no Raspberry Pi 

Um Hidden Service nada mais é do que um serviço disponibilizado através da rede Tor. Você em teoria pode criar um Hidden Service para qualquer serviço do Linux, embora os mais comuns sejam [Servidor Web](/blog/hospedando_seu_site_raspberry_pi/) ou [SSH](/blog/acesso_remoto_seguro_raspberrypi_ssh/). E enquanto serviços na internet costumam utilizar domínios da internet (.com, .net, etc), Hidden Services utilizam endereços `.onion`, que são gerados de maneira aleatória. 

Como o SSH já vem habilitado por padrão no [Raspberry Pi OS](/blog/como_instalar_linux_raspberry_pi/), para hospedar o serviço SSH como Hidden Service no Raspberry Pi, primeiro instale o Tor com o seguinte comando: 

    sudo apt-get install tor 

O Tor é instalado e iniciado automaticamente. Na sua configuração padrão, o Tor atende bem os requerimentos de anonimato como um cliente, mas se você precisa hospedar serviços com ele, precisa de configurações adicionais. Vamos editá-lo para adicionar um Hidden Service rodando o SSH. Adicione as seguintes linhas ao arquivo de configuração central do Tor: `/etc/tor/torrc`:

    HiddenServiceDir /var/lib/tor/ssh
    HiddenServicePort 22 127.0.0.1:22
    # assumindo que SSH está na porta 22

Salve o arquivo e reinicie o Tor com o seguinte comando:

    sudo systemctl restart tor

Ao reiniciar, o Tor irá criar um diretório com informações específicas para o seu novo Hidden Service do SSH localizado em `/var/lib/tor/ssh` (conforme criado acima), acessível somente pelo usuário root por conta da segurança. Ao passo que você não precisará editar nenhum outro arquivo de configuração, o arquivo `hostname` dentro deste diretório contém o endereço `.onion` do seu Hidden Service, do qual você precisará para acessá-lo remotamente. Um endereço .onion de exemplo poderia ser:

    $ sudo cat /var/lib/tor/ssh/hostname
    abcdefabcdefabcdefabcdefabcdefabcdefabcdef.onion

Guarde este endereço em algum lugar, pois você precisará-dele para configurar o dispositivo cliente.

## Acessando o SSH via Tor no seu dispositivo

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Onion_diagram.svg/500px-Onion_diagram.svg.png" alt="Onion Routing explicado" />
    <figcaption>
        O princípio do Onion Routing consiste em "encapar" uma mensagem com três chaves distintas para que ninguém exceto o destinatário possa vê-la. Crédito: Wikimedia.org
    </figcaption>
</figure>

Já andamos metade do caminho configurando o servidor, mas igualmente necessário é configurar o seu dispositivo cliente para também utilizar o Tor para identificar e acessar o seu Raspberry Pi. Assumiremos aqui que você está utilizando Linux no dispositivo cliente.

Conforme especificamos nos requerimentos acima, você também deverá instalar o Tor no seu dispositivo para acessar um Hidden Service, e adicionalmente um programa chamado `netcat` que fará o roteamento da conexão SSH pela rede Tor. Utilizando Ubuntu ou Debian, o comando para instalar é:

    sudo apt-get install netcat

Edite o arquivo de configuração `~/.ssh/config` e adicione uma nova entrada para o seu Hidden Service:

    Host meuraspi-tor
        # use o hostname que obteve do raspberry pi anteriormente
        Hostname abcdefabcdefabcdefabcdefabcdefabcdefabcdef.onion 
        User nomedeusuario
        ProxyCommand netcat --proxy 127.0.0.1:9050 --proxy-type socks5 %h %p

> Dica: se você já possui um host SSH habilitado, é de praxe criar sua "versão torificada" simplesmente adicionando `-tor` no campo *Host*. Por exemplo, se o seu Raspberry Pi internamente é o Host `raspi`, seu acesso via Tor seria `raspi-tor`.

Adicionalmente, se você [configurou seu SSH para utilizar chaves](/blog/acesso_remoto_seguro_raspberrypi_ssh/) ao invés de senhas na autenticação, deve especificar a localização delas novamente:

    Host meuraspi-tor
        Hostname abcdefabcdefabcdefabcdefabcdefabcdefabcdef.onion 
        User nomedeusuario
        # especifique a localização da chave privada:
        IdentityFile /home/usuario/.ssh/minhachave
        ProxyCommand netcat --proxy 127.0.0.1:9050 --proxy-type socks5 %h %p

Salve o arquivo, e teste a conexão com o comando:

    ssh meuraspi-tor

Note que, por conta da utilização do Tor e o roteamento por vários hosts, a velocidade da conexão é reduzida drasticamente. O SSH irá perguntar se você reconhece o fingerprint por conta dele ser um host novo. Se você enxerga o seu login do Raspberry Pi com sucesso, parabéns: o seu Hidden Service foi configurado corretamente, e está disponível além da sua rede caseira.

## Prós e contras de um Hidden Service no Raspberry Pi

Embora prático e simples de se implementar, nem tudo são flores com os Hidden Services. Embora sua maior vantagem seja a privacidade adicional e o acesso independente de firewall ou NAT, eles possuem duas grandes limitações:

 - O serviço precisa rodar sobre a rede Tor, reduzindo significantemente sua velocidade. Para comparação, imagine a redução da velocidade da sua conexão através de uma VPN. No caso do Tor, é como se você passasse por *três* VPNs para o mesmo destino. Este é o custo do anonimato.
 - Algumas redes, especialmente as corporativas, bloqueiam o uso do Tor dentro delas alegando risco de segurança. É possível ainda utilizá-lo através de soluções do próprio Tor, como *Bridges* ou *Pluggable Transports*, mas requerem mais esforço para serem implementados. É mais fácil simplesmente evitar seu uso.

Uma grande vantagem, porém, é a segurança adicional que é providenciada ao seu próprio Raspberry Pi: como você não o disponibiliza diretamente na internet, não há risco adicional que scanners e adversários encontrem seu Raspberry Pi e tentem atacá-lo.

## Bônus: acessando seu Raspberry Pi do seu smartphone

Não há como se tornar mais móvel hoje em dia do que através de um smartphone e conexão 4G e, dependendo da sua rotina, é provável que você passe mais tempo na rua do que com acesso a um computador. Há como acessar seu Raspberry Pi desta forma?

Incrivelmente, **sim!** Mas, por enquanto, apenas no Android...

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d8/Screenshot_from_termux.png/337px-Screenshot_from_termux.png" alt="screenshot do Termux" />
    <figcaption>
        O aplicativo Termux rodando no Android. Crédito: Wikimedia.org
    </figcaption>
</figure>

Graças a um aplicativo Android chamado [Termux](https://termux.com/), você pode ter acesso a um verdadeiro *shell* Linux no seu próprio celular. É possível instalar software do Linux dentro do aplicativo, incluindo o SSH e o Tor. Combinando os dois e os configurando como nos exemplos acima, é possível acessá-lo da mesma maneira do que num desktop. 

Nós descobrimos o Termux relativamente recentemente, mas desde então ele facilmente se tornou nosso aplicativo favorito, e o altamente recomendamos. Talvez no futuro escreveremos um post mais detalhado de como podemos utilizá-lo a fundo.

---

Você utilizou hidden services ou o Tor antes? Já conhecia esta utilização para acesso remoto? Escreva para nós no [Mastodon!](https://qoto.org/@kzimmermann)
