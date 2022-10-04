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

### 2. Discussão sobre o formato na Análise Sintática realizado pela ferramenta (se é LL(1), LR(1), LALR(1), SLR(1), etc).

### 3. Gramática no padrão BNF.

### 4. Implementação

#### 4.1. Yacc

#### 4.2 Árvore Sintática

### 5. Exemplos
