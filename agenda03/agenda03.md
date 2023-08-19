<div align="center">
<a href="https://github.com/monicaquintal" target="_blank">
<img align="right" height="100" src="https://observatoriodabicicleta.org.br/uploads/2020/09/bancos-de-dados-nova-600.png" />
</a>
<h1>Estudando Banco de Dados</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda03">
<h2>Agenda 03: Gatilhos.</h2>
</div>

- é muito comum, em aplicações que utilizam bancos de dados, que ações sejam disparadas em resposta ou como consequência de outras, realizando operações de cálculo, validações e, em geral, surtindo alterações na base de dados.
- em muitos casos, programadores optam por executarem tais ações a partir da própria aplicação, executando várias instruções SQL em sequência para obter o resultado, solução que pode até ser tida como mais segura, mas tende a tornar ainda mais “pesada” a execução de certas tarefas, requisitando mais recursos da máquina cliente.
  - a “solução” (ou uma forma alternativa) é a utilização de TRIGGERS no banco de dados, automatizando certas ações com base em eventos ocorridos.

## O que é um TRIGGER (ou gatilho)?
- é um objeto de banco de dados, associado a uma tabela, definido para ser disparado, respondendo a um evento em particular. 
  - os eventos são os comandos da DML (Data Manipulation Language): `INSERT`, `DELETE` ou `UPDATE`. 
- podemos definir inúmeros TRIGGERS em uma base de dados, e para cada comando acima, podemos definir vários TRIGGERS.
- os TRIGGERS poderão ser disparados para trabalharem antes ou depois do evento.

## Definindo:

- podemos definir os TRIGGERS para serem disparados, por exemplo, antes (BEFORE) ou depois (AFTER) de um INSERT. 
- para cada momento BEFORE ou AFTER, podemos ter um TRIGGER a ser disparado para defender alguma lógica.
- sintaxe de um trigger:

~~~sql
create
  [definer = { user | current_user }]
  trigger trg_name trg_time trg_event
  on tbl_name for each row trg_stmt
~~~

<div align="center">

Palavra-chave | Significado/Função
--------------|------------------
***definer*** | - quando o TRIGGER for disparado, esta opção será checada para verificar com quais privilégios este será disparado.<br>- utilizará os privilégios do usuário informado em user (‘root’@’localhost’) ou os privilégios do usuário atual (current_user).<br>- caso essa sentença seja omitida da criação do TRIGGER, o valor padrão desta opção é current_user().
***trg_name*** | nome do TRIGGER.
***trg_time*** | define se o TRIGGER será ativado antes (BEFORE) ou depois (AFTER) do comando que o disparou.
***trg_event*** | define qual será o evento (INSERT, DELETE ou UPDATE).
***tbl_name*** | nome da tabela onde o TRIGGER ficará “pendurado” aguardando o trg_event.
***trg_stmt*** | definições do que o TRIGGER deverá fazer quando for disparado.

</div>

## Definir dados de antes (OLD) e depois (NEW):

- em meio aos TRIGGERS, há dois operadores que possibilitam acessar as
colunas da tabela alvo do comando DML, ou seja, acessar os valores que serão enviados para a tabela antes (BEFORE) ou depois (AFTER) de um UPDATE, por exemplo.
- esses operadores permitirão ter dois momentos, o antes e o depois, podendo examinar os valores para que sejam ou não inseridos, atualizados ou excluídos da tabela.
- diretrizes:

<div align="center">

Evento | Diretrizes
-------|-------------
***INSERT*** | - ***NEW.nome_coluna*** permite verificar o valor enviado para ser inserido em uma coluna de uma tabela. <br>- ***OLD.nome_coluna*** `não` está disponível.
***DELETE*** | - ***NEW.nome_coluna*** `não` está disponível.<br>- ***OLD.nome_coluna*** permite verificar o valor excluído ou a ser excluído.
***UPDATE*** | ***OLD.nome_coluna*** e ***NEW.nome_coluna*** estão disponíveis, antes (BEFORE) ou depois (AFTER) da atualização de uma linha.

</div>

- ou seja: 
  - ao inserir uma nova linha em uma tabela, temos os valores das colunas disponível através do operador NEW.nome_coluna.
  - quando excluímos uma linha, temos ainda os valores das colunas da linha excluída através do operador OLD.nome_coluna.
  - temos os dois operadores disponíveis no UPDATE, pois essa declaração seria como um DELETE seguido por um INSERT.

## Criando o primeiro trigger:

> utilizar o BD minimercado, tabela compra_produto.

- o trigger validará se os dados foram passados em uma declaração INSERT antes (BEFORE) que sejam cadastrados na tabela de exemplo. 
- validaremos a quantidade comprada igual ou menor que 0 (zero) e, caso isso aconteça, atribuiremos a quantidade 1 (um), garantindo que toda compra sempre tenha valor positivo para acquantidade.

> vídeo tutorial [aqui](https://www.youtube.com/watch?v=bSrPAhFguNc).

1. clicar para abrir a estrutura da tabela.
2. será apresentada a estrutura; clicar em Triggers.
3. clicar no "+" para implementar o código do trigger (nesse caso, BEFORE INSERT).
4. inserir o código do trigger:

~~~sql
-- utilizando variáveis
set @qtd_comp = new.quantidade;
-- validando se quantidade é igual ou menor a 0
if (@qtd_comp) <= 0 then
-- atribui 1 se a quantidade for inválida
set new.quantidade = 1;
end if;
~~~

5. clicar no botão Apply, e em seguida, Finish.
6. criado trigger na tabela compra_produto.

### Importante:

- ao tentarmos inserir um registro de compra de produto onde a quantidade é menor ou igual a 0, o TRIGGER ao ser disparado atribuirá o valor enviado para 1 (um) através do operador NEW.nome_coluna. 
- como na Tabela de exemplo a coluna quantidade foi configurada com
valor default 1, se não for definido conteúdo o valor 1 será atribuído automaticamente.

### Inserindo um registro sem a definição da quantidade:

~~~sql
-- inserindo um registro na compra com o código 2 (dois):
insert into compra_produto (codigo_compra, codigo_produto, preco)
  values (2, 1, 8.90);

select *
  from compra_produto;
~~~

- no exemplo acima, mesmo não sendo definido um valor para o campo quantidade, o valor 1 (um) foi definido automaticamente.

### Inserindo um registro definindo uma quantidade menor ou igual 0:

~~~sql
-- inserindo mais um registro na compra com o código 2 (dois):
insert into compra_produto (codigo_compra, codigo_produto, quantidade, preco)
  values (2, 1, -1, 8.90);

select *
  from compra_produto;
~~~

- no exemplo acima, mesmo sendo definido um valor menor que 0 (zero) para o campo quantidade, o valor 1 (um) foi definido, por ação do TRIGGER.

## Excluindo um TRIGGER:

- sintaxe:

~~~sql
DROP TRIGGER trigger_name;
~~~

- pela interface gráfica do Workbench, é possível acessar a área de TRIGGERs da estrutura da Tabela, assim como fizemos para criá-la (clicar em "-").









---

[Voltar ao início!](https://github.com/monicaquintal)