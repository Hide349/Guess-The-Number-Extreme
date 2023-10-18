<h1 align="center">
    <p align="center">Guess The Number Extreme</p>

</h1>


## Índice

- [Sobre](#sobre)





## Sobre

Uma versão melhorada do primeiro projeto, (https://github.com/Hide349/Projeto_Circuitos_Digitais). Nesse jogo algumas coisas foram adicionadas, como por exemplo um cronômetro, placar, valores negativos e duas coordendadas para serem chutadas tornando assim o jogo bem mais divertido e dinâmico.

## Universidade

Projeto feito para disciplina de circuitos digitais do professor Ramon Santos na universidade **Universidade Federal do Cariri**. (https://www.ufca.edu.br/). 

## Ferramentas

- [Logisim](https://github.com/Logisim-Ita/Logisim)
- [java](https://www.java.com/pt-BR/)

## Clonar


```bash
    #Execute
    git clone https://github.com/Hide349/Guess-The-Number-Extreme.git
```
```bash
    #abrir logisim
    $ java -jar LOGISIM-ITA.jar 
```


## Por onde começar?
<p>Existem vários caminhos possíveis para concluir o projeto, o que eu escolhi dá o primeiro passo montando a tela que será apresentada para os jogadores, depois fazendo o cronômetro,chutes de x e y, alternador de jogadores, números aleatórios e fim de jogo<p>


## Tela 

<p>Para montar a tela é simples, basta usar a imagem de exemplo e copia-la</p>

<img src="./assets/tela.png"/>

Copiando a tela, a nossa ficará desse jeito.

<img src="./assets/tela1.png">

## Cronômetro

Com a tela montada, precisaremos criar cada componente dela para que o jogo funcione.Portanto, começaremos com o cronômetro.Para monta-lo, utilizaremos de quatro unidade de memória flip flop do tipo d, um somador e vários túneis

<img src="./assets/cron1.png">

## Funcionamento

Cada flip flop é responsável por guadar um bit, um cronômetro são basicamente 4 contadores. Dois de 0 até 9 e dois de 0 até 5. Com isso em mente percebe-se que essa é o primeiro dígito do cronômetro da esquerda para direita, ou seja, um contador de 0 até 9. Nesse caso, vai ser subtraido 1 até zero_A ser verdadeiro. Quando isso acontecer, utilizando dos preset e clear os flip flops vão ser obrigados a guardar o valor 1001 que seria o nove.

**Resumindo** : Esse seria um contador que vai de 9 até 0 e quando chega em zero volta para o nove. E o próximo contador teria um pulso de clock para decrementar uma unidade.

Repetindo a lógica faríamos mais três desses, em que dois seriam de 5 até 0( **dezenas** ) e mais um de 9 até 0( **unidades** ).

#### Partes restantes

<img align="center" src="./assets/cron2.png">

<p></p>
<img align="center" src="./assets/cron3.png">

<p></p>

<img align="center" src="./assets/cron4.png">



## Chutes de x e y

<p>O jogo precisa de duas coordenas. O jogador chuta essas duas e então é informado se a soma delas é igual, menor ou maior que as soma das coordenas geradas.Bom, para fazer isso precisaremos de uma máquina de três estados, para assim termos o estado chutando x, chutando y e verificando. Isso para ambos o jogadores claro.</p>

#### Máquina de três estados

Para fazer uma máquina de três estados precisaremos de dois fliop flops do tipo d e uma porta and.Além de que, esse estado será atualizado quando o botão próximo for pressionado.

<img src="./assets/m3.png">

<p></p>

O primeiro estado seria o chutando x, com o and dois barrado (00), o segundo estado seria o chutando y que seria o q do segundo flip flop (01) e o estado verificando seria o (10). Com os três estados agora precisamos guardar os valores de chutando x e y e mostrar seus valores nos displays.

## Chutando x e y
<p></p>


<img src="./assets/chutandoxy.png">

<p>
<p>
<p>Um valor com 4 bits será passado, o que precisamos fazer é direcionalo para o flip flop correto. Por isso, o clock dele, ou seja, oque decide se ele pode ser ou não atualizado é um and que consiste do estado dele, um not verificado(apenas por garantia) e o botão chutar. Isso garante que apenas seja atualizado o valor quando estiver no estado correto e o botão chutar for pressioando.<b>A mesma coisa vale para y</b>.Depois disso é só mostrar o valor, fazendo com que o bit a3 seja o negativo ou positivo</p>

## Alternando Jogadores

<p>Para alternar entre dois jogadores teremos que utilizar dois flips flops, mas por que se são só dois estados? Na verdade, é importante lembrar que cada jogador tem o estado chutando x e chutando y. Então na verdade são 4 estados.</p>

<img src="./assets/alternarab.png">

#### Lógica

O jogador só será alternado quando ele já tiver feito dois chutes, ou seja, estar em estado de verificado e clicar em próximo de novo. **turnout a** (significa que o tempo de a chegou ao fim) então deve forçar que entre em b jogando, o mesmo funciona para **turnout b**. Além de que, a e b só podem estar jogando se nenhum dos dois teve ser tempo esgotado.

## Alternat inputs

<p>Com os jogadores alternando temos que alternar de onde vai ser a entrada de dados, apra isso utilizaremos uma sequência de portas and com os estados a jogando e b jogando.</p>

<img src="./assets/inputab.png">

#### What?

<p>Os bits 0,1,2,3 podem receber ou valores de an ou bn. Para isso utilizaremos 4 portas or.Bom, para a0,a1,a2,a3 serem passados o jogador a tem que estar jogando e a mesma lógica vale para o jogador b.Por isso a sequência de portas and.Depois é só mostrar os valores que estão sendo passados</p>

## Somador de coordenadas

<p>Com as coordenadas em mãos temos que soma-las e checar se sua soma é maior,igual ou menor que as que foram geradas aleatoriamente</p>

O somador de coordenadas é um pouco diferente do comum, o bit a3 ou b3 signfica que a coordendada passada é negativa e para isso nós teremos que transformar o somador em um subtrador.

## halfadder

<img src="./assets/halfadder.png">

## fulladder
<img src="./assets/fulladder.png">

## adder(-)
<img src="./assets/adder(-).png">

A lógica para faze-lo é simples, o processo é o padrão no entanto a3 e b3 são bits que indicam se vai ser um subtrador ou um somador.

#### Usando adder(-)

<img src="./assets/somador(-).png">


## Gerando números aleatórios

<p>Agora é preciso gerar coordenadas aleatórias que serão comparadas com as chutadas pelo jogador.</p>

Utilizaremos o gerador de número aleatório oferecido pelo logisim, apenas o modificaremos para mudar o valor toda vez que um jogador acertar.

