#  Tornando o seu Raspberry Pi visível na Internet

Utilizar o Raspberry Pi como um servidor caseiro é uma forma interessante de se estudar e aprender a gerenciar serviços do [Linux](/blog/como_instalar_linux_raspberry_pi/) enquanto também desfrutamos dos benefícios que estes serviços nos providenciam. Por exemplo, anteriormente vimos como facilmente podemos [compartilhar arquivos entre nossos dispositivos de casa](/blog/compartilhando_arquivos_nas_raspberrypi/) utilizando um programa chamado Samba no Raspberry Pi. Após aprender a instalá-lo e configurá-lo, pudemos também nos beneficiar da conveniência de conectar qualquer dispositivo em casa, independente do sistema operacional.

Nestes exemplos, porém, ainda possuimos uma limitação: não é possível acessar o sistema *fora da nossa rede local*. No momento que saímos do alcance da nossa rede Wifi, já não seria mais possível acessar o nosso Raspberry Pi e nem os serviços que tão carinhosamente implementamos nele. Felizmente, ainda é possível cobrir esta diferença com soluções de Software. É isso mesmo, não é preciso gastar dinheiro comprando algum equipamento especial ou contratando um plano especial com o seu provedor de internet para realizar isto. Neste post, mostraremos um método para **acessar seu Raspberry Pi da Internet**, conhecido como *Port Forwarding*.

## Como funciona o *Port Forwarding*

A técnica chamada de [Port Forwarding](https://en.wikipedia.org/wiki/Port_forwarding) é relativamente simples, e pode ser implementada em virtualmente qualquer roteador e switch residencial moderno. Ela funciona da seguinte forma:

Quando você conecta um dispositivo à internet na sua casa (wifi ou não), está essencialmente conectando-o ao seu roteador *primeiro* para que este roteador se encarregue de gerenciar a conexão do dispositivo com os serviços externos da internet. É o seu roteador que está em contato direto com a internet, e realiza o trabalho de gerenciar as conexões que entram e saem da sua rede através de um processo chamado [Network Address Translation, ou NAT](https://en.wikipedia.org/wiki/Network_address_translation). 

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/NAPT-en.svg/1200px-NAPT-en.svg.png" alt="explicação do NAT e as redes internas" />
    <figcaption>
        O roteador (NAPT) atua como interface entre o "mundo" interno da rede local (10.1.1.x) e o resto da internet. Crédito: Wikimedia.org
    </figcaption>
</figure>

Como consequência do NAT, O seu dispositivo nunca "enxerga" a internet diretamente, e conversamente dispositivos da internet não podem acessá-lo diretamente - o que leva alguns a erroneamente acharem que o roteador funciona como um firewall. É possível, porém, abrir "exceções" no NAT do seu roteador, de forma que ele entenda que quaisquer conexões entre um certo dispositivo e a internet devam ser realizados diretamente, efetivamente "expondo" o dispositivo. Este é o processo chamado de port forwarding.

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/NAT_Concept-en.svg/1200px-NAT_Concept-en.svg.png" alt="Explicando o Port Forwarding via roteador" />
    <figcaption>
        Através do Port Forwarding, o Roteador expõe transparentemente o dispositivo interno com a comunicação externa, fazendo-o aparentar estar diretamente conectado. Crédito: Wikimedia.org
    </figcaption>
</figure>

Felizmente, quase qualquer roteador residencial ou de um provedor de internet oferece esta funcionalidade, sendo apenas necessário configurá-la corretamente. O procedimento geral consistem em:

 1. Identificar o endereço IP interno do Raspberry Pi.
 2. Configurar o roteador para permitir tráfego diretamente ao endereço do Raspberry Pi
 3. Opcional: associar um nome de domínio ao endereço IP externo do Raspberry Pi para facilitar o acesso (recomendado)

Exploraremos cada um destes passos a seguir.

## Passo 1: Identificando o endereço IP interno do Raspberry Pi

Para abrir esta exceção no roteador, precisamos especificar qual dispositivo deverá ser conectado diretamente à internet. Para isso, utilizaremos o endereço IP interno do Raspberry Pi na rede caseira.

Para obter o endereço IP do Raspberry Pi no Linux, execute o seguinte comando no terminal:

    ip addr

Este comando irá retornar um conteúdo parecido com o seguinte:

    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether dd:b6:71:b8:2f:81 brd ff:ff:ff:ff:ff:ff
    inet 192.168.10.7/24 brd 192.168.10.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::80eb:b427:3f1a:fc92/64 scope link
       valid_lft forever preferred_lft forever
    ...

Procure pela linha que contém a palavra `inet`; o número associado à ela é o seu IP interno, geralmente no formato `192.168.XX.YY`.

    ...
    inet 192.168.10.7/24 brd 192.168.10.255 scope global noprefixroute eth0
    ...

Se a sua distribuição Linux não oferece o comando `ip` (é o caso de distribuições minimalistas ou especialistas), é também possível encontrá-lo utilizando o comando `ifconfig`:

    $ ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.10.7  netmask 255.255.255.0  broadcast 192.168.10.255
        inet6 fe80::80eb:b427:3f1a:fc92  prefixlen 64  scopeid 0x20<link>
    ...
    

Note que dependendo do seu modelo do Raspberry Pi, você poderá ter dois endereços distintos, um para a interface Wifi e outro para a interface cabeada. Este é o caso dos modelos mais novos, como o [Raspberry Pi 3](https://amzn.to/3rfzseM) e o poderoso [Raspberry Pi 4](https://amzn.to/3clMHXi). 

Geralmente, preferimos utilizar aqui a interface cabeada para garantir a constância e a velocidade da conexão com a internet, mas não sendo possível (por exemplo, distância ou acesso ao roteador), também é perfeitamente possível fazer port forwarding via wifi. Se o seu Raspberry Pi não possuir WiFi integrado (como o modelo 1), é possível utilizar um [adaptador WiFi de USB](https://amzn.to/3rizqml).

Armado com o IP para ser exposto, vamos configurar o roteador.

## Passo 2: Expondo o Raspberry Pi diretamente à internet via Roteador

Por conta da grande diversidade de modelos e interfaces de roteadores disponíveis, infelizmente não podemos escrever um único guia definitivo para esta configuração. Portanto, descrevemos aqui os passos principais que você deve seguir.

Navegue até o endereço do seu roteador, geralmente descrito como `AAA.BBB.CCC.1` na maioria das redes caseiras. Faça o login como administrador - se você não sabe quais são as credenciais, poderá achá-las escritas atrás do seu roteador (esta também é uma *ótima* hora para trocá-las e evitar um [incidente de segurança futuro](https://security.stackexchange.com/questions/77112/danger-of-default-router-password)).

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Modem_DirecTV_4G_LTE_Colombia_(trasera).jpg/607px-Modem_DirecTV_4G_LTE_Colombia_(trasera).jpg" alt="Fundo de um roteador onde senhas padrões estão expostas" />
    <figcaption>
        Quase todos os dispositivos de rede residenciais possuem suas credenciais de fábrica expostas no verso em algum lugar. Os que não possuem podem ser achados com uma simples busca. Troque as suas para evitar problemas. Crédito: Wikimedia.org
    </figcaption>
</figure>

Uma vez autenticado, procure por configuração de "Port Forwarding" ou "Port filtering" sob as configurações de LAN. Nestas configurações, informe o endereço IP que você obteve no passo anterior como uma exceção ao no filtro de NAT do roteador e salve as configurações. O roteador será reiniciado.

Neste ponto, seu Raspberry Pi estará visível a partir da Internet. Para testá-lo, você precisará descobrir primeiro qual é o seu IP externo (acessível da internet), o que pode ser feito acessando [este link](https://duckduckgo.com/?q=ip), ou este comando a partir do seu Raspberry Pi:

    curl https://lite.duckduckgo.com/lite/?q=ip | grep "Your IP address"

Seu endereço IP público é o número informado. Munido desta informação, execute os seguintes comandos no seu Raspberry Pi para iniciar um servidor web de testes:

    cd /tmp
    python -m http.server 8090

A partir de outro computador ou seu celular, navegue para `http://SEUENDEREÇOIP:8090`. Se você conseguir acessar este endereço, parabéns: **seu Raspberry Pi está visível e acessível da Internet.** `;)`

## Passo 3: Adquirindo um domínio gratuito para o seu Raspberry Pi

Tecnicamente, seu Raspberry Pi está pronto para ser acessado externamente e não necessita de nenhuma outra configuração. Porém, memorizar um endereço IP pode ser um pouco complicado, e ter um nome de domínio (ex: `meuraspberrypi.net`) facilita bastante, e é recomendado - especialmente se você planeja hospedar vários serviços.

Ao contrário do que se aparenta, é possível também obter um nome de domínio de forma *completamente gratuita* de maneira similar aos blogs e sites gratuito em plataforma como o Wordpress ou Blogspot. Tratam-se de serviços gratuitos de [DNS](https://en.wikipedia.org/wiki/DNS) dinâmico, que farão o redirecionamento gratuito para o endereço IP do seu Raspberry Pi.

Através do provedor [FreeDNS](https://freedns.afraid.org/), por exemplo, você poderá registrar um sub-domínio sob o domínio `.afraid.org` apontando para o seu Raspberry Pi, tornando-o muito mais memorável. Outros provedores incluem [No-IP](https://www.noip.com/) e diversos outros. Com tanta facilidade e custo zero, não há razão para não ter um domínio para o seu Raspberry Pi. Falaremos mais sobre como utilizar este serviço num post futuro.

## Considerações extras de segurança

Colocar o seu Raspberry Pi disponível na Internet é divertido e engajante, mas não é um completo mar de rosas. Há muitos outros pontos sobre os quais devemos tomar consideração, e entre eles o mais importante é a **segurança do seu sistema**.

Qualquer computador exposto diretamente à internet se torna publicamente acessível a qualquer outro dispositivo no globo sem o filtro protetor do NAT, incluindo usuários maliciosos que podem querer atacar ou explorar o seu sistema. Mesmo que você não tenha muito o que "perder" com um simples Raspberry Pi, lembre-se que ele ainda se encontra anexado à sua rede interna, possibilitando o acesso de um usuário malicioso aos seus outros dispositivos se hackeado.

Segurança da computação é um assunto complexo, e com muitos pontos para serem considerados, então falaremos sobre isto com mais detalhes em outro post futuro. Você pode começar a assegurar seu Raspberry Pi considerando os seguintes pontos:

 - Mantendo o seu sistema operacional **atualizado**, com os *patches* de segurança instalados o mais cedo possível. Manter o software do seu computador atualizado é a forma leiga mais eficiente de evitar problemas de segurança.
 - Instalando e configurando um **Firewall** para permitir que apenas as portas onde os serviços estão atuando sejam abertas. O programa [ufw](https://code.launchpad.net/ufw) é um firewall popular no Linux.
 - Não habilitando mais serviços além daqueles que você necessita. Quanto mais serviços existem, maior a sua [superfície de ataque](https://en.wikipedia.org/wiki/Attack_surface) pela qual você pode ser comprometido. Não usa alguma coisa? Desabilite-a. **Reduza os riscos para o mínimo necessário.**

## Conclusão

Colocar os serviços do seu Raspberry Pi na internet, sejam eles um servidor web para o seu site, IRC ou XMPP, não é um processo complicado, e pode lhe ajudar a estabelecer sua presença online de forma simples, rápida e - mais importante - gratuita.

O *port forwarding* é um truque simples que disponibiliza seu computador na internet rapidamente, e quando combinado com um domínio gratuito, se torna uma forma poderosa de publicar sites e serviços na internet. Ainda assim, precisamos tomar alguns cuidados extras ao disponibilizar um servidor público numa rede onde não temos controle sobre quem a acessa - em outras palavras, a Internet.

Para explicações detalhadas de como habilitar Port Forwarding para modelos específicos de roteadores, existem alguns guias que explicam em detalhes o processo para vários roteadores caseiros disponíveis no mercado. O site [PortForward.com](https://portforward.com/), por examplo, possui explicações detalhadas que poderão lhe assistir no processo, se o seu roteador se encontra em sua lista. Outro recurso é o guia do [No-IP](https://www.noip.com/support/knowledgebase/general-port-forwarding-guide/).

Divirta-se colocando o seu novo site na internet a partir do seu Raspberry Pi!

----

O que você acha do método do *Port Forwarding* como uma maneira de disponibilizar seu Raspberry Pi na Internet? Conhece algum outro método de realizá-lo? O que faria para assegurar o seu Raspberry Pi uma vez publicado? Escreva para nossa conta no [Mastodon!](https://qoto.org/@raspibrasil)

