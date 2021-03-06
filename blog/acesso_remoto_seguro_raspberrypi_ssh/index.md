# Acesse seu Raspberry Pi remotamente de forma segura com chaves via SSH

Um dos pontos fortes do Raspberry Pi é a sua versatilidade quando se trata de computação. Graças à sua crescente capacidade e recursos, é possível utilizar versões mais recentes como o [Raspberry Pi 4](https://amzn.to/3wfUopM) como um [computador Desktop completo](/blog/raspberry_pi_como_desktop/), mas seu uso como um servidor também continua como uma de suas [formas de utilização principais](/blog/como_escolher_seu_raspberry_pi/). Um servidor nada mais é do que um computador que provém serviços e com o qual trabalhamos remotamente, através da rede. Com o seu baixo consumo de energia, o Raspberry Pi é um candidato perfeito para este uso.

O desafio de se trabalhar remotamente com computadores é garantir a conexão à eles. É preciso garantir que os comandos e dados sejam transmitidos com sucesso, e com segurança para que não sejam obstruidos ou manipulados por fatores externos, especialmente quando transmitidos pela internet. Felizmente, todos estes problemas estão cobertos através de uma ferramenta chamada [SSH](https://en.wikipedia.org/wiki/Secure_Shell_Protocol) ou *Secure Shell*, que garante a transmissão e transmissão dos dados entre os dois computadores. O SSH é a ferramenta ideal para trabalhar com o Raspberry Pi à distância, e embora venha já habilitado por padrão, é necessário configurá-lo para providenciar segurança e conveniência adicionais.

Vejamos neste post como.

## Como funciona o SSH?

O SSH é um protocolo que acrescenta **criptografia** à conexão entre dois computadores. De maneira simplificada, os dados são criptografados (embaralhados por uma chave secreta) antes de serem transmitidos, e ao serem recebidos, são desembaralhados pelo destinatário. 

Esta criptografia segue um modelo chamado de [*Public-key Cryptography*](https://en.wikipedia.org/wiki/Public-key_cryptography) ou criptografia assimétrica que envolve um par de chaves criptográficas entre dois atores, as quais são responsáveis por embaralhar e desembaralhar o conteúdo. Há a chave *privada* que deve ser mantida em segurança e a chave *pública* que pode ser compartilhada com outros que desejam se comunicar.

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Public_key_encryption.svg/525px-Public_key_encryption.svg.png" alt="como funciona a criptografia assimétrica" />
    <figcaption>
        A criptografia assimétrica utiliza uma chave pública para criptografar conteúdo e uma chave privada para descriptografá-lo, tornando possível a comunicação privada. Crédito: Wikimedia.org
    </figcaption>
</figure>

Qualquer sistema operacional que possua o SSH habilitado produz seu próprio par de chaves para participar do protocolo, incluindo o [Raspberry Pi OS](/blog/como_instalar_linux_raspberry_pi/) que o possui habilitado por padrão. Portanto, para acessar seu Raspberry Pi na sua rede local uma vez que ligado e conectado, basta usar o seguinte comando:

    ssh usuario@endereçoip

Onde `usuario` é o nome do seu usuário no Raspberry Pi (por padrão, `pi` no Raspberry Pi OS) e `endereçoip` é o seu endereço IP da rede local. Você pode descobrir este endereço olhando os dispositivos conectados na página de administração do seu roteador, similarmente à forma de realizar o [Port Forwarding](/blog/tornando_seu_raspberry_pi_visivel_internet/).

Ao executar este comando, você verá uma mensagem perguntando se você confirma a identidade do computador remoto. Como você está na rede local, e é a sua primeira vez conectando ao Pi, não há risco em aceitar. Digite a senha do seu usuário no Raspberry Pi e você terá acesso remoto seguro via SSH como se estivesse trabalhando localmente.

Em relação ao acesso, o guia termina aqui. Porém, há alguns problemas relacionados com a utilização de senhas. O primeiro problema é que senhas podem ser vazadas ou - pior - adivinhadas por um adversário determinado. Uma vez comprometida, não há como garantir a segurança da sua conexão via senha apenas. Além disso, senhas precisam ser digitadas a cada utilização, o que pode se tornar cansativo dependendo do tipo de trabalho realizado.

Felizmente, há uma solução para ambos estes problemas: *autenticação por chaves criptográficas*. Esta é uma das melhores práticas na utilização do SSH, e pode ser facilmente implementada no Raspberry Pi como veremos a seguir.

## Habilitando e utilizando autenticação por chaves (passwordless)

Na autenticação por chaves, o computador local utiliza a sua chave privada para autenticar com sua chave pública armazenada no computador remoto, de maneira similar à criptografia assimétrica. Para utilizá-la, primeiro precisamos primeiro criar nosso par de chaves em nosso computador local. Assumiremos aqui a utilização do Linux também.

A suíte de software do SSH inclui utilidades para gerar e gerenciar chaves públicas e privadas. Podemos gerá-las com o seguinte comando:

    ssh-keygen -t ed25519
    
Siga as instruções da tela e especifique `mykey` como o nome do seu arquivo quando solicitado. A opção `ed25519` especifica o tipo de chave a ser utilizada, e este algoritmo é o mais recente e considerado mais seguro do que as outras opções como RSA e ECDSA, baseada em criptografia elíptica.

Este comando criará dois arquivos, `mykey` e `mykey.pub` correspondendo respectivamente às suas chaves privada e pública. Para protegê-las, arrange-as dentro de um diretório seguro chamado `.ssh` dentro do seu diretório home, que é de praxe do SSH:

    mkdir $HOME/.ssh
    chmod 700 $HOME/.ssh # limite o acesso apenas à você
    mv mykey mykey.pub $HOME/.ssh

Com estas chaves em mãos, precisamos agora configurar o Raspberry Pi para aceitar nossa chave como forma de autenticação. Para isso, copie a sua chave *pública* para o seu Raspberry Pi com o `scp`, que copia arquivos via SSH:

    scp $HOME/.ssh/mykey.pub usuario@enderecoip:/home/usuario/.ssh/ # envie a chave PÚBLICA

Digite sua senha para confirmar. Após a transferência, acesse o Raspberry Pi e adicione a chave para as chaves confiadas:

    cat mykey.pub  >> .ssh/authorized_keys 

> Observação: você pode adicionar o acesso de computadores adicionais (mesmos usuários ou não) simplesmente repetindo este processo até agora.

Agora você poderá acessar seu Pi sem precisar de senha através do comando:

    ssh -i $HOME/.ssh/mykey usuario@enderecoip # note que é a chave privada agora

> Aviso: sua chave privada agora é como a sua senha. Proteja-a e armazene-a num backup seguro para evitar problemas de acesso futuros.

## Automatizando o processo

O comando anterior, embora bem mais rápido que via senha, ainda continua um pouco maçante e comprido. Podemos ainda melhorá-lo e diminuir a necessidade de digitação através da elaboração do arquivo de configuração do SSH. Para facilitar este acesso, crie o arquivo `$HOME/.ssh/config` no seu computador local e insira o seguinte conteúdo nele:

    Host meuraspberrypi:
        Hostname enderecoip
        User usuario
        IdentityFile $HOME/.ssh/mykey

Agora você pode rapidamente acessar o seu Raspberry Pi da seguinte forma:

    ssh meuraspberrypi

Muito mais rápido, prático e seguro que a utilização de senhas!

## Pontos de segurança adicionais na internet

Ao passo que a utilização do Raspberry Pi na sua rede caseira local tipicamente não precisa de medidas adicionais de segurança, um dispositivo com [livre acesso à internet](/blog/tornando_seu_raspberry_pi_visivel_internet/) requer mais atenção em relação à segurança - especialmente num serviço de autenticação como o SSH.

A primeira recomendação é que, uma vez que o acesso via chaves for habilitado, **desabilite a autenticação remota por via de senhas**. Desta forma, você reduz a chance que algum adversário ganhe acesso ao seu sistema *mesmo sabendo a sua senha*. Para isso, edite o arquivo `/etc/sshd_config` no seu Raspberry Pi e adicione a seguinte linha:

    PasswordAuthentication no # se estiver "yes" basta trocar para "no"

A segunda recomendação é **trocar a porta do seu serviço SSH**, que por padrão é disponibilizado na porta 22. Muitos scanners automáticos maliciosos na internet procuram por esta porta padrão de serviços, e trocá-la por outra porta aleatória pode adicionar mais segurança. Ainda no Raspberry Pi, edite esta linha (que provavelmente estará comentada):

    Port 12345 # troque 12345 para um número aleatório que só você sabe!

Agora reinicie o serviço do SSH no Raspberry Pi:

    sudo systemctl restart sshd

Como a porta de serviços mudou, você deve editar sua configuração local para refletí-la:

    Host meuraspberrypi:
        Hostname enderecoip
        User usuario
        IdentityFile $HOME/.ssh/mykey
        Port 12345 # <-- coloque aqui o seu número escolhido

Após esta atualização, você poderá acessá-lo via `ssh meuraspberrypi` novamente.

## Outras possibilidades com o SSH

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/f/fb/FTP_model.png" alt="diagrama do FTP" />
    <figcaption>
        Utilizando SSH, é possível assegurar o antiquado FTP para torná-lo seguro de forma bem fácil. Crédito: Wikimedia.org
    </figcaption>
</figure>

Como o SSH providencia apenas uma camada segura de comunicação, é possível utilizá-lo em conjunto com outros protocolos ou aplicações sinergisticamente.

Uma das aplicações mais populares desta combinação é o [**SFTP**](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol) (Secure File Transfer Protocol) que combina a autenticação do SSH para transferir arquivos de maneira segura entre dois computadores. 

O SFTP corrige falhas de segurança presentes no antigo FTP sem a necessidade de utilização de certificados externos, e pode ser completamente automatizada graças à autenticação via chaves. Falaremos mais sobre este excelente serviço num post futuro.

Outra aplicação é o roteamento das conexões do seu computador usando um computador remoto como proxy e assegurando-a via SSH. Este é um conceito chamado **proxy-chaining** e pode servir como uma maneira simples de circunvir censura de rede (exemplo: filtros de internet em escolas e escritórios) e providenciar um pouco mais de privacidade.

---

Você já utilizava o SSH para acessar seu Raspberry Pi antes de ler este arquivo? Como configura o acesso remoto a ele? Compartilhe conosco no [Mastodon!](https://qoto.org/@raspibrasil)
