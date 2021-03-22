# Usando o Raspberry Pi como um NAS na sua rede caseira

Depois de [escolher o modelo apropriado](/blog/como_escolher_seu_raspberry_pi/) do seu Raspberry Pi e [instalar Linux nele](/blog/como_instalar_linux_raspberry_pi/), podemos finalmente começar a brincar com ele e experimentá-lo com várias soluções e *stacks* de software para nos servir da melhor forma. Afinal, é através destes constantes experimentos que podemos melhorar nosso entendimento e experiência com o [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/).

Uma das melhores formas de estudar o software livre é através da aplicação prática: procure um projeto que poderá ajudar você a realizar alguma tarefa, e aprenda com sua implementação. Neste artigo, mostraremos como é fácil tornar o seu Raspberry Pi num dispositivo de **armazenamento em rede** na sua casa através de um software chamado [Samba](https://www.samba.org), que permitirá você a compartilhar arquivos entre todos os dispositivos da sua casa, independente se rodarem Linux, Windows, Mac, Android, ou iOS.

Vamos em frente!

## Como o armazemanento em rede (NAS) funciona

Para este projeto, tornaremos o Raspberry Pi num dispositivo de [*Network Attached Storage*](https://en.wikipedia.org/wiki/Network-attached_storage) ou, abreviadamente, *NAS*. 

O NAS funciona como um servidor central de arquivos dentro da rede, com o qual outros computadores e dispositivos podem interagir para armazenar ou recebê-los. Se você já trabalhou num escritório onde haviam drives de redes disponíveis (F:\, G:\, etc.), o NAS via Samba funciona de forma quase idêntica.

<figure>
    <img src="https://cdn.ttgtmedia.com/rms/onlineImages/network_attached_storage_mobile.jpg" alt="arquitetura do NAS numa rede local" />
    <figcaption>O NAS atua como um ponto central através do qual outros dispositivos clientes podem enviar ou receber arquivos</figcaption>
</figure>

Da mesma forma que um servidor web utiliza o protocolo HTTP para enviar sites para navegadores da web, um servidor de arquivos "conversa" com computadores em rede através de um protocolo chamado SMB. O Samba é o servidor mais popular deste protocolo disponível para o Linux, e será o software que utilizaremos neste projeto.

## Requerimentos para este projeto

Para este projeto, graças à leveza do Samba junto ao sistema Linux, versões modestas do Raspberry Pi podem ser utilizadas para realizar a tarefa. Edições [orientadas à servidores](/blog/como_escolher_seu_raspberry_pi/) como o [Raspberry Pi 3B](https://amzn.to/3sb9NoL) podem muito bem manuseá-lo, assim como o poderoso [Raspberry Pi 4](https://amzn.to/2QuK0Kn) e até mesmo o primeiro modelo do [Raspberry Pi B](https://amzn.to/3vLW75S) de 2012 possui recursos suficientes para agir como um NAS caseiro.

<figure>
    <img src="https://images-na.ssl-images-amazon.com/images/I/71srygtslbL._AC_SL1131_.jpg" />
    <figcaption>O <a href="https://amzn.to/3vLW75S">Raspberry Pi Model B</a> original de 2012 pode servir como um NAS numa rede caseira de poucos dispositivos</figcaption>
</figure>

Para a parte de software, utilizaremos o *Raspberry Pi OS* como sistema operacional por conta da facilidade de se instalar e configurar software nele. Se você gostaria de mais informações sobre como instalar o Raspberry Pi OS, escrevemos anteriormente um [artigo descrevendo o processo passo-a-passo](/blog/como_instalar_linux_raspberry_pi/).

Uma *conexão de internet* no Raspberry Pi é necessária para instalar e configurar seu NAS, podendo tanto ser cabeada ou WiFi. Uma conexão cabeada é recomendada por conta da maior velocidade e estabilidade em relação ao WiFi, mas ambas funcionam.

Finalmente, é necessário ter espaço suficiente para armazenar os arquivos a serem compartilhados. Você pode utilizar armazenamento externo como um [Pendrive de alta velocidade](https://amzn.to/3fabSgW) ou um [HD externo](https://amzn.to/3f3UR87), ou armazenar diretamente no cartão MicroSD do seu Raspberry Pi.

## Instalando e configurando o Samba no Raspberry Pi

Primeiramente, instale o pacote `samba` no Raspberry Pi OS utilizando o seguinte comando no terminal:

    sudo apt-get install samba

Este comando também funciona no Ubuntu Server Edition para Raspberry Pi OS. `apt` listará as dependências necessárias para insalar o Samba. Pressione 'y' e Enter para prosseguir. 

Após a instalação, o serviço do Samba (`smbd` nos sistemas Linux) é iniciado automaticamente, mas ainda é necessário configurá-lo para fazê-lo funcionar da maneira exata que queremos. Em nosso caso, configuraremos o Samba para compartilhar apenas um diretório específico do nosso sistema, conhecido como *mountpoint* em inglês, e nos certificar que apenas usuários designados possam acessá-los.

Para isso, antes de começar a configuração, criaremos um usuário específico para acessar e manipular os arquivos via Samba. Você também poderia usar o seu usuário padrão para isso, mas por segurança é desejável ter um usuário específico para operar serviços. Desta forma, se por algum motivo o Samba seja comprometido, você poderá simplesmente deletar o usuário do Samba e recriá-lo - o seu usuário pessoal não será impactado.

Para criar o usuário `sambauser`, que será designado para o Samba, utilize o seguinte comando:

    sudo useradd -r -m -U -d /home/sambauser -s /bin/bash sambauser

Através deste comando, o usuário sambauser não terá uma senha associada a ele, outra medida de segurança que impede logins locais no sistema de serem realiados. Isso não é um problema, porém, porque todo o trabalho do sambauser será realizado remotamente através do serviço do Samba. Para isso, precisamos configurá-lo sob estas considerações.

Com o usuário criado, crie um diretório que servirá de *mountpoint* para o seu NAS. Você poderá criá-lo em qualquer lugar do seu sistema, inclusive em armazenamento externo. Neste exemplo, criaremos no próprio cartão SD do seu Raspberry Pi, dentro do diretório Home do seu usuário (por padrão, `pi` no Raspberry Pi OS) e concederemos as permissões corretas para que o usuário sambauser possa acessá-lo:

    mkdir /home/pi/NAS
    chmod 777 /home/pi/NAS

Com isso, podemos Como tudo no Linux, a configuração do Samba é feita através de um arquivo de texto simples, localizado em `/etc/samba/smb.conf`. Para editá-lo, abra-o com o seu editor de texto favorito prefixado com `sudo`, por conta de ser um arquivo do sistema. Por exemplo:

    sudo nano /etc/samba/smb.conf

A configuração padrão do Samba já é bem completa em termos de funcionalidade e segurança. Precisamos apenas adicionar o *mountpoint* desejado e quais usuários poderão ter acesso a ele. Adicione o seguinte segmento no fim do arquivo `smb.conf`:

    [NAS]
        comment = NAS on RaspberryPi
        path = /home/pi/NAS
        browseable = yes
        read only = no
        create mask = 0777
        directory mask = 0777
        valid users = sambauser pi
        guest ok = no

A linha `valid users = sambauser pi` especifica que apenas estes dois usuários terão acesso (via Samba) à este serviço (também é possível tornar o compartilhamento público, mas este não é o escopo deste artigo).

Finalmente, é necessário adicionar o usuário sambauser à lista de usuários autenticados pelo serviço Samba. Para este caso, será necessário adicionar uma senha para ele, válida apenas para o Samba. Guarde-a bem: **é com esta senha que você irá utilizar o Samba.**

    sudo smbpasswd -a sambauser

Para finalizar, reinicie o serviço do Samba no Raspberry Pi OS com o seguinte comando:

    sudo systemctl restart smbd

O samba estará rodando e compartilhando o diretório que você especificou como *mountpoint*. Para testá-lo, obtenha o seu endereço IP com o comando `ip addr`. No Windows, acesse `\\xxx.xxx.xxx.xxx\NAS$` do Windows Explorer, onde `xxx.xxx.xxx.xxx` é o endereço IP do seu Raspberry Pi. No Linux, acesse `smb://xxx.xxx.xxx.xxx/NAS` no seu gerenciador de arquivos favorito.

## Tornando o seu NAS mais eficiente

Seu NAS está pronto para trabalhar e compartilhar arquivos entre seus vários dispositivos da sua casa. Ainda há outras coisas que podem ser feitas para otimizá-lo caso você quiser, afinal o aprendizado sempre é constante no Linux, entre elas as seguintes:

 - Para garantir a confidencialidade da conexão entre o NAS e os dispositivos clientes, é possível realizar a transferência dos arquivos com um protocolo chamado **SFTP**, que emprega o famoso Secure Shell (SSH) para proteger a conexão e transferência dos arquivos. Falaremos mais sobre como implementá-lo junto ao SSH num artigo futuro.
 - É possível aumentar a velocidade da transferência usando armazenamento externo como um [HD](https://amzn.to/3f3UR87) ou até mesmo [SSD externo](https://amzn.to/3r9y5hu). Outra vantagem do SSD é que eles poderão durar muito mais tempo que um HD tradicional, por conta da ausência de falhas mecânicas e os ciclos reduzidos de escrita e leitura quando implementados apenas como armazenamento.

## Conclusão

Tornar seu Raspberry Pi num NAS caseiro para compartilhar arquivos entre seus dispositivos na sua casa não é complicado, e nem requer muitos recursos. Graças à simples implementação do Samba, é possível começar a compartilhar arquivos em questão de alguns minutos com apenas um pouco de configuração.

A implementação do Samba no Raspberry Pi exemplifica novamente como o aprendizado do [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/) se torna muito mais poderoso e apreciável quando envolve uma aplicação prática do conhecimento. Ao realizar este projeto, você estará tanto aprendendo mais sobre administração de sistemas quanto também realizando um serviço aos seus interesses. É sob esta combinação que o aprendizado flui.

----

O que você achou de tornar o Raspberry Pi num NAS para compartilhar arquivos? Conhece alguma outra solução para realizar este tipo de compartilhamento numa rede caseira? Deixe-nos saber na nossa [conta no Mastodon!](https://qoto.org/@raspibrasil)
