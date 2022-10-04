<h4 align="center">Departamento Academido de Computação - Universidade Tecnológica Federal do Paraná (UTFPR)</h4>
<h5 align="center">Campo Mourão – PR – Brasil</h5>
<div align="center">henriquesantos@alunos.utfpr.edu.br</div>

<h1 align="center">
  <br>
  <img src="https://i.imgur.com/yMdJFrT.png" alt="Markdownify" width="600">
  <br>
  Compiladores
  <br>
</h1>

<h4 align="center">Projeto de Implementação de um Compilador para a Linguagem TPP</h4>

## Análise Léxica

### 1. Introdução

A análise léxica é a primeira etapa do processo de compilação de um código-fonte, nessa fase do processo o código é examinado e apartir disso são gerados tokens que representam cada lexema presente no ”texto”. Os tokens são definidos pela linguagem e fazem parte do modo de escrever empregado na mesma.

A linguagem que serviu de base para esse trabalho é a T++.

Este relatório está particionado em 4 seções que demonstram o funcionamento e a implementação do programa responsável por identificar os tokens a partir dos lexemas de entrada que identificam um código escrito na linguagem T++. Na seção 2 sera apresentada a especificação da linguagem, bem como os itens que definem toda a sua estrutura léxica, a seção 3 mostra a representação de cada lexema reconhecido pela linguagem por um dispositivo formal (DFA). A implementação bem como a biblioteca usada para esse projeto serão abordados na seção 4, além de exemplos de entrada e seus respectivos resultados na seção 5.

### 2. Especificação da Linguagem 

A linguagem descrita neste relatório é a  T++. A linguagem consegue reconhecer cerca de 35 tipos diferentes de lexemas, incluindo palavras reservadas. A linguagem pode ”reconhecer” desde nomes de variáveis  e funções, chamados de  identificadores, até números em diferentes notações e símbolos comuns em linguagens de programação, os tipos de tokens reconhecidos pela linguagem podem ser vistos na tabela 1.

<div align="center">
	
|lexemas | tokens|
|--------------------|---------|
|se | identificador|
|então | número inteiro|
|senão | número em ponto flutuante|
|fim | número em notação científica|
|repita | igualdade|
|flutuante | diferença|
|retorna | ou lógico|
|até | e lógico|
|leia | negação|
|escreva | adição|
|inteiro | subtração|
| | multiplicação|
| | divisão|
| | menor que|
| | maior que|
| | abre parenteses|
| | fecha parenteses|
| | abre colchetes|
| | fecha colchetes|
| | virgula|
| | dois pontos|
| | atribuição|
	
</div>
<h5 align="center"> Tabela 1. Tabela contendo todos os possíveis tipos de tokens reconhecidos pela linguagem T++</h5>

Na tabela 1 pode-se observar que as palavras reservadas da linguagem estão à esquerda da figura e representam exatamente o lexema usado no código, diferentemente dos tokens dispostos a direita, descritos dessa forma textualmente, mas no código são representados por símbolos diferentes.

### 3. DFA: Autômatos Finitos Determinísticos

Assim como a todas as linguagens livre de contexto, os lexemas usados pela linguagem podem ser descritos de uma maneira formal por meio de dispositivos formais tais como os autômatos finitos.

Um automato finito é composto por um conjunto de estados, um conjunto de símbolos reconhecidos pela linguagem, um conjunto de transições responsáveis por ligar os estados mutualmente, o estado inicial do automato e um conjunto de possíveis estados finais.

O estado inicial do automato é marcado com um triangulo na lateral esquerda,  os possíveis estados finais são denotados com um círculo na sua borda, além de seu rótolo que identifica o estado. As transições são identificadas pelos símbolos ou classe de símbolos (ex: letra) que possibilitam a troca de estados no automato, como pode ser visto na figura 1.

<div align="center">
<img src="https://i.imgur.com/qaagE7a.png" alt="Markdownify" width="500">
</div>
<h5 align="center"> Figura 1. Exemplo de automato que representa formalmente a identificação da linguagem responsavel por ”reconhecer” um número de ponto flutuante</h5>

Os autômatos têm uma forte ligação com as expressões regulares empregadas a cada tipo de lexema encontrado no código. As expressões regulares serão explicadas e exemplificadas na seção 4, onde serão abordados também assuntos com relação à aplicação dos autômatos e expressões regulares no reconhecimento desses lexemas.

Os autômatos servem, nesse caso, somente para formalizar as ”linguagens” livre de contexto reconhecidas no código, cada estado final de um automato ”reconhece” ou identifica os lexemas individualmente no texto, portanto não seria a abordagem adequada para este caso, já que a entrada para o lexer e um texto contendo vários lexemas.

### 4. Implementação

A implementação feita para esta etapa consiste na definição das expressões regulares, usadas para identificar os lexemas no texto de entrada, reconhecimento de possíveis erros (que se limitam nessa etapa a símbolos que não são reconhecidos pela linguagem de programação que o compilador está sendo desenvolvido) e o retorno de uma lista de tokens e seus respectivos lexemas reconhecidos do texto.

Todo o projeto foi desenvolvido na linguagem de programação Python com o auxílio da biblioteca PLY, uma biblioteca que auxilia no uso de ferramentas de parser de textos.

O texto é analisado pela biblioteca token por token até que a entrada de texto termine, assim quando passado um arquivo-fonte com o código na linguagem, todo ele e examinado para que se obtenha os tokens retirados do mesmo. Um novo token é buscado a cada um já encontrado, desde que o texto ainda possua símbolos válidos. 

#### 4.1. Expressões Regulares

As expressões regulares têm o propósito de identificar padrões textuais a partir de uma entrada, sendo assim possíveis identificar textos e símbolos que seriam muito difíceis de serem identificados com a leitura humana do texto ou que demandaria muito tempo para que isso ocorresse.

<div align="center">
<img src="https://i.imgur.com/JNvJ1nU.png" alt="Markdownify" width="600">
</div>
<h5 align="center"> Figura 2. Exemplo de expressao regular que identifica um ponto flutuante no texto de entrada</h5>

#### 4.2. PLY

A biblioteca PLY possui um procedimento específico quando se trata de reconhecer tokens de um texto, é necessário definir o token em uma lista e definir uma variável ou função com o nome do token e um prefixo t_ que definem a expressão regular desse token, como na figura 4.

<div align="center">
<img src="https://i.imgur.com/2OCFVfg.png" alt="Markdownify" width="300">
</div>
<h5 align="center"> Figura 3. Sintaxe de decaração usada na biblioteca PLY</h5>

### 5. Exemplos

Na figura 4 e 5 são mostrados alguns exemplos de entradas de texto na linguagem T++ e seus respectivos resultados após analise léxica aplicada na entrada.
 
 <div align="center">
<img src="https://i.imgur.com/nq9QS4o.png" alt="Markdownify" width="500">
</div>
<h5 align="center"> Figura 4. Exemplo simples de entrada e saída (I)</h5>


<div align="center">
<img src="https://i.imgur.com/QMBAHDw.png" alt="Markdownify" width="500">
</div>
<h5 align="center"> Figura 5. Exemplo simples de entrada e saída (II)</h5>

## Análise Sintática

### 1. Introdução

A análise sintática é uma técnica de análise de texto que visa identificar e classificar as estruturas sintáticas de um determinado texto. Essa técnica é muito útil para a compreensão de um texto, uma vez que ajuda a identificar as relações entre as palavras e as frases. Além disso, a análise sintática também pode ser útil para a tradução de um texto, já que ela permite identificar as estruturas sintáticas de um texto e, assim, facilitar a sua tradução para outro idioma.

Esta seção relata todos os pontos para a criação da parte sintática do compilador, mostrando o que é a gramática BNF, como ela funciona, como o Yacc ajuda na criação da sintática e mostrando os resultados dessa etapa.

### 2. Analise Sintática LALR.

Este programa trabalha com o analisador sintático do tipo LALR (look-ahead left-right), ou seja, ele analisa as informações provenientes da gramática BNF da esquerda para a direita e de baixo para cima, tentando deduzir as análises sintáticas e gerando uma tabela de ações do próximo estado.

O analisador sintático LALR é utilizado pelo fato de existirem muitos estados diferentes que possuem o mesmo conjunto de componentes, então para resolver isto ele combina esses estados e os expressa através de uma tabela LALR que é utilizada de forma mais simples e barata computacionalmente.

Além desses benefícios de se utilizar o LALR também temos a vantagem de sua análise ser realizada de maneira Botton-up, ou seja, as últimas regras mais à esquerda serão as primeiras a serem geradas, para melhorar a eficiência na hora de identificar uma informação. Isto ocorre, pois é mais barato computacionalmente você identificar um token nas regras que podem gerar Tokens, e ir subindo elas até chegar nó raiz, do que partir do nó raiz e ir buscar este Token.

### 3. Gramática BNF.

Para que o programa consiga captar as regras da linguagem e separar os significados das palavras na mesma, além da separação dos Tokens, também se faz necessário uma separação lógica dentro da própria linguagem, e para que essa separação seja possível uma gramática livre de contexto, ou BNF, foi utilizada.
 
Esta gramática consiste em um conjunto de regras que devem ser atendidas para que dado programa seja ou não aceito em uma linguagem, e que além de ser aceito também possa gerar uma árvore de recorrência para este programa que será muito útil nos próximos passos para se criar um compilador. Então, para gerar todos os possíveis caminhos dessa linguagem, as seguintes regras foram utilizadas:

Estas regras partem de um S’ que será sempre o nó raiz de uma árvore que será gerada, a partir dele um autômato de pilha vai buscando novos possíveis caminhos de escolha para que o programa no final seja aceito, se o mesmo for aceito a árvore é gerada através de uma imagem, todavia se for rejeito, um erro deve ser impresso mostrando a linha e coluna que ele ocorreu.


### 4. Implementação

#### 4.1. Yacc

O Yacc é uma ferramenta do python para facilitar na criação e na utilização da gramática BNF para geração da árvore de um compilador, ela possui vários métodos para geração de código e trabalha em conjunto com o Lex da parte léxica facilitando em muito a programação como um todo.
 
A primeira etapa que precisa ser feita para utilizar o Yacc e importar suas bibliotecas que podem ser vistas abaixo:
 
Nelas, além do ply.yacc que e a biblioteca padrão para geração de código, temos também mais duas coisas que precisam ser importadas, uma biblioteca de geração de código chamada anytree além de toda a parte léxica que já foi criada e explicada nos capítulos anteriores, para ser possível acessar os Tokens gerados anteriormente.
 
Após isso devemos criar funções que irão gerar a gramática BNF da linguagem, um exemplo dessas funções pode ser visto abaixo:
 
Como podemos observar, estas funções possuem o seguinte escopo, o nome da função primeiramente deve conter um p_ acompanhado de um nome, que será o nome dado a regra que irá ser criada na gramática, e como parâmetro dessa função se passa a palavra a ser verificada, logo em seguida temos a regra que deve ser tratada em formato de string, a primeira palavra dessa regra deve ser exatamente o nome dado a regra BNF, e depois dos”:”vem a regra em si (neste exemplo o nome e programa, e a regra e lista declarações), se esta regra for um conjunto final, então a frase é aceita e retorna ali, se for uma função ela continuará entrando até encontrar um final ou um erro. Além disso, também temos a parte de geração da árvore, ela utiliza da biblioteca anytree como já especificado acima e cria nós para cada interação nesta função onde este nó possui um nome e um filho que será dado quando esta função retornar da lista de declarações.
 
Existem algumas funções que possuem diferenças das demais, e estas são a p_error e a find_column, e elas podem ser vistas a seguir:
 
Elas são funções específicas para tratamento de erros, onde a p_error fica responsável por se algum erro for encontrado ele imprime o Token, a linha e a coluna deste erro, todavia para encontrar a coluna um cálculo um pouco mais complexo se faz necessário, então a find_column foi utilizada, onde se passa o Token e utilizando funções da lex e da yacc conseguimos a coluna do erro. 
 
E por último temos a parte de geração da árvore que irá utilizar os nós da anytree e gerar uma imagem jpg com a seguinte função:
 
Nela, se a função de erro não tiver sido acionada nenhuma vez, ela gera uma árvore com todos os nós e seus conteúdos.


#### 4.2 Árvore Sintática

Com todos os passos realizados a árvore gerada irá ser como a da imagem 3.

Nela podemos visualizar os nós gerados e os seus caminhos, além também de uma prova visual do bottom-up, pois os identificadores como já citado nas sessões anteriores no nó mais à esquerda de todos, e mais abaixo e terminam no nó raiz.

### 5. Exemplos
