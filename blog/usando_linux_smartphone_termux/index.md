# Usando Linux no seu Smartphone com o Termux

Aqui no Raspberry Pi Brasil temos o lema que não há nada que não possa ser resolvido através de um [Single-board Computer (SBC)](/blog/bem_vindo_ao_raspberrypi_brasil/) e o Software Livre. Embora os SBCs sejam computadores versáteis e flexíveis, variando desde os simples modelos como o [Raspberry Pi 3](https://amzn.to/3qlUOqH) até os poderosos [Raspberry Pi 4B](https://amzn.to/3slgdlW) que podem até [ser utilizados como Desktops](/blog/raspberry_pi_como_desktop/), algumas vezes precisamos de um fator de mobilidade em nossa computação moderna.

Quando se trata de mobilidade, praticamente não há quem ganhe dos nossos smartphones, em termos de conectividade e vida útil da bateria. Infelizmente, ao os utilizarmos, ficamos restritos aos Apps e suas plataformas, sendo difícil ter o poder que o Linux e o Software Livre nos providencia nestes dispositivos. Isto é, até agora. Neste post, mostramos como é possível ter acesso a um ambiente Linux completo no seu smartphone Android através de um aplicativo poderoso chamado **Termux** para que você possa levar sua computação com você e até [acessar seu Raspberry Pi fora de casa](/blog/tornando_seu_raspberry_pi_visivel_internet/) através do seu smartphone.

Vamos em frente.

## O que é o Termux?

O [Termux](https://termux.com/) é um aplicativo para Android que emula um ambiente Linux completo dentro do Android. Diferente de outros "aplicativos Linux" disponíveis, não só o Termux emula um *shell* como o bash ou SSH, ele oferece um ambiente **completo** que disponibiliza várias utilidades do Linux e até um gerenciador de pacotes que permite você a instalar software adicional ao ambiente. Tamanha é a plenitude do aplicativo que os desenvolvedores inclusive o consideram uma distribuição Linux independente.

Nos bastidores, o Termux faz uso do fato que o Android também é baseado no Linux para utilizar um mechanismo chamado [*chroot*](https://en.wikipedia.org/wiki/Chroot) que isola o seu próprio ambiente do resto do Android, essencialmente tornando-se um "Linux dentro do Linux."

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Diagramme_ArchiEmulateur.png/400px-Diagramme_ArchiEmulateur.png" alt="Descrição de funcionamento do Chroot" />
    <figcaption>
        O chroot cria um ambiente virtual isolado que pode ser operado e modificado independente do ambiente "pai." Crédito: Wikimedia.org
    </figcaption>
</figure>

Uma vez dentro do ambiente *chroot*, o Termux opera seu próprio mundo, trazendo funcionalidades nativas do Linux à interface Android. O Termux traz o shell bash nativamente e pronto para ser utilizado, e também o seu próprio mecanismo de gerenciamento de pacotes chamado `pkg`, que funciona de maneira similar ao `apt` do [Raspberry Pi OS](/blog/como_instalar_linux_raspberry_pi/) e do Debian. E a melhor notícia de todas: *não requer "rooting" para funcionar.* Virtualmente qualquer versão recente do Android pode rodá-lo.

A função do *chroot* de "pegar emprestado" a fundação Linux que o Android usa pode ser a razão pela qual o Termux infelizmente não está disponível para o iPhone, o que é realmente uma pena dado o poder do aplicativo.

## Instalando e utilizando o Termux

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/d/d8/Screenshot_from_termux.png" alt="Screenshot do Termux no Android" />
    <figcaption>
        O Termux oferece um ambiente Linux completo para o seu celular Android. Crédito: Wikimedia.org
    </figcaption>
</figure>

Você pode baixar o Termux diretamente do Google Play, mas seus próprios desenvolvedores recomendam a utilização da versão disponível no [F-Droid](https://f-droid.org/en/packages/com.termux/) (a alternativa Free Software ao Google Play) por conta desta receber as atualizações mais frequentemente.

Na sua primeira execução, o Termux lembra a linha de comando do Linux, disponibilizando algumas informações de onde encontrar ajuda e o `bash` para você inserir comandos. Embora já completamente utilizável a partir deste ponto, podemos melhorá-lo com alguns passos a mais.

Além do aplicativo em si, o Termux mantém seu próprio ambiente separado, portanto primeiramente é necessário *atualizá-lo* também para sua versão mais recente. Podemos fazer isso com o comando `pkg`:

    pkg upgrade

O `pkg` no Termux é do que um *wrapper* para o `apt` do Debian que o aponta para o melhor repositório do Termux disponível. Por conta do mechanismo *chroot* descrito acima, você já está rodando como usuário `root` e portanto o comando `sudo` não é necessário.

Se houverem atualizações disponíveis, instale-as digitando `y` e ao final do processo seu ambiente Linux estará atualizado.

Podemos usar o `pkg` para instalar software adicional dentro do Termux. Recomendamos instalar os seguintes pacotes para obter um ambiente Linux versátil e produtivo:

 - tmux: um [terminal multiplexer](https://en.wikipedia.org/wiki/Tmux) que permite você rodar várias "janelas" de terminais numa única sessão.
 - mc: gerenciador de arquivos do terminal com dois painéis. Um pouco esquisito de usar no começo, mas excelente uma vez que acostumado.
 - elinks: um navegador web apenas de texto, ótimo para consultar documentação no terminal.
 - um editor de texto, nosso favorito sendo o [vim](https://vim.org).

O comando para instalá-los é:

    pkg install tmux mc elinks vim

Finalmente, você pode conceder permissões adicionais para o ambiente do Termux acessar o resto do armazenamento interno do seu celular ou até mesmo o cartão MicroSD. Isto possibilitará acessar fotos e outros arquivos de outros aplicativos de maneira bem conveniente, sem precisar utilizar a função de "compartilhar" do Android. Para isso, utilize o comando:

    termux-setup-storage

O Android perguntará se você quer conceder acesso ao armazenamento. Aperte "sim" e você poderá acessar o resto do seu smartphone no diretório `~/storage/`, onde `~/storage/shared` é o seu armazenamento interno e `~/storage/external-1` é o seu cartão MicroSD.

Agora você pode se sentir em casa usando Linux completamente do seu próprio celular!

## Acessando seu Raspberry Pi do seu celular

Você já tem o computador móvel (smartphone), acesso à Internet (conexão 4G) e um sistema operacional familiar (Linux no Termux). Será possível conectar remotamente ao seu Raspberry Pi agora?

A resposta é um ressonante **sim**: da mesma forma que de um computador desktop remoto.

Providenciado que você tenha configurado seu Raspberry Pi para [ser visível na Internet](/blog/tornando_seu_raspberry_pi_visivel_internet/) ou acessível [via rede Tor](/blog/acesso_remoto_tor/), basta apenas você configurar o seu ambiente no Termux.

Primeiro, instale o SSH no termux:

    pkg install ssh

Crie o arquivo de configuração `.ssh/config` e gere suas chaves SSH conforme descrito [em nosso post anterior](/blog/acesso_remoto_seguro_raspberrypi_ssh/). Seu serviço agora pode ser acessado via `ssh meuservico`

Se você acessa o Raspberry Pi apenas via Tor, os passos seguintes são necessários. Instale o Tor:

    pkg install tor

Você precisa iniciar o Tor, mas o Termux não possui uma infraestrutura para gerenciar serviços (systemd, openrc, etc) tal como numa distribuição desktop. Você ainda pode iniciá-lo desta forma:

    tor &> /dev/null &

Este comando irá iniciar o tor no *background* e omitir qualquer output dele, tornando-o silencioso e transparente. Uma vez iniciado, você poderá acessá-lo via `torsocks ssh meuservico`

## Levando o Termux para o próximo nível

<figure>
    <img src="/static/images/mobile_accessories.jpg" alt="acessórios para seu smartphone" />
    <figcaption>
        Será que podemos tornar um smartphone num computador? De certa forma, sim!
    </figcaption>
</figure>

Você agora tem em mãos agora um ambiente Linux completo que pode acessar seu Raspberry Pi. Seu smartphone é literalmente um computador Linux!

Ainda assim, existem algumas limitações de hardware entre o seu smartphone e um computador laptop ou desktop completo, principalmente na interface de input (digitar comandos do Linux numa tela de toque é cruel), e no tamanho de sua tela. Ao passo que estes problemas não podem ser resolvidos apenas por software, existem algumas adições simples que podem melhorar muito a experiência.

A adição de um teclado externo é uma dádiva para quem está digitando comandos apenas numa tela de toque, e altamente recomendado para qualquer um que está trabalhando seriamente através do Termux. Alguns modelos de [teclados bluetooth sem conector](https://amzn.to/3avZLHX), que se conectam-se com os dispositivos apenas via handshake, são portáteis e ideais para "levar o trabalho com você." 
Alternativamente, adaptadores de USB-OTG [para MicroUSB](https://amzn.to/32FpM3f) ou [USB-C](https://amzn.to/2QRdty7) podem ser utilizados para conectar qualquer teclado USB diretamente no seu smartphone, tornando-se perfeito para usar em escritórios, etc. Você pode inclusive pode conectar um [hub USB](https://amzn.to/3vbBwXD) e assim utilizar ambos o teclado e o mouse (!!!) no Termux.

<figure>
    <a href="https://amzn.to/2QnI070"><img src="https://images-na.ssl-images-amazon.com/images/I/51vhLMusFML._AC_SL1200_.jpg" alt="acessórios para seu smartphone" /></a>
    <figcaption>
        Adaptadores USB podem ser utilizados para conectar periféricos de desktops no seu smartphone.
    </figcaption>
</figure>

No caso da tela, é um pouco mais complicado. [Adaptadores de USB-C para HDMI](https://amzn.to/2Qgta2g) existem, mas são raros os modelos de smartphone que realmente podem utilizá-los. Como este suporte não é dependente da versão do Android e sim do hardware do dispositivo, você precisa saber se o modelo suporta o protocolo [Mobile High-Definition Link](https://en.wikipedia.org/wiki/Mobile_High-Definition_Link) (MHL), que é utilizado com este acessório. Modelos como o [Huawei Mate 30](https://amzn.to/32ByWOa) ou o [Samsung Galaxy S9](https://amzn.to/3sI8soM), por exemplo, funcionam com este adaptador.

A alternativa simples é utilizar um dispositivo de *casting*, como o famoso [Chromecast](https://amzn.to/3tNF428), que transfere a imagem à tela HDMI via WiFi. Novamente esta não é uma solução perfeita por conta da utilização da banda do seu roteador wifi e algumas redes corporativas que não permitem comunicação multicast, mas pode auxiliar a experiência. Se nem isso é possível, um [stand de smartphone](https://amzn.to/3gxd6Uu) simples pode ser o mínimo.

## Limitações do Termux

Como nem tudo são flores, nem no mundo do Software Livre, temos que reconhecer as limitações do Termux em comparação ao Linux instalado no desktop.

A maior limitação do Termux como um aplicativo é sua dependência sobre o Android. Parte por conta do *chroot* do Linux, é impossível utilizá-lo no iPhone ou outras plataformas, o que é uma grande pena para usuários que gostam dos produtos da Apple.

Em seguida, há algumas diferenças entre a implementação do Termux e o Linux propriamente dito que podem entrar em conflito com alguns programas. Por exemplo, como não há um sistema `init` para gerenciar serviços, coisas que devem rodar no background devem ser iniciadas conforme o exemplo com Tor acima. A hierarquia do sistema de arquivos também é diferente, e certas localizações são mascaradas por links ou completamente removidas como `/usr/local`. Isto pode causar algumas surpresas operacionais.

Finalmente, o Termux sem "rooting" do dispositivo não possui permissões para certos acessos e operações no sistema Android, mesmo se você é usuário root dentro dele. Alguns programas disponíveis no Termux irão avisar desta limitação, outros não poderão nem ser executados sem este acesso. A maioria desta última classe, porém, está disponível num repositório separado.

Mesmo com tudo isso considerado, o Termux é um ótimo aplicativo para quem gostaria de trabalhar com o Linux fora de casa e em locais onde trazer o computador não é prático. Combinado com os acessórios indicados acima, é possível construir uma "estação de trabalho" portátil, que pode inclusive acessar seus recursos de casa remotamente. 

O Raspberry Pi Brasil altamente recomenda o Termux para quem precisa usar o Linux fora de casa.

---

Você já conhecia o Termux antes? Como faz para acessar seu Raspberry Pi do Celular? Compartilhe com a gente no [Mastodon!](https://qoto.org/@raspibrasil)
