<div align="center">
<a href="https://github.com/monicaquintal" target="_blank">
<img align="right" height="100" src="https://observatoriodabicicleta.org.br/uploads/2020/09/bancos-de-dados-nova-600.png" />
</a>
<h1>Estudando Banco de Dados</h1>
<p>Disciplina: Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda02">
<h2>Agenda 02: Funções.</h2>
</div>

- uma `rotina armazenada` é um subprograma que pode ser criado para efetuar tarefas específicas nas tabelas do banco de dados, usando comandos da linguagem SQL e lógica de programação.
- há dois tipos de rotinas armazenadas:
  - `Procedures`.
  - `Funções` (um pouco similares, mas possuem aplicações diferentes).

## Funções:

- invocadas de formas diferentes (call nos procedures x declaração nas funções).
- função é usada para gerar um valor que pode ser usado em uma expressão, geralmente baseado em um ou mais parâmetros fornecidos à função. 
- funções são executadas geralmente como parte de uma
expressão.

> O MySQL possui diversas funções internas, e ainda permite que sejam criadas as próprias funções!

### 1. Sintaxe para criação de uma função:

~~~sql
delimiter $$
create function nome_funcao ([parâmetros])
returns tipo_dados
begin
 /*corpo da função*/
return <expressão ou valor ou conteúdo da variável de retorno>;
end $$
delimiter ;
~~~

Onde:

- nome_funcao: nome que identificará a função; segue as mesmas regras para definição de variáveis, não podendo iniciar com número ou caracteres especiais (exceto underline “_”).
- parâmetros: opcionais e, caso não sejam necessários, devem permanecer apenas os parênteses vazios na declaração da function. Para que uma function receba parâmetros, é necessário utilizá-los dentro dos parênteses.
- returns: define o tipo de conteúdo que será retornado pela função.
- return: define a expressão utilizada para obter o resultado da função, pode também ser um valor ou uma variável. O resultado da expressão, o valor ou a variável, devem possuir conteúdo compatível com o tipo de dado da cláusula returns.

### 2. Sintaxe de declaração de parâmetros em Functions:

~~~sql
(nome tipo, nome tipo, nome tipo)
~~~

Onde:

- nome: nome do parâmetro, segue as mesmas regras de definição de variáveis.
- tipo: tipo de dado do parâmetro (int, varchar, decimal, etc).

### 3. Como invocar (chamar) uma Função:

~~~sql
select nome_funcao([parâmetros]);
~~~

## Exemplos:

> Para aplicar os exemplos, utilizado o BD minimercado, estudado na agenda anterior.

### Exemplo 1:

- função que receba dois valores inteiros e retorne o resultado da multiplicação entre eles:

~~~sql
delimiter $$
create function fnc_multiplica (a int, b int)
returns int
begin
  set @r = a * b;
  return @r;
end $$
delimiter ;
~~~




---

[Voltar ao início!](https://github.com/monicaquintal)