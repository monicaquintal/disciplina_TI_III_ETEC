<div align="center">
<a href="https://github.com/monicaquintal" target="_blank">
<img align="right" height="100" src="https://observatoriodabicicleta.org.br/uploads/2020/09/bancos-de-dados-nova-600.png" />
</a>
<h1>Estudando Banco de Dados</h1>
<p>Disciplina: Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda01">
<h2>Agenda 01: Blocos de Linguagem de Consulta Estruturada e bons estudos.</h2>
</div>

> Durante os estudos vamos acompanhar o desenvolvimento de uma integração entre dois sistemas. O MySQL possui vários recursos que auxiliarão nesse projeto, a programação realizada diretamente no banco de dados, agrupando instruções de acordo com as necessidades do negócio com certeza é um deles.

## Importante:

- os comandos da linguagem SQL são muito poderosos, mas normalmente consegue-se melhorar o desempenho das aplicações através da programação do banco de dados. 
- ao desenvolver módulos que sejam executados diretamente no servidor:
  - diminui-se o tráfego de informações na rede, 
  - esconde-se boa parte das estruturas das tabelas e
  - agiliza-se o processamento e retorno das
mensagens. 
- internamente o banco de dados possui mecanismos integrados que permitem unir as estruturas tradicionais de programação com os comandos SQL.

## Introdução:

- cada banco de dados possui um conjunto específico de comandos que definem a linguagem de programação do banco de dados. 
  - no caso do Oracle, a linguagem é o PL/SQL.
  - o SQL Server possui o Transact-SQL.
  - o DB2 possui sua própria linguagem de programação.
  - o PostGreSQL possui diversas extensões que podem ser utilizadas como linguagem de programação.
  - no MySQL não é diferente! 
- é possível criar módulos programáveis, como funções, procedimentos, objetos, pacotes, gatilhos etc. ***Em todos os casos, há um engine responsável pela integração e execução dos módulos no servidor de banco de dados***.

<img align="right" height="100" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" />

## MySQL:

### Variáveis
- suporta variáveis específicas com a sintaxe @nomevariável. 
- esse nome pode conter letras, números e os caracteres especiais ‘_’ (underline), ‘$’ (cifrão) e ‘.’ (ponto).
- as variáveis não precisam ser inicializadas. Elas contêm NULL por padrão e podem armazenar um valor inteiro, real ou uma string.
- sintaxe:

~~~sql
set @variável= { expressao inteira | expressao real | expressao string }
[,@variável= ...].
~~~

- também é possível atribuir um valor a uma variável em outras instruções diferentes de set. 
- neste caso o operador de atribuição é ``:=`` (dois pontos e igual) em vez de = (igual), porque = é reservado para comparações em instruções diferentes de set. 
- exemplo:

~~~sql
set @t1=0, @t2=0, @t3=0;
select @t1:=(@t2:=1)+@t3:=4,@t1,@t2,@t3;
~~~

### Blocos de comando:
- dependendo da rotina a ser executada, pode requerer várias consultas e atualizações na base, o que acarreta um maior consumo de recursos pela aplicação. 
- no caso de aplicações web, isso se torna ainda mais visível, devido a maior quantidade de informações que precisam trafegar pela rede e de requisições ao servidor.
- considerando que os servidores têm configurações melhores, utilizar o banco de dados para fazer parte do processamento pode ser uma saída para minimizar o consumo desses recursos.

> Mas como executar várias ações no banco de dados a partir de uma única instrução? 
- a solução são `Stored Procedures` (Procedimentos Armazenados).
  - são rotinas definidas no banco de dados, identificadas por um nome pelo qual podem ser chamadas. 
  - um procedimento desses pode executar uma série de instruções, receber
parâmetros e retornar valores.

## Usar ou não usar Stored Procedures: