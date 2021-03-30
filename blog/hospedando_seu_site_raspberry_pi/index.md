# Hospede o seu site de graça na sua própria casa usando o Raspberry Pi

Há poucos limites sobre o que o seu Raspberry Pi pode fazer quando combinado com o poder e flexibilidade do [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/). Anteriormente, por exemplo, demonstramos como o é possível tornar o Raspberry Pi num [servidor NAS](/blog/compartilhando_arquivos_nas_raspberrypi/), permitindo o compartilhamento de arquivos entre os dispositivos da sua rede local. É com esta aplicação prática do Software Livre com o conhecimento que realmente podemos aprender como o nosso computador realmente funciona.

Seguindo os nossos estudos após aprender a utilizá-lo como um servidor e [torná-lo visível na internet](/blog/tornando_seu_raspberry_pi_visivel_internet/), daremos um passo à frente e mostrar neste artigo como você pode **hospedar o seu próprio site**, de graça, na sua casa com o Raspberry Pi. Esta é uma técnica conhecida como *self-hosting* e embora pareça complicado em princípio, a técnica é bastante simples e rápida de se implementar.

Vamos em frente.

## Instalando um servidor web no Raspberry Pi

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/500px-Client-server-model.svg.png" alt="como o modelo client-server funciona" />
    <figcaption>
    O modelo "cliente e servidor" utilizado na internet institui que vários dispositivos externos podem acessar o conteúdo provido por um servidor central através de uma rede, que pode ser a internet. Para hospedar um site, usamos um servidor Web. Crédito: Wikimedia.org
    </figcaption>
</figure>

Para hospedar um serviço, é necessário um servidor que o providencie em sua rede. No caso de um site na internet, este servidor é chamado de *servidor HTTP* (o protocolo através do qual os navegadores da internet "conversam" entre si), mais comumente conhecidos como servidores web.

Graças à popularidade deste tipo de serviço, hoje podemos contar com vários programas que são software livre disponíveis para atender à esta necessidade. Dentre os servidores web mais populares atualmente, se encontram o [Apache](https://httpd.apache.org/), [LigHTTPD](https://www.lighttpd.net/) e o relativamente recente [NginX](https://nginx.org/en/). Todos estes realizam bem o trabalho, e cada um deles possuem vantagens e desvantagens, mas neste artigo iremos focar no servidor Apache, que provavelmente é o mais utilizado entre os sites na internet hoje em dia.

O foco deste artigo é na distribuição Raspberry Pi OS, sobre o qual escrevemos [um tutorial detalhado de instalação anteriormente](/blog/como_instalar_linux_raspberry_pi/), mas os mesmos passos se aplicam para distribuições similares como Debian ou Ubuntu Server, que também possuem imagens para o Raspberry Pi.

Primeiramente, instalaremos o pacote do Apache no Raspberry Pi OS com o seguinte comando:

    sudo apt-get install apache2

Após a instalação, o Apache é iniciado automaticamente com configurações de segurança padrões ativadas, mas ainda é possível configurá-lo para poder funcionar da maneira que desejamos. 

Por padrão, o Apache servirá todos os conteúdos armazenados no diretório `/var/www/` para qualquer cliente que solicitá-lo, o que torna lançar uma versão "mínima" do seu site bem fácil. Para isso, crie um arquivo chamado `index.html` usando o seu editor de texto favorito com o seguinte conteúdo:

    <!DOCTYPE html>
    <html>
        <head>
            <title>Raspberry Pi!</title>
        </head>
        <body>
            <h1>Hello World! Eu sou um Raspberry Pi</h1>
        </body>
    </html>

Em seguida, mova este `index.html` para o diretório padrão do Apache:

    sudo cp index.html /var/www/

Finalmente, para confirmar que a página foi configurada corretamente, abra o navegador e acesse o endereço `http://localhost/`

<figure>
    <img src="/static/images/raspberry_pi_apache_server.jpg" alt="página sendo servida corretamente pelo Apache" />
    <figcaption>
    Página sendo servida corretamente pelo Apache.
    </figcaption>
</figure>

Parabéns, você publicou a sua primeira página na web.

## Configurando o acesso público dedicado ao seu Raspberry Pi

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d1/First_Web_Server.jpg/500px-First_Web_Server.jpg" alt="o primeiro servidor web da história, no CERN" />
    <figcaption>
    Este computador, configurado e instalado no CERN é considerado por muitos como o primeiro Servidor Web da história. Curiosamente, o software que utilizara para o serviço eponimamente se chamava "Web." Crédito: Wikimedia.org
    </figcaption>
</figure>

Seu site já se encontra disponível localmente mas, conforme vimos no post anterior, para disponibilizar qualquer serviço do seu Raspberry Pi fora da sua rede local, é preciso configurá-lo para ser [acessível na internet através do Port Forwarding](/blog/tornando_seu_raspberry_pi_visivel_internet/). Quando se trata de um site, porém, obter um domínio e acesso dedicado a ele é bem mais importante. É este domínio que você compartilhará com os outros visitantes para que possam acessar o seu site, e não o seu endereço IP.

Geralmente, para um site pequeno, um subdomínio com DNS gratuito pode ser suficiente para garantir que os usuários encontrem o seu site. Para isso, é possível utilizar o serviço do [No-IP](https://www.noip.com) para manter seu domínio apontando para o seu endereço de IP. Você pode criar uma conta gratuita nele e estabelecer o subdomínio em alguns minutos. Após isso, poderá compartilhar o endereço do seu site com todos na Internet!

## Ferramentas para criação de conteúdo no seu site

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Logo_of_Hugo_the_static_website_generator.svg/400px-Logo_of_Hugo_the_static_website_generator.svg.png" alt="Logo do gerador de sites estáticos Hugo" />
    <figcaption>
        Para gerar um site estático (HTML puro) programas como o Hugo ajudam bastante. Crédito: Wikimedia.org
    </figcaption>
</figure>

Sua página da web está já disponível, mas convenhamos que está bem básica e poderia melhorar um pouco. Para isso, é necessário criar conteúdo para o seu site na forma de mais páginas armazenadas dentro do diretório `/var/www/`.

Todo o conteúdo da web acessado por via de navegadores é escrito numa linguagem chamada HTML (Hypertext Markup Language) que é a que utilizamos para criar a "mini-página" na seção anterior. Há vários guias que ensinam como aprender esta linguagem na internet, sendo o guia apresentado pelo [HTML Dog](https://www.htmldog.com/) uma recomendação pessoal, pois este é bem didático.

Como escrever manualmente cada página em HTML pode ser um pouco maçante, existem algumas ferramentas que automatizam o processo de criação da página, permitindo que você foque na provisão do conteúdo (texto). Estas ferramentas são chamadas de [geradores de sites estáticos](https://jamstack.org/generators/). Talvez a mais famosa delas seja o framework [Hugo](https://gohugo.io), que permite a criação de páginas completas com templates já pré-elaborados. Outro bem conhecido é o [Jekyll](https://jekyllrb.com/), disponibilizado por padrão no Github.

O site do Raspberry Pi Brasil, por exemplo, utiliza um gerador de site estático próprio, escrito na linguagem Python. Se você tiver interesse em utilizá-lo, [acesse-o aqui no Github](https://github.com/raspibrasil/sitegen).

## Considerações e melhorias futuras

A configuração padrão do Apache pode servir-lhe bem para um servidor ou site pequeno, mas quando quisermos expandir nosso servidor com múltiplos serviços e sites independentes, precisamos ajustar um pouco a configuração. Isso é especialmente desejável no caso do [Rasbperry Pi 3](https://amzn.to/3qlUOqH) ou [Raspberry Pi 4](https://amzn.to/3slgdlW), que possuem bastante recursos para hospedarem vários serviços na web. 

Nesete caso, é necessário utilizar [Virtual Hosts](https://httpd.apache.org/docs/2.4/vhosts/examples.html), que permitem que múltiplos domínios e sites sejam acessados em paralelo numa mesma máquina física. Felizmente, esta configuração não é difícil, e a documentação do projeto do Apache é bem detalhada.

A utilização de um gerador de site estático pode ser suficiente para o gerenciamento de um blog ou site puramente informacional, mas dependendo do tipo de site que você estiver desenvolvendo, pode não ser suficiente, especialmente se depende do input dos visitantes para funcionar. Neste caso, um site dinâmico, alimentado por uma linguagem de programação backend como Python, PHP, Ruby on Rails ou Node.js é necessária, mas a implementação destas é um pouco mais complicada - e consome mais recursos. Falaremos mais como utilizá-los num post futuro.

## Conclusão

Hospedar seu site na internet usando o Raspberry Pi com sua conexão caseira não é complicado, e não vai lhe custar nada. 

Realizar o *self-host* do seu site é parecido com ir a algum lugar de bicicleta; personalizável, leve, requer algum esforço, mas certamente irá levá-lo até lá. Para sites pequenos, pode ser a melhor e mais barata solução! Porém, se você precisar de algo muito mais sofisticado, pode não ser a melhor estratégia, especialmente considerando a velocidade das conexões caseiras, e a quantidade de recursos que o seu Raspberry Pi poderá trazer. 

No fim do dia, este é mais um ótimo exercício para demonstrar o poder do Software Livre e a capacidade que pode trazer para a sua vida. 

O que você achou de hospedar o seu site gratuitamente com o Raspberry Pi? Possui uma forma melhor de gerenciar o domínio ou o conteúdo do seu site? Compartilhe com a gente no [Mastodon!](https://qoto.org/raspibrasil)
