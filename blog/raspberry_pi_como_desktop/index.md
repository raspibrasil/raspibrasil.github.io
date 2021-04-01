# É possível utilizar o seu Raspberry Pi como um computador desktop? Não subestime a sua capacidade!

A grande promessa (e charme!) do Raspberry Pi é dele ser um "computadorzinho" portátil e de baixo consumo de energia, disponibilizável em qualquer lugar: você pode trabalhar em seus projetos de software e aprender facilmente com ele, graças à flexibilidade e expansibilidade do [Software Livre](/blog/bem_vindo_ao_raspberrypi_brasil/). A própria [Raspberry Pi Foundation](https://raspberrypi,org), inclusive, considera o projeto como primariamente focado em educação na ciência da computação. Porém, nos últimos anos, os recursos e interfaces disponíveis no Raspberry Pi aumentaram significantemente, expandindo as possibilidades do objetivo original. Seria possível utilizá-lo como um computador comum Desktop?

O [Raspberry Pi 4](https://amzn.to/3wfUopM) lançado recentemente possui especificações similares à um desktop ou laptop mediano, e provavelmente foi designado com este objetivo em mente. Alguns o apontam como uma versão High-end do tradicional SBC, e a possível direção a ser seguida com os modelos futuros, podendo até mesmo um dia torná-los equivalentes ou competidores aos tradicionais Desktops. Mas será que a realidade prossegue com essa visão utópica? Neste post, exploraremos as possibilidades sobre utilizar o Raspberry Pi como um computador desktop padrão, e se é possível em 2021 substituí-lo por completo.

Vejamos a seguir.

## Recursos do Raspberry Pi comparado a outros computadores

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/RaspberryPiModelBRev2.by.Philipp.Bohk.jpg/400px-RaspberryPiModelBRev2.by.Philipp.Bohk.jpg" alt="Raspberry Pi Model B de 2012" />
    <figcaption>
        O Raspberry Pi Model B, lançado em 2012 é bem minimalista comparado aos outros SBCs e modelos atuais do Raspberry Pi. Crédito: Wikimedia.org
    </figcaption>
</figure>

Anteriormente, escrevemos sobre como o propósito de utilização pode afetar a sua decisão sobre [qual modelo de Raspberry Pi comprar](/blog/como_escolher_seu_raspberry_pi/). Peça-chave também nesta decisão é a quantidade de recursos estimados como necessários, e um Desktop tradicionalmente requer mais.

O Raspberry Pi certamente evoluiu desde o seu primeiro lançamento em massa em 2012 com o Modelo B. Na época, a plataforma era bem básica, com um CPU single-core de 700MHz, 512MB de RAM, duas portas USB, saída de vídeo HDMI e de áudio, e apenas conectividade via Ethernet cabeada. Esta era uma configuração comparável aos dos computadores de pelo menos 10 anos antes, mas pôde atender bem os requerimentos da época como um SBC puramente educativo, já que esta utilização não requeria muitos recursos inicialmente.

Com o lançamento do [modelo 3](https://amzn.to/2OiCeTe) em 2016, porém, o Raspberry Pi passou a se tornar muito mais próximo da configuração de um computador pessoal de uso geral. Foram adicionados conectividade WiFi, duas portas adicionais de USB, CPU Quad-core e a memória RAM aumentada para 1 GB. Talvez ainda "atrasado" em comparação aos computadores contemporâneos, mas já bem comparável a um laptop padrão em termos de conectividade e usabilidade de periféricos. Sem contar que, para um mero SBC alimentado por fonte USB, estes recursos eram e ainda são impressionantes.

<figure>
    <a href="https://amzn.to/3wfUopM"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Raspberry_Pi_4_Model_B_-_Side.jpg/400px-Raspberry_Pi_4_Model_B_-_Side.jpg" alt="Raspberry Pi Model 4B de 2019" /></a>
    <figcaption>
        O avançadíssimo Raspberry Pi 4B, com até 8GB de RAM, é comparável a um desktop ou laptop moderno. Crédito: Wikimedia.org
    </figcaption>
</figure>

Mais recentemente em 2019, o [Raspberry Pi 4](https://amzn.to/3wfUopM) fora lançado, essencialmente igualando seu plano entre os demais computadores tradicionais. Com um CPU ARM quad-core de 1.6 GHz e até *8 GB de RAM*, não há praticamente diferença entre o Raspberry Pi 4 e um computador desktop. Além disso, conectividade Bluetooth e WiFi de 5 GHz também foram introduzidas junto de duas saídas micro-HDMI, tornando-o comparável aos laptops modernos.

Com tantos recursos disponíveis, o Raspberry Pi 4 é o candidato mais próximo para substituir seu Desktop como um computador de uso geral. Porém, ainda é possível "exaurir" estes recursos quando utilizamos software ineficiente e pesado como o sistema operacional Windows, como você já deve ter experienciado várias vezes. Felizmente, existe uma ótima solução para este caso: o **Linux**.

## Maximizando o desktop e minimizando os recursos com o Linux

<figure>
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/WeeChat_2.7-rc1.png/800px-WeeChat_2.7-rc1.png" alt="Sessão de trabalho no Terminal Linux" />
    <figcaption>
        A leveza e flexibilidade do Linux garante que ele seja perfeitamente utilizável até com o mínimo de recursos, como por exemplo usando o terminal e a linha de comando. Crédito: Wikimedia.org
    </figcaption>
</figure>

O Linux é uma ótima escolha como o [sistema operacional do seu Raspberry Pi](/blog/como_instalar_linux_raspberry_pi/) pela sua leveza, rapidez e flexibilidade. Graças à flexibilidade e modularidade do Linux, é possível torná-lo mais leve ou robusto com base nas suas necessidades, o que o torna perfeito para plataformas modestas como um SBC.

Felizmente, até mesmo um sistema operacional gráfico e com todos recursos modernos como um navegador, suíte de produtividade e outros programas conseguem caber confortavelmente no Raspberry Pi 4 de 4 GB de RAM. A distribuição Raspberry Pi OS, que [demonstramos a instalação](/blog/como_instalar_linux_raspberry_pi/) anteriormente, já possui por padrão todos estes programas disponíveis. E ao passo que a utilização dos recursos varia de acordo com o uso, o Raspberry Pi OS consegue mantê-los relativamente estável uma sessão normal de uso.

<figure>
    <img src="!LINK" alt="Sessão de trabalho no Raspberry Pi OS" />
    <figcaption>
        O Raspberry Pi OS é um sistema operacional moderno que consegue confortavelmente providenciar um ambiente de computação como um tradicional desktop.
    </figcaption>
</figure>

Para testá-lo, por exemplo, colocamos nosso Raspberry Pi 4 numa sessão Linux padrão nossa de uso em laptops: navegador aberto, terminal com várias sessões abertas, gerenciador de arquivos e LibreOffice em uso. Consumo de memória máximo: !LINK GB RAM. A experiência também foi bem suave, sem "travar" o sistema e alternando tranquilamente. 

<figure>
    <img src="!LINK" alt="Sessão de testes do Raspberry Pi Brasil" />
    <figcaption>
        Exemplo da sessão de testes.
    </figcaption>
</figure>

Para uma utilização padrão, sem software muito específico, o Raspberry Pi 4 pode muito bem servir como um Desktop Tradicional.

## Limitações do Raspberry Pi como Desktop

Nossos testes foram realizados com um usuário médio, "surfando na internet" em mente. Se as suas necessidades de software são muito específicas, como edição de vídeo ou áudio, ou software de engenharia por exemplo, a sua experiência com o Raspberry Pi no Desktop pode ser bem diferente - ou até mesmo precária.

Para aqueles que procuram realizar trabalhos gráficos pesados em grande volume, o Raspberry Pi 4 pode não ser a melhor escolha para substituir o Desktop. Mesmo sendo capaz de reproduzir vídeo em resolução 4K, a GPU do Raspberry Pi pode ser limitada para processamento em massa de vídeos ou imagens de altíssimo tamanho. E mesmo se conseguir através, por exemplo, de Overclock, a temperatura e o consumo de energia aumentam significantemente, sendo necessário um [heatsink](https://amzn.to/35JxY4x) ou outro [acessório de arrefecimento](/blog/melhores_acessorios_raspberry_pi/) para evitar dano.

Por razão similar, o Raspberry Pi provavelmente não será sua melhor plataforma se você é um Gamer ávido. Além da maioria dos jogos não ser publicado para o Linux (exceto talvez via Steam), requerimentos pesados de gráficos não casam bem com o Raspberry Pi. Dito isto, ainda há algumas exceções notórias: o jogo [Minetest](https://minetest.org), versão software livre do famoso Minecraft, pode ser tanto hospedado quanto jogado no Raspberry Pi 4.

## O teste definitivo: 512 MB e Single-core como um Desktop?

Além do teste mencionado, nos propusemos a fazer talvez o teste mais profundo envolvendo um Raspberry Pi: usar o Raspberry Pi Model B de 2012 como um computador Desktop. Levaríamos ele ao limite!

Com 512 MB e um CPU single-core rodando em MHz, poucos diriam que este SBC teria alguma chance no mundo do desktop de 2021. Ainda assim, a equipe Raspberry Pi Brasil colocou o desafio a teste, realizando o equivalente a colocar um kart de 50 cilindradas para puxar um trailer de carga.

O veredito? **É possível, mas bem sofrido...**

<figure>
    <img src="/static/images/puppy_linux_raspib.jpg" alt="Raspberry Pi Model B rodando Puppy Linux" />
    <figcaption>
        Raspberry Pi Model B (2012) com 512MB RAM rodando Puppy Linux (Raspup).
    </figcaption>
</figure>

Primeiramente, sabíamos que o Raspberry Pi OS seria muito pesado para a tarefa, portanto optamos por uma distribuição Linux leve e especializada em computadores antigos: o [Puppy Linux](https://puppylinux.org). Um dos seus diferenciais é que ele roda diretamente da memória do computador, tornando-se assim muito mais rápido por diminuir o número de vezes que os dados são lidos ou escritos no disco, mas mesmo assim, a experiência é um pouco devagar no Model B de 2012.

<figure>
    <img src="/static/images/puppy_linux_stats.jpg" alt="Sessão do Terminal no Puppy Linux" />
    <figcaption>
        Sessão de terminal do Puppy Linux rodando no Raspberry Pi Model B. Note o consumo baixíssimo de RAM (79 MB!)
    </figcaption>
</figure>

O Puppy Linux carrega e roda o desktop sem problemas, mas é bem devagar por limitações do CPU. É possível abrir alguns aplicativos gráficos e até o navegador, mas o sistema se torna inaceitavelmente lento. Para aplicativos do terminal, o ambiente ainda é utilizável, mas ainda assim não faz o Model B como a melhor escolha como desktop.

Falaremos mais sobre esta distribuição, e como instalá-la no Raspberry Pi num post futuro.

## Conclusão

O [Raspberry Pi 4](https://amzn.to/3wfUopM) pode muito bem ser utilizado como um Desktop moderno quando combinado com um sistema operacional Linux, e para utilização padrão de software. Não será a melhor escolha para gamers ou outros usuários especialistas, mas em geral consegue realizar a tarefa bem.

Com a tendência dos SBCs de aumentar seus recursos daqui para frente, é interessante imaginar o conceito do Raspberry Pi substituindo um computador por inteiro no futuro, ou até mesmo escritórios ou bibliotecas inteiras substituindo seus PCs por Raspberry Pis compactos e baratos. Quem sabe dessa forma pode-se abrir uma Lan House completamente com Software Livre e por uma fração do Preço? Só o tempo dirá!

-----

Você já utilizou seu Raspberry Pi como seu computador desktop? Como foi a experiência? Já experimentou outra distribuição além do Raspberry Pi OS? Escreva para a nossa conta no [Mastodon](https://qoto.org/@kzimmermann)!

Abraços,

**Equipe Raspberry Pi Brasil**
