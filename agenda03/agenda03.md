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

## Criando novo TRIGGER:

- para atualização automática da quantidade em estoque a partir da compra de um produto pelo cliente.
- utilizar o gatilho de ***AFTER INSERT***, ou seja, após a inserção.

~~~sql
update produto
 set quantidade_estoque = quantidade_estoque - new.quantidade
where codigo_produto = new.codigo_produto;

-- sendo: 
-- quantidade_estoque = quantidade do produto atualmente em estoque
-- new.quantidade = quantidade do produto comprada pelo cliente
~~~

- para evidenciar a execução do TRIGGER, verificar o saldo atual dos produtos cadastrados no estoque.

~~~sql
select * from produto;
~~~

- simular a venda de um dos produtos e depois verificar como ficou o saldo:

~~~sql
insert into compra (data, cpf_cliente)
  values ('2023-01-01', '55588833320');

insert into compra_produto (codigo_compra, codigo_produto, quantidade, preco)
  values (3, 1, 33, 8.90);

select * from produto;
~~~

- com a ação do TRIGGER, o saldo do produto Arroz pct 5 kg que era de 100 passou a ser de 67, após o lançamento da compra de 33 unidades.

## Restrições em relação a TRIGGERS:

- a implementação deste recurso atualmente no MySQL tem várias limitações, entre principais temos:
  - não se pode chamar diretamente um TRIGGER com CALL, como se faz com um Stored Procedures.
  - não é permitido iniciar ou finalizar transações em meio à TRIGGERs.
  - não se pode criar um TRIGGER para uma tabela temporária – TEMPORARY TABLE.
  - TRIGGERs ainda não podem ser implementadas com a intenção de devolver para o usuário ou para uma aplicação mensagens de erros.

---

## Você no comando

> Utilizar o banco de dados do consultório para desenvolver os exemplos.

<em>
"Carlos, analista responsável pelo projeto de integração dos Sistemas no Consultório da Dra. Ana Lúcia já sabe como incluir o registro na worklist dos aparelhos e o que fazer quando um exame é realizado, para isso ele criou os PROCEDURES incluir_worklist e confirmar_realizacao_exame respectivamente. O desafio agora é tentar responder duas questões fundamentais para seguir com o projeto:<br>
1. Quando devo incluir o registro na worklist do aparelho?<br>
2. Quando devo confirmar a realização do exame?"<br>
</em>
<br>

> O principal objetivo da fase de análise de um projeto é a coleta de requisitos. Esses requisitos devem ficar sempre à disposição da equipe desenvolvedora para que todas as soluções sejam definidas com base nas necessidades e regras de negócio do cliente, sem desvios de foco ou alteração de escopo. No caso do Consultório da Dra. Ana Lúcia, temos duas informações que nos ajudarão a auxiliar o Analista Carlos nesse novo desafio. São elas:

### A) “Somente serão integrados os agendamentos recepcionados para realização de procedimentos de imagem.”

- isso quer dizer que o registro deverá ser incluído na worklist do aparelho quando o agendamento for recepcionado. 
- mas o que caracteriza um registro de agendamento recepcionado?
  - ao analisar a estrutura e os registros da Tabela agendamento, podemos verificar que o campo "chegou" define o que foi chamado de agendamento recepcionado, quando preenchido com a letra “S”.
- por padrão, um agendamento é criado como não recepcionado, ou seja, campo chegou igual a letra “N”, significando que para que ele seja considerado recepcionado, é necessário aplicar uma alteração no registro (UPDATE), passando seu conteúdo para “S”. 

> Portanto, quando devo incluir o registro na worklist dos aparelhos?
- “Devo incluir o registro na worklist dos aparelhos após a alteração do conteúdo do campo chegou do registro de agendamento para a letra “S”.

### B) “Implementar uma estrutura no banco de dados do consultório que será utilizada pelo aparelho para confirmação da integração dos dados e que posterior será utilizada para que o aparelho retorne à realização do exame.”

- Isso quer dizer que o processo de confirmação de realização do exame deverá ser executado quando o aparelho retornar à execução do exame por meio da Tabela integracao_aparelhos. 
- mas o que caracteriza um registro integrado que tenha sido retornado sua realização do aparelho?
  - ao analisar a estrutura e os registros da Tabela integracao_aparelhos, podemos verificar a existência de 3 (três) colunas:
    - integracao_id: identificador da integração.
    - worklist_id: identificador da worklist do agendamento que foi integrado.
    - dt_realizacao: data de realização do exame.
- portanto, a realização de um exame é definida quando o campo dt_realizacao for preenchido (UPDATE), ou seja, enquanto ele não for preenchido significa apenas que a
integração do exame foi confirmada e que está aguardando sua realização, situação essa definida na inclusão (INSERT) do registro.

> Logo, quando devo confirmar a realização do exame? 
- "Devo confirmar a realização do exame após o preenchimento do conteúdo do campo dt_realizacao após a alteração do registro."

### Nos dois casos, os conteúdos dos campos são definidos após uma operação de alteração realizada nos registros, sendo assim, Carlos conseguirá cumprir mais essa etapa do projeto, sem a necessidade de solicitar qualquer tipo de alteração em nenhum dos sistemas envolvidos, apenas com a implementação no banco de dados de dois TRIGGERS (gatilhos) de AFTER UPDATE (após uma alteração no registro) nas Tabelas de agendamento e integracao_aparelhos, utilizando a seguinte codificação:

1. Na tabela agendamento:

~~~sql
-- AFTER UPDATE

-- verifica se o procedimento do agendamento é de imagem
if (fnc_tipo_proc(new.pro_id) = 'I') then
-- verifica se a alteração modificou o conteúdo do campo chegou
-- verificando se o conteúdo anterior era ‘N’ e novo é ‘S’
if (old.chegou = 'N') and (new.chegou = 'S') then
  -- chama a procedure passando como parâmetro
  -- o identificador do agendamento que será
  -- incluído na worklist do aparelho
  call incluir_worklist(new.agendamento_id);
end if;
end if; 
~~~

2. Na Tabela integracao_aparelhos:

~~~sql
-- AFTER UPDATE

-- verifica se a alteração modificou o conteúdo do campo dt_realizacao
-- verificando se o conteúdo anterior era nulo e novo não é
if (old.dt_realizacao is null) and (new.dt_realizacao is not null)
then
-- chama a procedure passando como parâmetro
-- o identificador da integração do agendamento
-- que terá sua realização confirmada
call confirmar_realizacao_exame(new.worklist_id);
end if; 
~~~

### Para verificar se o processo está sendo executado corretamente, escolher um registro de agendamento de exame que ainda não tenha sido recepcionado:

1. recepcionar o agendamento de exame (passo que será realizado no Sistema do Consultório):

~~~sql
update agendamento a
set a.chegou = 'S'
where a.agendamento_id = 4;
~~~

2. integrar o agendamento ao aparelho (passo que será realizado no Sistema dos Aparelhos):

~~~sql
insert into integracao_aparelhos (worklist_id)
values (1);
~~~

~~~sql
update worklist_aparelhos w
set w.integrado = 'S'
where w.agendamento_id = 4;
~~~

3. retornar a realização do exame (passo que será realizado no Sistema dos Aparelhos):

~~~sql
update integracao_aparelhos i
set i.dt_realizacao = '2019-01-15'
where i.integracao_id = 1;
~~~

4. conferir com select * worklist_aparelhos, integracao_aparelhos e agendamento.

---

## Fichário

<em>
"1. Desenvolva um gatilho (trigger) que insira um registro de garagem coberta para todo apartamento incluído do tipo cobertura.<br>
2. Desenvolva um gatilho (trigger) que desvalorize o preço do apartamento em 30% quando uma garagem vinculada a ele for excluída."
</em>
<br>

> Resolução [aqui](./monicaQuintal_agenda03_ti_iii.pdf).

---

[Voltar ao início!](https://github.com/monicaquintal)