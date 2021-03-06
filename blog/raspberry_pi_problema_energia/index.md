# Evitando problemas de energia com o seu Raspberry Pi

Parte da popularidade do Raspberry Pi na cena dos [Single Board Computers](/blog/bem_vindo_ao_raspberrypi_brasil/) certamente provém do fato que seus periféricos e demais interfaces podem ser atendidos por dispositivos de computadores disponíveis comumente nas casas e escritórios atuais. É possível ligá-lo no próprio carregador de celular e conectar periféricos através de USB como um próprio [Computador Desktop](/blog/raspberry_pi_como_desktop/), tornando seu uso muito mais flexível e natural. Porém, mesmo com o Raspberry Pi aderindo a certos padrões, quando se trata de *energia* é preciso uma atenção especial para escolher uma fonte adequada para que todas as operações de computação sejam executadas de forma adequada sem danificar o equipamento por conta de uma voltagem ou amperagem inadequada. 

Embora fontes comuns de celular possam confortavelmente manter os modelos antigos do Raspberry Pi operando sem acessórios, esta situação muda com os modelos mais novos, que consomem mais energia para funcionar, ou quando plugamos periféricos que aumentam o consumo de energia do dispositivo. Ao passo que o consumo de energia é um ponto frequentemente ignorado pela maior parte dos usuários de computadores, no caso do Raspberry Pi a energia disponível é pouca e acontada, o que pode causar alguns problemas inesperados se não tomada a atenção. Neste post, veremos porque alguns problemas de energia podem ocorrer em certos casos com o Raspberry Pi, e como podemos evitar que aconteçam.

## Requerimentos mínimos vs recomendados de energia do Raspberry Pi

Todos os modelos do Raspberry Pi até a versão 3 foram pensados sob a ótica de compatibilidade com fontes comuns DC utilizadas por smartphones, padronizadas há muito tempo na voltagem 5V. Desta forma, até as velhas fontes daquele tocador de MP3 que você tinha desde 2003 são suficientes para alimentar um Raspberry Pi até o modelo 3 por si só. 

A partir do modelo 2, porém, o design do Raspberry começou a incorporar mais capacidade de computação e memória, o que começou a aumentar de forma significante o consumo de energia do design original. A compatibilidade da voltagem com fontes padrão de smartphone fora mantida, porém, e na ausência de qualquer outro periférico os modelos 2 e 3 ainda podem ser mantidos ligados.

A partir do modelo 4, o Raspberry Pi teve um salto significante de recursos, e seus requerimentos de energia se tornaram maiores do que o padrão de 5V das fontes de smartphone comuns. Ele passou a requerer sua própria fonte para operar de maneira correta, surpreendendo muitos acostumados com os modelos anteriores. 

A verdade, porém, é que desde o modelo 2, já era de conhecimento que uma fonte comum não poderia garantir *todas* as operações com o Raspberry Pi, especialmente quando combinadas com periféricos de USB. Prova disto é que a Raspberry Pi Foundation sempre manteve publicado ambos os [requerimentos *mínimos* e *recomendados* de energia](https://www.raspberrypi.org/documentation/faqs/#pi-power-specs) para cada modelo do Raspberry Pi. Portanto, ao passo que estes modelos acabam funcionando com uma fonte qualquer, isto não significa que eles garantem a operação em todos os casos.

Segundo a documentação da Raspberry Pi Foundation, os modelos do Raspberry Pi em geral possuem os seguintes valores de Voltagem e Amperagem *recomendados* para operar:

 - Model B: 5V / 1.2A
 - Model 2 a 3: 5V / 1.8A
 - Model 4: **5.1V** / 3A.

Para comparação, uma fonte de smartphone genérica consegue providenciar 5V a 0.7A apenas, o que é bem abaixo da capacidade recomendada para operações dos modelos 3 e anteriores, e insuficiente para o modelo 4 em diante. Se você trabalha apenas com o Raspberry Pi como um [servidor via acesso remoto](/blog/acesso_remoto_seguro_raspberrypi_ssh/), pode não encontrar problemas com energia numa fonte comum, mas ao plugar algum periférico como um teclado, pode se surpreender se o sistema inteiro sofrer um reboot por conta do pico de consumo de energia.

## Soluções para evitar problemas de energia na operação do Raspberry Pi

Se você está frustrado com a dificuldade de utilizar periféricos ou a capacidade total do seu Raspberry Pi via por conta de problemas de energia, há algumas soluções diferentes que você pode considerar: trocar a fonte ou a alimentação dos seus periféricos.

### Fontes com maior amperagem

Ao passo que hoje temos uma vasta disponibilidade de fontes para smartphones com "modo rápido" de carregamento, a verdade é que a maioria ainda segue o mesmo padrão 5V/0.7A decidido há quase duas décadas. Até mesmo as fontes "rápidas" operam em dois modos distintos, sendo o 5B/0.7A o *fallback* caso o dispositivo não suporte voltagens e amperagens maiores. E enquanto a voltagem da maioria das fontes é padronizada nos 5V, a amperagem pode variar significantemente - para cima ou para baixo.

Ao invés de "catar milho" buscando na gaveta uma fonte de celular apropriada, é muito mais eficiente procurar exatamente por uma fonte que atenda os requerimentos de energia recomendados do seu Raspbery Pi. E felizmente, [fontes que fornecem 5V/1.2A existem](https://amzn.to/33KgrrB) e caem como uma luva nos requerimentos da maior parte dos Raspberry Pis descritos acima.

Uma fonte com capacidade de amperagem mais alta é capaz de fornecer corrente elétrica adicional para quando o Raspberry Pi recebe um dispositivo USB conectado, não causando o reboot por falta de energia, e pode garantir o funcionamento no caso do uso de outros periféricos também. A grande vantagem é que mesmo que um pouco acima dos 1.2A recomendados pela documentação oficial, é possível também utilizar fontes com amperagem mais alta, como 1.5A, já que a demanda por corrente elétrica é controlada pelo dispositivo, não a fonte alimentadora. Até mesmo [fontes com 3A de alimentação](https://amzn.to/3w79HA5) podem ser utilizadas.

Ao fornecer ao Raspberry Pi a *capacidade* de corrente mais alta, o "pico de energia" súbito que causa problemas ao conectar USBs é mantido e resguardado, permitindo a continuidade do Raspberry Pi ininterrupta. Por outro lado, também é possível resolver o problema do *outro lado*: utilizando um hub USB auto-alimentado.

### Dispositivos e Hubs USB com fonte própria

<figure>
    <a href="https://amzn.to/3fnKP0c">
    <img src="/static/images/powered_usb.jpg" alt="Exemplo de Hub USB com fonte" />
    </a>
    <figcaption>
        Um Hub USB com fonte externa pode suprir energia aos seus periféricos sem drenar o Raspberry Pi.
    </figcaption>
</figure>

É possível também evitar o dreno de energia dos dispositivos periféricos simplesmente alimentando-os de outra maneira que não seja oriunda do Raspberry Pi. Alguns dispositivos, como [HD externos de mesa](https://amzn.to/3tLCA3f), possuem sua própria fonte de alimentação externa para funcionar pois consomem mais energia que uma porta USB convencional pode fornecer. Estes são os HDs recomendados para criar um [armazenamento caseiro como um NAS](/blog/compartilhando_arquivos_nas_raspberrypi/). Plugar o Raspberry Pi neste dispositivo já com fonte própria não causa consumo adicional a ele.

Alternativamente, alguns [Hubs USB](https://amzn.to/3fnKP0c) possuem alimentação própria também, funcionando tanto quanto uma forma de carregar dispositivos nele conectados quanto um hub de dados que não consome a energia do host. É possível, por exemplo, conectar o hub à tomada, conectá-lo ao Raspberry Pi e em seguida utilizar deste hub para conectar os demais periféricos, causando "interferência" mínima ao seu Pi.

### Fontes oficiais do Raspberry Pi Foundation

<figure>
    <a href="https://amzn.to/3ojEJlI">
    <img src="/static/images/fonte_rpi4.jpg" alt="Fonte Oficial do Raspberry Pi 4" />
    </a>
    <figcaption>
        A fonte oficial do Raspberry Pi 4 por enquanto é a única alternativa para alimentar este modelo, que possui requerimentos de Voltagem e Corrente únicos dentro da linha.
    </figcaption>
</figure>

Finalmente, não podemos deixar de frisar que a Raspberry Pi Foundation designou todo o hardware envolvido, incluindo as *fontes oficiais* que são as recomendadas ao operar o Raspberry Pi.

Segundo a Fundação, estas fontes são designadas para prover exatamente a energia necessária para o funcionamento de cada um dos modelos do Raspberry Pi, além de contarem com cabos resistentes e bem-isolados (a má-construção destes pode acarretar no aumento de resistência no circuito, reduzindo a potência que alcança o dispositivo para começar).

Fontes oficiais e homologadas são vendidas pela própria fundação e estão disponíveis no Brasil também. As [fontes para os modelos 1 a 3](https://amzn.to/3tT4xWW), por exemplo, fornecem energia à 5V 2.5A, sem precisar de um cabo USB extra. E no caso do audacioso [Raspberry Pi 4](https://amzn.to/3eO35Rp), acreditamos que não há alternativa à [fonte oficial do Raspberry Pi Foundation](https://amzn.to/3wcFLml) por conta também na mudança da voltagem necessária do dispositivo. A certeza, porém, é que ao utilizá-la, você terá corrente o suficiente para alimentar diversos dispositivos ao mesmo tempo - incluindo as 4 portas USB disponíveis.

## Conclusão

A [útilização do Raspberry Pi como um desktop](/blog/raspberry_pi_como_desktop/) é uma realidade com os modelos mais recentes, mas num mundo *low power* como este, pode ser necessário um pouco mais de atenção sobre o quanto entra e sai de energia no sistema total.

Embora fácil e rápido, simplesmente plugar seu Pi numa fonte velha de smartphone Android pode não suprir a corrente total necessária para torná-lo operacional em caso de conectar e desconectar múltiplos dispositivos USB, o que o causa dar reboot por falta de energia. 

Felizmente o problema pode ser resolvido de algumas formas simples, como utilizando uma fonte com amperagem maior ou um HUB USB com sua própria fonte. Em último caso, podemos utilizar as fontes oficiais desenvolvidas pela Raspberry Pi Foundation - no caso do [Raspberry Pi 4](https://amzn.to/3eO35Rp), por exemplo, é a única solução.

---

Como você faz para evitar problemas de energia com o seu Raspberry Pi? Você usa as fontes oficiais ou alguma outra solução? [Escreva pra gente no Mastodon!](https://qoto.org/@raspibrasil)

---

**Disclaimer:** o Raspberry Pi Brasil não é um órgão oficial da Raspberry Pi Foundation e não possui a documentação oficial referente às especificações de energia e de hardware do Raspberry Pi. Consulte a documentação oficial da [Raspberry Pi Foundation](https://raspberrypi.org) no caso de dúvida. O Raspberry Pi Brasil não se responsabiliza em caso de danos oriundos da utilização de qualquer informação deste site.
