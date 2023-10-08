<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://www.dropreal.com/br/wp-content/uploads/2021/03/icones_VALENDO.png" /></a>
</a>
<h1>Estudando Segurança de Sistemas de Informação.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda09">
<h2>Agenda 09: Testes de Software.</h2>
</div>

## 1. Introdução

- `qualidade de software`: o objetivo é garantir que tanto o processo de desenvolvimento quanto o produto de software atinjam os níveis de qualidade especificados.
- para isso, é necessário levar em consideração o `VV&T` (Validação, Verificação e Teste):
  - ***Validação***: 
    - Estamos construindo o produto certo? 
    - A validação consiste em assegurar que o produto final corresponda aos requisitos do usuário.
  - ***Verificação***: 
    - Estamos construindo corretamente o produto?
    - A verificação consiste em assegurar consistência, completude e corretude do produto em cada fase e entre fases consecutivas do ciclo de vida do software.
  - ***Teste***: examina o comportamento do produto por meio da sua execução.

## 2. Teste de Software

-  é um processo de checagem aplicado a programas de computador em diversas fases do desenvolvimento. 
- é um controle de qualidade que pode envolver etapas, desde a escolha das condições em que a aplicação será colocada à prova, até a simulação de uso real dela e o desenvolvimento de relatórios sobre os resultados obtidos.
- ***propósito***: verificar se o produto corresponde às funcionalidades esperadas no desenvolvimento e às necessidades dos usuários.
- ***qual a importância dos testes de software?*** Ajuda que o seu time encontre pequenos erros que atrapalham a emissão de documentos fiscais e bugs que levem à perda de desenvolvimentos avançados.
- trata-se de uma etapa essencial para que o produto final seja entregue ao cliente funcionando dentro das expectativas.
- há diversos tipos de testes que podem ser realizados para avaliar diferentes aspectos.

## 3. Principais tipos de teste de software

### a) Teste de Usabilidade:
- de suma importância para avaliar a qualidade do software quanto à experiência do usuário.
- finalidade: compreender o quão intuitivo, compreensível e inteligível é a interface do programa para o usuário final.
- é fundamental a compreensão de como o software será utilizado.
- exemplo: 
  - nem sempre a aplicação é executada em primeiro plano, o que leva a equipe a construir uma interface que permaneça agradável quando redimensionada.
- como os perfis de usuário variam a cada projeto, o teste de usabilidade é realizado com esses grupos de pessoas, de modo que elas opinem acerca da facilidade de uso, das questões visuais (cores, fontes, poluição visual etc.), entre outros detalhes que prejudicam a experiência de uso.

### b) Testes Funcionais:
- consiste em uma série de testes (técnicas), cujo objetivo é atestar se a aplicação é capaz de desempenhar as funções que se propõe a fazer.
- as técnicas mais comuns são os testes:
  - `caixa-branca`: tem como foco a análise do comportamento interno do software, ou seja, o seu código fonte.
  - `caixa-preta`: feito em cima das funções que devem ser desempenhadas pelo programa.

### c) Teste de Integração:
- está entre os principais tipos de teste de software.
- finalidade: analisar o comportamento do software quando interage com outras aplicações ou processos. 
- há diversas situações em que os testes de integração se mostram úteis: quando o software se comunica com um banco de dados ou servidor que estabelece a conexão dele com a internet, por exemplo.
- a ideia é compreender se o processo em questão gera alguma falha/instabilidade. O mesmo vale para aplicações a serem utilizadas em cooperação pelo usuário final.

### d) Testes de Performance:
-  são uma série de análises voltadas para o desempenho do software mediante várias situações.
- a partir dos diagnósticos, a equipe é capaz de compreender os limites do programa sob diversas condições.
- para constatar a qualidade da aplicação, ela é submetida a avaliações que simulam eventos e situações previsíveis de acordo com a rotina do cliente, ou seja, testes de carga, estresse e estabilidade. 
- quaisquer falhas detectadas durante o teste são corrigidas pela equipe precisa e cirurgicamente.

### e) Teste de Carga e Estresse:
-  o software, assim como o hardware, pode apresentar problemas quando recebe cargas altas de processos e requisições.
- isso acontece para mensurar se as condições nas quais ele será submetido não vão comprometer o seu desempenho.
- imprevisivelmente, a sobrecarga pode acontecer durante a utilização, gerando o que chamamos “estresse”. 
- para descobrir o nível de tensão capaz de levar o software a parar de funcionar, é executado o teste de estresse, que consiste em simular eventos de carga excessiva, forçando o software ao extremo.

### f) Teste de Estabilidade:
- a partir do momento em que se planeja construir um software para o cliente, é necessário que o produto final apresente certa estabilidade, condizente com a carga de trabalho a ser suportada diariamente.
- o ideal é que o software não sofra perda de performance depois de determinado tempo de uso.

### g) Teste de Regressão:
- é uma metodologia usada, entre outras coisas, para evitar a recorrência de um erro.
- exemplo: quando o programador modifica o código, seja para eliminar um bug ou acrescentar funcionalidades, e procura identificar falhas até então inexistentes.
- isso pode acontecer em função de problemas previamente corrigidos em uma versão anterior. 
- o teste de regressão é essencial para impedir que um sistema, após um update, assim que as atualizações forem instaladas, fique instável.

### h) Teste de Segurança:
-  é um dos mais importantes da lista, sobretudo quando falamos em software corporativo. 
- a proteção dos dados é imprescindível a toda e qualquer empresa que armazena informações no ambiente virtual — que é repleto de ameaças.
- esse teste é realizado por uma equipe especializada em Segurança da Informação, incumbida de avaliar se há brechas de segurança a partir de procedimentos, como análise de vulnerabilidade, coleta de informações e violação de senha.
- dessa maneira, o produto final só é entregue ao cliente quando os requisitos de segurança são devidamente preenchidos, garantindo à empresa que suas informações ficarão protegidas contra invasão cibernética.

## 4. TDD - TEST DRIVEN DEVELOPMENT / DESENVOLVIMENTO ORIENTADO A TESTE

- é parte da metodologia XP (Extremme Programming), também utilizado em diversas outras metodologias, além de poder ser utilizada livremente.
- o TDD transforma o desenvolvimento, pois deve-se primeiro escrever os testes, antes de implementar o sistema. 
- os testes são utilizados para facilitar no entendimento do projeto, usados para clarear a ideia em relação ao que se deseja em relação ao código.
- é a forma de "separar o projeto lógico do físico".
- a criação de teste unitários ou de componentes é parte crucial para o TDD. 

> "Os componentes individuais são testados para garantir que operem corretamente. Cada componente é testado independentemente, sem os outros componentes de sistema. Os componentes podem ser entidades simples, como funções ou classes de objetos, ou podem ser grupos coerentes dessas entidades.

- não é só o teste unitário que vai trazer o sucesso à aplicação, é necessário testar o sistema como um todo.
- "Os componentes são integrados para compor o sistema. Esse processo está relacionado com a busca de erros que resultam das interações não previstas entre os componentes".
- um sistema é um conjunto de unidades integradas, por este motivo é importante os testes unitários para ver se no micromundo tudo funciona, mas também temos de testar a integração, ou seja, ao integrar dois ou mais componentes, devemos realizar testes para verificar se a integração funciona.
- ***o que se ganha com isso?*** 
  - qualidade no código.
  - código mais simples e organizado.
  - documentação mais clara (componentização).










---

[Voltar ao início!](https://github.com/monicaquintal)