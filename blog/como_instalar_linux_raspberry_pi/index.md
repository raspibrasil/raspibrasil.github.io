# Como instalar Linux no Raspberry Pi?

Quando se trata de trabalho com *Single Board Computers*, [escolher o hardware](/blog/como_escolher_seu_raspberry_pi/) é apenas metade da questão. Além da variedade de modelos que se encontram à disposição, escolher o [sistema operacional](https://pt.wikipedia.org/wiki/Sistema_operativo) (OS em Inglês), que proverá todo o suporte para o seu trabalho no seu SBC, é essencial.

A diversidade de sistemas operacionais disponíveis para SBCs como o Raspberry Pi é enorme, maior ainda que a de hardware, e a escolha de qual sistema utilizar pode ser um pouco confusa, especialmente se você nunca trabalhou com outro OS fora do Windows. Adicionalmente, a instalação de um OS no Raspberry Pi não segue um procedimento padrão de instalação onde se clica em menus e botões para avançar para os próximos passos e finalizar o processo. Felizmente, esta tarefa não precisa ser difícil; de fato, mostraremos passo a passo o processo.

Para os propósitos deste post, detalharemos o processo de instalação do sistema operacional [Raspberry Pi OS](https://en.wikipedia.org/wiki/Raspberry_Pi_OS) (previamente conhecido como Raspbian), uma distribuição Linux baseada no [Debian](https://www.debian.org) e desenvolvida oficialmente pela [Raspberry Pi Foundation](https://www.raspberrypi.org/software/operating-systems/). Embora Raspberry Pi OS seja um dos sistemas mais populares utilizados no Raspberry Pi, ele certamente não é o único, e diversas outras distribuições de Linux podem ser instaladas com este processo, que como você verá, não é complicado.

Vamos em frente.

## Por que Linux?

<figure>
    <img src="/static/images/tux.png" alt="Tux, o mascote do Linux"/>
    <figcaption>Tux, o pinguim mascote do Linux</figcaption>
</figure>

Este artigo, tal como o site em geral, foca no Linux porque acreditamos que este é o sistema mais eficiente para um computador pessoal ou servidor com recursos limitados. As razões por trás desta decisão são várias.

Primeiramente, sistemas Linux (chamados de *Distribuições Linux*) são [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/), podendo desta forma ser instalados, copiados e modificados conforme necessário. Este ponto é essencial para o aprendizado, experimentação e pesquisas, onde pode ser necessário reinstalar do zero um sistema depois de um erro de configuração, ou instalar em diversas máquinas para a utilização em rede ou para simular outras interações entre sistemas - e claro, completamente **sem custo algum**.

A liberdade de modificação também significa que os sistemas Linux podem ter componentes não-essenciais removidos ou refatorados, tornando-os muito **mais leves e rápidos** ao serem utilizados. Em computadores com recursos limitados como o [Raspberry Pi 3](https://amzn.to/3qlUOqH), ou anteriores, esta diferença é crucial para uma experiência suave e prazerosa, ao contrário de um sistema pesado e lento.

Além da leveza e a flexibilidade do sistema, o Linux também é geralmente considerado um sistema **mais seguro** do que o onipresente Windows. Este é um ponto importantíssimo quando se trata de trabalhar com o Raspberry Pi como um servidor (onde múltiplos clientes e usuários podem acessar recursos dele) por longos períodos de tempo. Embora a segurança é crucial em todos os sistemas de computadores, quando um único desktop é comprometido, um único usuário é afetado. Quando um servidor é comprometido, todos os seus usuários estão em potencial perigo. Utilizar um sistema que é seguro por padrão e constantemente atualizado como o Linux é crucial.

Finalmente, há a inúmera possibilidade de **escolhas** quando tratamos do Linux. Não só temos a flexibilidade para modificar e construir nosso sistema como quisermos, mas também podemos escolher entre vários sistemas já disponíveis para nos servir da melhor maneira. Há imagens genéricas, prontas para uso do Raspberry Pi como um desktop, como o próprio Raspberry Pi OS, outras prontas para servidores como o Ubuntu Server Edition, outras são mais minimalistas como o [Arch Linux](https://archlinuxarm.org), que permite você a construir seu sistema do zero.

Seguindo em frente, vejamos como instalar um sistema operacional no Raspberry Pi.

## Como o processo de instalação funciona no Raspberry Pi

Diferente da instalação num computador tradicional, onde primeiro insere-se a mídia de instalação do sistema operacional e os dados são depois copiados para o disco rígido, no Raspberry Pi o processo é um pouco mais integrado, embora similar em conceito.

<figure>
  <a href="https://amzn.to/3l3UOuh"><img src="/static/images/sd_card.jpg" alt="Exemplo de MicroSD Card" /></a>
  <figcaption>Ao contrário dos computadores tradicionais, no Raspberry Pi você precisa extrair a imagem de instalação diretamente na sua mídia de armazenação</figcaption>
</figure>

Para instalar qualquer sistema operacional no Raspberry Pi, você precisa *extrair uma imagem* (arquivo `.img`) já pré-configurada deste sistema num [cartão MicroSD](https://amzn.to/3rA6QxW) que será utilizado nele. Se você nunca utilizou Linux antes (onde este é o processo padrão para criação de *Live Media*), este conceito pode parecer um pouco estranho, mas felizmente existem ferramentas didáticas que tornam o processo simples e rápido.

Se você usa Windows ou não está acostumado a lidar com a linha de comandos do terminal do Linux, o aplicativo [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager) desenvolvido pela Raspberry Pi Foundation é a maneira recomendada para fazer a instalação. Você pode baixá-lo para Windows, Mac e algumas das principais distribuições Linux como o Ubuntu e Debian. Felizmente, mesmo se a sua distribuição Linux não for suportada, ainda é possível instalar a imagem utilizando o comando `dd` do Linux, que veremos mais à frente.

Com um cartão MicroSD em mãos, vejamos na próxima seção como instalar o Raspberry Pi OS no Raspberry Pi.

## Instalando o Raspberry Pi OS no através do Raspberry Pi Imager

Primeiramente, baixe o Raspberry Pi Imager do repositório do [Raspberry Pi Foundation](https://www.raspberrypi.org/downloads/) para a sua plataforma. Uma vez instalada, abra o programa e verá a seguinte mensagem:

<figure>
    <img src="/static/images/rpi_imager_menu.jpg" alt="Menu principal do Raspberry Pi Imager" />
    <figcaption>Menu principal do Raspberry Pi Imager</figcaption>
</figure>

O Raspberry Pi Imager pode tanto baixar uma imagem de uma lista pré-inclusa nas suas opções (Raspberry Pi OS e Ubuntu Server Edition) e extraí-la para o seu cartão MicroSD ou utilizar uma imagem que você já baixou para o seu computador para extraí-la ao cartão MicroSD. Como neste caso estamos lidando com o Raspberry Pi OS, utilizaremos a própria função do Imager para baixar e instalar a imagem:

<figure>
    <img src="/static/images/rpi_imager_choosing_os.jpg" alt="Escolhendo uma imagem para baixar e instalar" />
    <figcaption>Escolhendo baixar a imagem do Raspberry Pi OS através do próprio Imager</figcaption>
</figure>

É possível também escolher uma imagem que você já baixou de outro lugar também através do aplicativo. Por exemplo, para instalar [Puppy Linux](http://www.puppylinux.org/), basta você primeiro baixar seu arquivo de imagem (terminando com a extensão `.img`) e escolhê-lo na interface do Raspberry Pi Imager:

<figure>
    <img src="/static/images/rpi_imager_custom_image.jpg" alt="Opção para escolher uma imagem customizada" />
    <figcaption>Opção do Imager para escolher uma imagem já existente no seu computador</figcaption>
</figure>

<figure>
    <img src="/static/images/rpi_imager_custom_image2.jpg" alt="Diálogo de escolha de arquivos .img" />
    <figcaption>Escolhendo uma imagem no seu computador</figcaption>
</figure>

Escolha em seguida o slot do seu cartão MicroSD (geralmente `/dev/sdb` ou `/dev/mmcblk0` no Linux) para o qual a imagem será extraída.

<figure>
    <img src="/static/images/rpi_imager_choosing_sdcard.jpg" alt="Escolhendo o dispositivo do SD Card" />
    <figcaption>Escolhendo o dispositivo do Cartão MicroSD</figcaption>
</figure>

> Atenção: ao realizar este procedimento, todos os dados do cartão MicroSD serão permanentemente apagados. Faça o backup destes dados antes de prosseguir.

Clique OK. O Raspberry Pi Imager baixará a imagem (dependendo do tamanho, pode demorar bastante), e em seguida automaticamente extraí-la para o seu cartão MicroSD.

Ao fim do processo, você poderá remover o seu cartão SD e inserí-lo no seu Raspberry Pi para começar a usar Linux nele. A instalação está concluída.

### Instalando através da linha de comando

Se você usa uma distribuição Linux não oficialmente suportada pelo Raspberry Pi Imager, não se preocupe: é perfeitamente possível extrair a imagem através da linha de comando (terminal). Para isso, o comando `dd` é utilizado.

Se o seu dispositivo do cartão SD é `/dev/mmcblk0`, e a sua imagem é `distro.img` o comando:

    sudo dd if=distro.img of=/dev/mmcblk0 bs=4M status=progress

Irá realizar a extração e preparo do seu cartão SD. Quando este terminar (pode demorar até 5 minutos dependendo do tamanho da imagem) você poderá utilizar o cartão SD no seu Raspberry Pi.

O comando `dd` é poderoso, mas a sua utilização errada pode causar a destruição dos dados armazenados no dispositivo. Por isso, deve ser utilizado com cuidado. Falaremos mais sobre este comando no futuro.

## Conclusão

Instalar Linux no Raspberry Pi é um pouco diferente de um computador comum, mas nem por isso é difícil. Utilizando-se do programa Raspberry Pi Imager, o processo é intuitivo, e usuários avançados podem utilizar a linha de comando para rapidamente realizá-lo. Uma vez realizada a instalação, você está pronto para começar a usar o Linux no Raspberry Pi. É um novo mundo, e falaremos mais sobre isso no futuro.

Você já instalou Linux no Raspberry Pi? Qual distribuição e qual método utilizou? Mande uma mensagem para nossa conta no [Mastodon!](https://qoto.org/@raspibrasil)

Abraços!

**Equipe Raspberry Pi Brasil**
