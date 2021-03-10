# Como escolher o seu primeiro Raspberry Pi?

Olá mundo, e feliz ano novo atrasado! Desde que publicamos [nosso primeiro artigo explicando o que são o Raspberry Pi, SBCs e o Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/), a grande pergunta que ficou foi: diante de tantos modelos de SBCs (e do próprio Raspberry Pi)  existentes, como escolher aquele que é o melhor para nós?

Pensando nesta dúvida frequente entre os iniciantes no Single Board Computing, elaboramos este artigo para tirar suas dúvidas e informá-lo da melhor maneira possível para dar o seu primeiro passo neste mundo incrível de aprendizado e realização.

Venha conosco!

## Objetivos e Recursos

A sua decisão em qual SBC é o melhor para você provém principalmente de duas grandes variáveis: o seu **objetivo** em usar o dispositivo, e quanto de **recursos** você necessitará.

O seu objetivo pretendido ao utilizar o seu Raspberry Pi ou SBC poderá afetar significantemente a sua escolha final. Por exemplo: você pretende utilizá-lo mais como um computador Desktop, conectando um monitor, teclado e mouse nele? Ou pretende utilizá-lo mais como um servidor em rede, instalando-o em algum lugar remoto na casa e administrando-o através da rede? Ou está pensando em sair um pouco do mundo do software e quer montar máquinas e mexer com hardware?

Embora seja possível alcançar cada um dos objetivos acima com qualquer SBC, alguns são mais apropriados para cada uma destas tarefas.

### Desktop

Versões recentes do Raspberry Pi, especialmente a partir do [modelo 4](https://amzn.to/3slgdlW), são análogas a um computador desktop e em muitos casos possuem especificações iguais ou melhores que alguns deles. Nossa recomendação é que pelo menos 4 GB de memória RAM sejam dedicados para o uso de um SBC como uma alternativa a um computador Desktop, e com bastante conectividade USB ou sem fio para conectar periféricos.

Com 4 a 8 GB de memória, o [Raspberry Pi 4](https://amzn.to/3slgdlW) funciona bem como uma reposição de um computador Desktop, consumindo significante menos energia e apresentando uma interface gráfica familiar e eficiente quando combinado com o poder do [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil.html). A presença de WiFi e Bluetooth integrada no chip torna-o ainda mais poderoso, possibilitando você a conectar seus periféricos sem fio facilmente, e conectar a uma rede caseira sem fio com facilidade.

Um outro projeto de SBC projetado pela Asus, o [Asus Tinkerboard](https://www.asus.com/us/Single-Board-Computer/Tinker-Board/) possui especificações parecidas com Desktops tradicionais, podendo até mesmo exibir vídeo em resolução 4K. É uma alternativa interessante ao Raspberry Pi como um Desktop.

### Servidor

O Raspberry Pi também funciona bem como um servidor em rede por conta do seu baixo consumo de energia, tamanho compacto e suas especificações bem-posicionadas para pequenos servidores. Por conta do consumo relativamente menor de recursos em comparação aos computadores desktops atuais, até modelos mais antigos do Raspberry Pi, como o [Raspberry Pi 3](https://amzn.to/3qlUOqH) com 1GB de memória, podem ser suficientes nestes casos.

Graças à eficiência e dos sistemas operacionais livres disponíveis para servidores, é possível colocar um SBC com recursos relativamente modestos performando bem como um servidor pessoal. Como resultado, o consumo de energia e a geração de calor também são bastante reduzidos, podendo algumas vezes não precisar de refrigeração para serem mantidos.

Outras alternativas para esta forma de utilização incluem outros fabricantes de SBCs como o [Banana Pi](https://en.wikipedia.org/wiki/Banana_Pi), ou o [BeagleBone](https://amzn.to/35GN62I).

### Integração de Hardware e IoT

Quando se trata de projetos com foco em Hardware - por exemplo: sensores, controle remoto, Internet of Things (IOT) - ainda é possível utilizar o Raspberry Pi para diversos projetos, dado suas interfaces diversas de comunicação, e a possibilidade de extendê-lo através da [interface PCI Express](https://en.wikipedia.org/wiki/PCI_Express) com periféricos extras de forma compacta. Porém, neste campo o campeão indiscutível é o projeto [Arduino](https://www.arduino.cc/).

Não há apenas um único "modelo" de Arduino: você adquire as placas contendo o CPU e as arruma conforme as suas necessidades de hardware. É possível integrá-lo com [sensores de ambiente](https://amzn.to/3bEImOT), [motores](https://amzn.to/3oMeofz), e [inúmeros outros periféricos](https://amzn.to/3bGXjje) para adaptá-lo perfeitamente às suas necessidades.

O Arduino também integra o lado do software em seus produtos, com todos os componentes sendo programáveis através de linguagens de programação como o C ou [Python](https://amzn.to/3qnhcju). É uma forma prática de trazer um projeto de software para a vida real.

## Apetrechos e periféricos

Embora utilizável por si próprio, a performance e experiência do Raspberry Pi podem ser melhoradas com a adição de alguns periféricos que extendem sua utilização e oferecem proteção ao equipamento. 

Como recomendação mínima, recomendamos a utilização pelo menos de um [case de proteção](https://amzn.to/3qjZ7Ty) para a frágil placa do Raspberry Pi e, no caso do Raspberry Pi 4, a [fonte oficial do Raspberry Pi Foundation](https://amzn.to/3nEGcRG), já que modelos a partir desta versão possuem uma amperagem um pouco maior do que as fontes de celular comuns. E se utilizado como um computador desktop, recomendamos também a compra de um [*heatsink*](https://amzn.to/35JxY4x) por conta do calor gerado por seu processador mais poderoso.

Para saber mais sobre os diversos acessórios para complementar e melhorar a experiência do Raspberry Pi, preparamos para você um post exclusivo sobre o assunto: [Quais os melhores acessórios e periféricos para o Raspberry Pi?](/blog/melhores_acessorios_raspberry_pi.html)

## Guia rápido de escolha

Sumarizando o post e para facilitar a sua escolha, segue abaixo um guia rápido descrevendo as escolhas recomendadas para o seu primeiro SBC dependendo do seu caso de uso:

 - **Desktop**: [Raspberry Pi 4](https://amzn.to/3slgdlW), de 4 a 8GB de RAM, ou Asus Tinkerboard.
 - **Apenas como servidor**: [Rasberry Pi 3B](https://amzn.to/3qlUOqH), [BeagleBone](https://amzn.to/35GN62I).
 - **Projetos de IOT ou customização de hardware**: [Arduino](https://amzn.to/3bGXjje).

Estas três categorias provavelmente cobrirão a maior parte dos casos de uso, mas dada a abundância de alternativas é possível ter combinações bem variadas de hardware na sua jornada.

E para você, qual é o melhor SBC para cada tipo de uso e por quê? Escreva sua resposta para a nossa [conta no Mastodon](https://qoto.org/@raspibrasil)!

Abraços e até o nosso próximo post!

Equipe Raspberry Pi Brasil
