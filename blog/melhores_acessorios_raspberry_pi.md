# Quais os melhores acessórios e periféricos para o Raspbery Pi?

Anteriormente no blog, exploramos os [vários tipos e modelos do Raspberry Pi](/blog/como_escolher_seu_raspberry_pi.html)  que podem te servir melhor para cada um dos seus objetivos em explorar o mundo dos *Single Board Computers*. Seja como Desktop ou Servidor, ou para as suas próximas invenções de IoT, existe um modelo de Raspberry Pi ou outro SBC que é perfeito para o seu próximo projeto.

Embora por si próprio um computador completo e inteiramente funcional (afinal, esta é a essência de um SBC), a performance e experiência de utilizar um Raspberry Pi podem ser muito melhoradas com a adição de alguns periféricos que extendem a capacidade e oferecem proteção ao equipamento. Afinal, o dispositivo é um SBC, e não um *All-in-one computer*... `;)` Mais capacidade, refrigeração, e algumas vezes proteção física contra os elementos são qualidades desejáveis à qualquer computador, e felizmente você pode oferecê-las ao Raspberry Pi através de alguns acessórios-chave. Neste post, detalharemos alguns dos acessórios que consideramos recomendados, ou algumas vezes indispensáveis para o seu Raspberry Pi. Venha com a gente!

## Case de proteção

O primeiro acessório recomendado é o [case de proteção](https://amzn.to/3qjZ7Ty) do Raspberry Pi. A placa dele é pequena e frágil, podendo ser danificada facilmente por conta de impacto, ou humidade demais. Um case provém uma proteção simples e eficaz ao seu Raspberry Pi, evitando que ele seja danificado acidentalmente.

O [case oficial do Raspberry Pi Foundation](https://amzn.to/3qjZ7Ty) torna o dispositivo claramente identificável com suas cores branca e vermelha e a logo estampada na tampa de maneira ainda bem compacta - o dispositivo continua cabendo na palma da mão:

![Comparação do tamanho do Raspberry Pi 4 - ele cabe na palma da mão](/static/images/raspi4_palm_size.jpg)

Existem ainda outros cases não-oficiais que também cabem no Raspberry Pi. Alguns são feitos de [outros materiais como alumínio](https://amzn.to/39w6Abn) que além de mais resistentes possuem um efeito de refrigeração passiva, além de outros designs e materiais (como [acrílico](https://amzn.to/3icPvqV)) e tamanhos. Todos são eficientes na hora de proteger seu Raspberry Pi.

## Heatsink e refrigeração

Embora possua baixo consumo de energia e poder computacional, o Raspberry Pi gera uma quantidade considerável de calor durante a utilização e, por conta da ausência de um sistema de arrefecimento, não consegue dispersar o calor tão eficientemente quanto um computador ou servidor tradicional. 

Portanto, a depender da temperatura do ambiente (quase sempre verdadeiro para o Brasil) ou da intensidade de uso, um sistema de refrigeração ou *heatsink* para seu Raspberry Pi pode se tornar necessário.

*Heatsinks* funcionam de forma passiva, sendo simplesmente peças que conduzem rapidamente o calor a fim de carregá-lo para fora do CPU por condução. Alguns cases possuem esta função embutida, especialmente se feitos de materiais metálicos, mas é possível comprar [*heatsinks* extras](https://amzn.to/35JxY4x) de alumínio para serem encaixadas dentro de cases existentes. Para usos de pouca intensidade como um servidor pequeno, um bom *heatsink* pode ser suficiente.

[![Heatsink com o Raspberry Pi](/static/images/raspberry_pi_heatsink.jpg)](https://amzn.to/35JxY4x)

Existem também sistemas ativos de refrigeração, que são um ventilador interno que refrigera o dispositivo similarmente aos de um computador tradicional. Alguns deles podem ser [montados diretamente na placa do Raspberry Pi](https://amzn.to/2Ly1h3b) através das interfaces PCIe, não sendo necessário a utilização das portas USB, e mantendo o conjunto de forma compacta. 

[![Resfriamento ativo via PCIe](/static/images/raspberry_pi_active_cooling.jpg)](https://amzn.to/2Ly1h3b)

Outros essencialmente são como [ventiladores externos com entrada USB](https://amzn.to/3srtCZx), que você pode colocar por cima dele e ligá-los utilizando uma das saídas USB disponíveis. Um pouco menos organizado, mas ainda assim eficiente.

[![ventilador externo USB](/static/images/external_fan_usb.jpg)](/static/images/external_fan_usb.jpg)

Particularmente, se você pretende utilizar o seu Raspberry Pi como um desktop, com várias aplicações gráficas e um navegador sendo utilizados simultaneamente, a demanda causa o dispositivo a se sobreaquecer rapidamente, podendo chegar a temperaturas até mesmo danosas ao CPU. Neste caso, o uso de refrigeração ativa é altamente recomendado.

## Fonte de alimentação

O Raspberry Pi e a maioria dos outros SBCs são designados para funcionar com uma fonte de Smartphone comum, operando a 5V DC e utilizando saídas MicroUSB ou USB-C para alimentação. Porém, a partir do modelo Raspberry Pi 4, o Raspberry Pi Foundation aumentou os requerimentos de alimentação, tornando a maioria das fontes de Smartphone incompatíveis com este modelo.

Como resultado, o Raspberry Pi 4 (e possivelmente os modelos futuros) precisam da [fonte oficial específica](https://amzn.to/3nEGcRG) com a amperagem correta para funcionar corretamente. A não utilização desta fonte poderá acarretar na danificação do dispositivo.

## Armazenamento

O Raspberry Pi precisa pelo menos de um cartão MicroSD para conseguir rodar um sistema operacional. Ao passo que estes se tornaram muito mais populares recentemente graças à popularização dos Smartphones Android, quando se trata de um SBC, são necessárias algumas considerações extras.

Primeiramente, a maior parte dos cartões MicroSDs antigos possui uma velocidade de leitura muito lenta em comparação a um HD ou outra mídia de armazenamento tradicional, o que reflete na performance do Raspberry Pi se utilizados (o computador parece "travar" de vez em quando, quando na verdade está apenas esperando os dados serem copiados).

Portanto, ao invés de abrir a gaveta e pegar o primeiro cartão SD que achar para instalar, é recomendado utilizar um [cartão MicroSD de alta velocidade](https://amzn.to/3oNsn4y), como aqueles que conformam aos [padrões modernos do MicroSD](https://en.wikipedia.org/wiki/SD_card#Class), como UHS-I ou UHS-II.

A segunda consideração é quanto ao tamanho do armazenamento. Enquanto a maior parte dos sistemas operacionais livres como Linux e FreeBSD cabem tranquilamente dentro de 8GB de espaço, pode ser necessário um espaço extra para armazenamento de dados e arquivos conforme o gosto e necessidades do usuário. Nossa recomendação é de pelo menos 32GB de espaço.

Porém, por conta das limitações e durabilidade reduzida dos cartões MicroSD, é melhor reservar ao cartão apenas o espaço necessário para o sistema operacional, e conectar qualquer capacidade adicional externamente, via saídas USB. Dependendo do seu caso de uso, você poderá utilizar desde [Pendrives comuns USB](https://amzn.to/2KgjXnn) de alta capacidade ou, quando baixa latência for requisito, [um HD externo](https://amzn.to/3sqMUy6) pode ser a única solução.

## As opções são inúmeras

E para você, qual é o melhor SBC para cada tipo de uso e por quê? Escreva sua resposta para a nossa [conta no Mastodon](https://qoto.org/@raspibrasil)!

Abraços e até o nosso próximo post!

Equipe Raspberry Pi Brasil
