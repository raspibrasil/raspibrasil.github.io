# Hello World! O que é o Raspberry Pi e o Software livre?

`Hello world!`

Somos a comunidade brasileira do Software Livre e dos *single board computers* como o Raspberry Pi. Neste blog, buscamos explorar e reportar todas as notícias sobre a computação de porte pequeno e de baixo consumo de energia, e sobre como o [Software Livre](https://www.gnu.org/philosophy/free-sw.en.html) como o GNU/Linux pode expandí-lo para obter qualquer solução que você precisar.

Embora alguns estejam familiarizados com estes termos, iniciantes podem se confundir com alguns dos termos que utilizamos aqui. Este post inicial servirá como clarificação e explicação inicial sobre todos os termos mais técnicos que aqui utilizamos. Venha conosco aprender mais!

## O que é o Raspberry Pi? Como ele difere de um computador tradicional?

O Raspberry Pi é um tipo de *single board computer* ([computador de placa única](https://pt.wikipedia.org/wiki/Computador_de_placa_%C3%BAnica), no Português) - ou SBC - desenvolvido pela [Raspberry Pi Foundation](https://www.raspberrypi.org/) na Inglaterra. O propósito principal do projeto desde sua concepção em 2012 foi de instruir e educar pessoas sobre a ciência da computação através de um computador financeiramente acessível e altamente configurável.

Como todo SBC, o Raspberry Pi é um computador completo construído numa única placa de silicone com todos os componentes - ex: CPU, Placa de Vídeo, saídas USB, placa de rede e adaptador WiFi - estão disponíveis no mesmo espaço compacto, que geralmente pode ser colocado facilmente numa [caixinha protetora](https://amzn.to/2WD8h0I). Acompanhado de uma fonte DC 5V -  equivalente a um carregador de smartphone Android comum - e periféricos como mouse e teclado USB e um monitor HDMI, um Raspberry Pi funciona perfeitamente como um pequeno computador desktop.

![Utilizando um raspberry Pi como um Desktop, completo com monitor e HD externo](/static/images/raspberry_pi_as_desktop_pc.jpg)

Porém, antes de jogar o seu PC fora e procurar o SBC mais próximo, saiba que o Raspberry Pi não é uma bala de prata e uma alternativa 100% a alguns tradicionais computador desktop (ainda). Na maioria das vezes, a limitação maior são os recursos como memória e capacidade do processador. 

A versão mais atual do Raspberry Pi (no momento desta publicação em Dezembro de 2020) por exemplo é o [Raspberry Pi 4B](https://amzn.to/34zoLuV), que possui 4GB de memória RAM e um processador ARMv8 quad-core 1.5GHz. Estas são especificações impressionantes para um SBC alimentado por fonte de celular, mas que provavelmente deixam um pouco a desejar para usuários mais *power users* ou que almejam utilizar seu computador para tarefas mais arrojadas como edição de vídeo ou áudio, ou jogos. 

Em comparação a um laptop, o Raspberry Pi também pode deixar a desejar em quesito de mobilidade, pois não possui bateria nem os acessórios periféricos como a tela ou teclado embutidos. Há projetos de hardware que buscam resolver estes dois casos, com talvez o mais famoso deles sendo o [PINE64](https://www.pine64.org/), que monta laptops e até smartphones utilizando a placa do Raspberry Pi como base.

Outra limitação é que o próprio hardware do Raspberry Pi, que utiliza um processador da [arquitetura ARM](https://www.arm.com/why-arm/architecture), não suporta ainda todos os sistemas operacionais existentes. Estes frequentemente focam na arquitetura x86, popularizada pela instalação do *Personal Computer* desde os anos 90, e ainda dominam o mercado. Software como jogos ou aplicativos proprietários específicos ainda não suportam esta plataforma amplamente.

Felizmente quase todo o software livre suporta a arquitetura ARM e roda muito bem no Raspberry Pi. Pelo menos cinco das [maiores distribuições Linux](https://distrowatch.com/dwres.php?resource=major) oficialmente suportam a arquitetura ARM, podendo ser instaladas no Raspberry Pi. Isto nos leva ao nosso próximo ponto: por quê você *deve* utilizar software livre em conjunto com ele.

## O que é o Software Livre e porque ele é a melhor escolha para o Raspberry Pi?

Se o hardware do nosso computador é um carro, o software certamente é o motor que lhe dá vida. A escolha do software que você instala e roda no computador é altamente responsável pela sua performance e a experiência que você tira ao utilizá-lo. 

Quantas vezes não nos frustramos com algum software que "dá pau" de vez em quando, ou que é extremamente lento para performar? Você acha que comprar um computador novo é a solução? Acredite, nossos computadores *não* envelhecem com o tempo - é o software que instalamos neles que se torna cada vez maior e menos eficiente. Quando utilizamos software não-livre como o Windows, que são proprietários e distribuidos somente pela Microsoft, não temos como nos livrar deste destino, senão por aceitá-lo e trocar de computador com frequência.

Embora não podemos controlar 100% a forma que o software é criado e atualizado, o [Software Livre](https://www.gnu.org/philosophy/free-sw.pt-br.html) oferece uma alternativa ao software que é desenvolvido atrás de portas fechadas e que ninguém consegue dizer ao certo como funciona, ou por que ele funciona de uma certa maneira. Quando o software é livre, [temos a liberdade](https://www.gnu.org/philosophy/free-sw.html) de utilizá-lo, modificá-lo (ou solicitar a modificação) e distribuí-lo como quisermos.

![The four software freedoms - Credit: Free Software Magazine](http://freesoftwaremagazine.com/articles/rule_1_hold_on_loosely/c20080905_four_freedoms.jpg)

Estas liberdades, combinada com o fato que o Software Livre frequentemente é mais seguro e eficiente do que o proprietário, tornam o Software Livre a implementação perfeita para ser utilizada com o seu Raspberry Pi. É através deste software que iremos torná-lo um computador que fará tudo o que desejamos dele no nosso dia-a-dia, seja um Desktop, servidor caseiro, servidor para um site pessoal hospedado na sua própria casa, drive de rede, ou servidor VPN para bloquear anúncios.

Quais Sistemas operacionais livres você deve usar, então? A escolha, como sempre, é sua, mas nossa recomendação é o [Ubuntu Linux](https://ubuntu.com/download/raspberry-pi), por ser simples e familiar de se utilizar e configurar, mas outras distribuições e o FreeBSD também são ótimos candidatos.

Combinando o Raspberry Pi e o Software Livre, temos uma plataforma de computação verdadeiramente completa para resolver todos os problemas que você tiver.

## Quais são os próximos passos para começar com o Raspberry Pi?

Se você leu até aqui e está interessado em aprender mais, assine o feed deste blog para não perder nenhum artigo que postamos aqui.

Seus próximos passos lógicos são escolher um modelo de Raspberry Pi (ou outro SBC) e feito isso, escolher qual Sistema Operacional irá instalar nele, e colocar a mão na massa! Falaremos mais sobre cada um destes passos nos nossos próximos posts.

O que você achou de começar a utilizar o Raspberry Pi? Conhece outros SBCs que também são interessantes? [Siga-nos no Mastodon](https://qoto.org/@raspibrasil) e nos conte o que achou!

Abraços!

*Publicado em 22 de Dezembro de 2020*
