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

### [Exemplo 1](https://www.youtube.com/watch?v=DVdII76yiUg&feature=youtu.be):

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

- chamando a função:

~~~sql
select fnc_multiplica (8, 10) resultado;
~~~

> Quando temos uma aplicação que faz um select por diversas vezes durante um código, é mais simples fazer uma futura mudança apenas na procedure ou function. Caso contrário, haverá uma amarração por variável no código, ou teria que percorre-lo por completo para fazer as trocas.

### Exemplo 2:

- na tabela compra_produto, há campos quantidade e preco; criar uma
função que calcule o preço total a partir do conteúdo dos dois campos.

~~~sql
delimiter $$
create function fnc_preco_total (vl_unitario double, quantidade double)
returns double
begin
  set @r = vl_unitario * quantidade;
  return @r;
end $$
delimiter ;
~~~

- após a criação da function, utilizá-la apresentando todos os produtos que foram vendidos com o preço total de cada venda, calculado por meio da function fnc_preco_total.

~~~sql
select cp.*
    , fnc_preco_total(cp.preco, cp.quantidade) preco_total
  from compra_produto cp
~~~

- importante: coluna preco_total é definida como `alias` (apelido) do retorno.

### Exemplo 3: 

- criar uma function para obter o valor total de um compra.

~~~sql
delimiter $$
create function fnc_valor_compra (cod_compra int)
returns double
begin
  declare total_compra double;
  set total_compra = (select sum(fnc_preco_total(cp.quantidade, cp.preco))
      from compra_produto cp
      where cp.codigo_compra = cod_compra);
  return total_compra;
end $$
delimiter ;
~~~

- para obter o total de uma compra, achamos o preço total de cada produto vendido, por meio da function fnc_preco_total, antes de acumular o valor a partir da function SUM, do SQL.

~~~sql
select fnc_valor_compra(1) total_compra;
~~~
Obs.: O número 1 é o parâmetro correspondente ao identificador da compra que se deseja obter o total, o que significa que somente os registros dessa compra serão considerados na execução da função.

---

## Você no comando:

> Utilizar o banco de dados do consultório para desenvolver os exemplos.

### Requisitos que deverão ser implementados na integração:
1. Somente serão integrados os agendamentos recepcionados para realização de procedimentos de imagem.

2. Valorizar o procedimento após a confirmação de sua realização de acordo com o convênio.

### Criando as functions:

> Situação 1:

- a estrutura possui um campo tipo, preenchido com a letra I (procedimento de Imagem) ou C (Consulta), conforme demonstrado
com o comando select.
- criar uma function que receba o identificador do procedimento e retorne o seu tipo:

~~~sql
delimiter $$
create function fnc_tipo_proc (cod_proc int)
returns varchar(1)
begin
  declare tipo_proc varchar(1);
  set tipo_proc = (select p.tipo
    from procedimento p
    where p.pro_id = cod_proc);
return tipo_proc;
end $$
delimiter ;
~~~

- para executá-la:

~~~sql
select fnc_tipo_proc(1) tipo_procedimento;
~~~

- portanto, com a criação da function fnc_tipo_proc, quando necessitarmos verificar se um procedimento é de imagem, precisamos apenas chamá-la, passando como parâmetro o identificador do
procedimento.

> Situação 2:

- criar uma function específica de valorização do procedimento, centralizando a regra em um só lugar (criar uma function que receba o identificador do procedimento e do convênio e nos retorne o valor).

~~~sql
delimiter $$
create function fnc_valor_proc (cod_proc int, cod_conv int)
returns double
begin
  declare valor_proc double(10,2);
  set valor_proc = (select p.valor
    from convenio_procedimento_valor p
    where p.pro_id = cod_proc
    and p.convenio_id = cod_conv);
  return valor_proc;
end $$
delimiter ;
~~~

- executando a função:

~~~sql
select fnc_valor_proc(1, 1) valor_procedimento;
~~~

> Melhorando o procedure confirmar_realizacao_exame, substituindo a consulta para obter o valor do procedimento pela function:

~~~sql
drop procedure if exists confirmar_realizacao_exame;
--- exclui o procedimento anterior, de mesmo nome

delimiter $$
create procedure confirmar_realizacao_exame (in workl_id int)
begin
 select wa.agendamento_id
--  , cpv.valor - Substituir a exibição do campo valor pela chamada da
-- function func_valor_proc.
  , fnc_valor_proc(a.pro_id, a.convenio_id) valor
into @agend_id
 , @valor
 from worklist_aparelhos wa
 inner join agendamento a on a.agendamento_id = wa.agendamento_id
--  inner join convenio_procedimento_valor cpv
-- on cpv.pro_id = a.pro_id
-- and cpv.convenio_id = a.convenio_id
-- Retirar a junção que era responsável por definir o valor do procedimento
where wa.worklist_id = workl_id;


update agendamento a
 set a.realizado = 'S'
 , a.valor = @valor
where a.agendamento_id = @agend_id;
end $$
delimiter ;
~~~

- chamando a função:

~~~sql
select a.*
 , fnc_valor_proc(a.pro_id, a.convenio_id) valor_receber
 from agendamento a
where a.realizado = 'N';
~~~

---

## Fichário

IMPORTANTE: Utilizar o banco de dados imobiliária para resolver os exercícios.

1. Desenvolva uma function que retorne o nome do síndico passando como parâmetro o identificador do síndico. Depois utilize a function criada para desenvolver uma instrução que apresente os dados dos condomínios (nome, endereço) e o nome do síndico de cada um deles.

2. Desenvolva uma function que calcule o valor da taxa de condomínio a partir do valor do apartamento, passando como parâmetro o identificador do apartamento e o percentual aplicado ao valor para calcular a taxa. Depois utilize a function criada para desenvolver uma instrução que apresente os dados dos apartamentos (numero, valor) de um determinado condomínio e a taxa a ser paga.

---

[Voltar ao início!](https://github.com/monicaquintal)