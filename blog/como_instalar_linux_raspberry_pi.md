# Como instalar Linux no Raspberry Pi?

Outline:

 - Recap of why Linux is the most recommended platform for the Pi.
 - How the process of installing differs from a usual distribution
 - Process of Installing and booting Raspbian (or Ubuntu Server?) in the Raspberry Pi.

Quando se trata de trabalho com *Single Board Computers*, [escolher o hardware](!LINK como escolher) é apenas metade da questão. Além da variedade de modelos que se encontram à disposição, escolher o [sistema operacional](https://pt.wikipedia.org/wiki/Sistema_operativo) (OS em Inglês), que proverá todo o suporte para o seu trabalho no seu SBC, é essencial.

A diversidade de sistemas operacionais disponíveis para SBCs como o Raspberry Pi é enorme, maior ainda que a de hardware, e a escolha de qual sistema utilizar pode ser um pouco confusa, especialmente se você nunca trabalhou com outro OS fora do Windows. Adicionalmente, a instalação de um OS no Raspberry Pi não segue um procedimento padrão de instalação onde se clica em menus e botões para avançar para os próximos passos e finalizar o processo. Felizmente, esta tarefa não precisa ser difícil; de fato, mostraremos passo a passo o processo.

Para os propósitos deste post, detalharemos o processo de instalação do sistema operacional [Raspbian](https://en.wikipedia.org/wiki/Raspberry_Pi_OS) (conhecido também como Raspberry Pi OS), uma distribuição Linux baseada no [Debian](https://www.debian.org) e desenvolvida oficialmente pela [Raspberry Pi Foundation](https://www.raspberrypi.org/software/operating-systems/). Embora Raspbian seja um dos sistemas mais populares utilizados no Raspberry Pi, ele certamente não é o único, e diversas outras distribuições de Linux podem ser instaladas com este processo, que como você verá, não é complicado.

Vamos em frente.

## Por que Linux?

Este artigo, tal como o site em geral, foca no Linux porque acreditamos que este é o sistema mais eficiente para um computador pessoal ou servidor com recursos limitados. As razões por trás desta decisão são várias.

Primeiramente, sistemas Linux (chamados de *Distribuições Linux*) são [Software Livre](!LINK free software), podendo desta forma ser instalados, copiados e modificados conforme necessário. Este ponto é essencial para o aprendizado, experimentação e pesquisas, onde pode ser necessário reinstalar do zero um sistema depois de um erro de configuração, ou instalar em diversas máquinas para a utilização em rede ou para simular outras interações entre sistemas - e claro, completamente **sem custo algum**.

A liberdade de modificação também significa que os sistemas Linux podem ter componentes não-essenciais removidos ou refatorados, tornando-os muito **mais leves e rápidos** ao serem utilizados. Em computadores com recursos limitados como o [Raspberry Pi 3](https://amzn.to/3qlUOqH), ou anteriores, esta diferença é crucial para uma experiência suave e prazerosa, ao contrário de um sistema pesado e lento.

Além da leveza e a flexibilidade do sistema, o Linux também é geralmente considerado um sistema **mais seguro** do que o onipresente Windows. Este é um ponto importantíssimo quando se trata de trabalhar com o Raspberry Pi como um servidor (onde múltiplos clientes e usuários podem acessar recursos dele) por longos períodos de tempo. Embora a segurança é crucial em todos os sistemas de computadores, quando um único desktop é comprometido, um único usuário é afetado. Quando um servidor é comprometido, todos os seus usuários estão em potencial perigo. Utilizar um sistema que é seguro por padrão e constantemente atualizado como o Linux é crucial.

Finalmente, há a inúmera possibilidade de **escolhas** quando tratamos do Linux. Não só temos a flexibilidade para modificar e construir nosso sistema como quisermos, mas também podemos escolher entre vários sistemas já disponíveis para nos servir da melhor maneira. Há imagens genéricas, prontas para uso do Raspberry Pi como um desktop, como o próprio Raspbian, outras prontas para servidores como o Ubuntu Server Edition, outras são mais minimalistas como o [Arch Linux](https://archlinuxarm.org), que permite você a construir seu sistema do zero.

Seguindo em frente, vejamos como instalar um sistema operacional no Raspberry Pi.

## Como o processo de instalação funciona no Raspberry Pi

Diferente da instalação num computador tradicional, onde primeiro insere-se a mídia de instalação do sistema operacional e os dados são copiados para a mídia de armazenamento,

## Instalando o Raspbian no Raspberry Pi