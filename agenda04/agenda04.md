<div align="center">
<a href="https://github.com/monicaquintal" target="_blank">
<img align="right" height="100" src="https://observatoriodabicicleta.org.br/uploads/2020/09/bancos-de-dados-nova-600.png" />
</a>
<h1>Estudando Banco de Dados</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda04">
<h2>Agenda 04: Visões Controladas e Permissões.</h2>
</div>

- para disponibilizar informações contidas em um banco de dados, são necessárias implementações de regras e controles de acesso.
-  ou seja, restringir parte ou toda informação de determinadas estruturas do banco de dados.
- aplicações bem projetadas geralmente expõem uma interface pública, enquanto mantêm privados os detalhes de implementação, permitindo, assim, mudanças futuras de projeto sem impacto nos usuários finais.

## 1. O que são views?

- view consiste em um mecanismo de consulta de dados. 
- diferentemente das tabelas, as views, não envolvem armazenamento de dados.
- ***cria-se uma view atribuindo um nome a uma instrução select e, em seguida, armazenando a consulta para que outros a usem.*** 
- outros usuários podem, então, usar sua view, para acessar dados como se estivessem consultando tabelas diretamente (na verdade, podem nem saber que estão usando views).

> para os exemplos a seguir, utilizado o banco de dados minimercado.

### a) ocultar o número do CPF, entre as informações dos clientes do minimercado, tabela cliente.

- definir uma view chamada "cliente_vw", e determinar que todos a usem para acessar os dados de cliente. 
- definição da view:

~~~sql
create or replace view cliente_vw (nome_cliente, endereco_cliente) as
/* nome da view e apelidos p/ os campos que serão apresentados quando ocorrer a execução. */
  select 
    nome, endereco 
  from 
    cliente;
  /* consulta com campos e regras para seleção dos dados. */
~~~

- a definição de apelidos para as colunas não é obrigatória: é possível criar uma view sem defini-los. 
- neste caso, o código para criação seria:

~~~sql
create or replace view cliente_vw as
  select 
    nome, endereco
  from 
    cliente;
~~~

> é possível criar a view pela janela SQL (conforme exemplos acima), ou utilizando a interface gráfica; vídeo de demonstração [aqui](https://www.youtube.com/watch?v=NDzndxOW2JM).

- quando a instrução create view é executada, o servidor de banco de dados armazena a definição da view para uso futuro. 
- uma vez que a view tenha sido criada, os usuários podem consultá-la como fariam com uma tabela, como em:

~~~sql
select *
  from cliente_vw;
~~~

- do ponto de vista do usuário, a view se parece exatamente com uma tabela. 
- se quiser saber quais colunas estão disponíveis em uma view, usar o comando `describe` para examiná-la.

~~~sql
describe cliente_vw;
~~~

> é possível usar qualquer cláusula da instrução select quando estiver consultando por meio de uma view, incluindo group by, having e order by.

- há várias ***razões para se utilizar view***, como:
  - segurança de dados: restrição de colunas e linhas presentes em uma tabela.
  - agregação de dados: aplicações em relatórios, que geralmente requerem dados agregados.
  - escondendo a complexidade: restringir aos usuários finais a visualização de regras e instruções complexas para obtenção de dados apresentados no resultado de uma consulta.

## 2. Views atualizáveis

- alguns SGBD (***incluindo MySQL***) permitem modificar dados por meio de uma view, desde que obedeça às regras:
  - não são usadas funções de agregação (max(), min(), avg() etc).
  - aview emprega cláusulas group by ou having.
  - não existem subconsultas na cláusula select ou from, e nenhuma subconsulta na cláusula where não se refere a tabelas na cláusula from.
  - aview não utiliza union, union all ou distinct.
  - a cláusula from inclui pelo menos uma tabela ou view atualizável.
  - a cláusula from usa junções internas se houver mais de uma tabela ou view.

### Exemplo:

- para demonstrar a atualização de views, atualizar a view cliente_vw. 
- alterar o nome do primeiro cliente de “manuel barbosa” para “manoel barbosa”.
- codificação:

~~~sql
update cliente_vw
  set nome_cliente = 'manoel barbosa'
  where nome_cliente = 'manuel barbosa';
~~~

## 3. Alterar a View

- sintaxe:

~~~sql
alter view nome_da_view as
  select * from nome_outra_tabela;
~~~

- exemplo:

~~~sql
alter view cliente_vw as
  select nome, endereco
    from cliente
    order by nome;
~~~

## 4. Excluindo a View

- sintaxe:

~~~sql
drop view nome_da_view;
~~~

- exemplo:

~~~sql
drop view cliente_vw;
~~~

## 5. Concluindo:

- com uma view, além de definirmos o que será disponibilizado para o usuário final, dependendo das regras utilizadas para sua criação, ela poderá ser atualizável.

<div align="center">
<h2>Permissões</h2>
</div>

- depois de definirmos os dados que serão disponibilizados, o próximo passo é dar acesso somente aos usuários que preenchem as regras estabelecidas pelo negócio para visualização desses dados.
- a Ferramenta WorkBench oferece o recurso para a criação de usuários pela interface gráfica, por meio do Menu Server, opção Users e Privileges, conforme apresentado [aqui](https://www.youtube.com/watch?v=Pdulm9A9JRc).
- nessa interface, além de criar o usuário, é possível gerenciar os privilégios dele, divididos em 3 (três) categorias:

### a) Account Limits:

- nessa guia são definidos alguns limites para conta que você está criando.
- exemplo: a quantidade máxima de queries (consultas) que o usuário poderá executar em uma hora, entre outras.
- max. queries, max. updates, max. corrections, concurrent connections.

### b)  Administrative Roles:

- nessa guia é possível atribuir alguns privilégios administrativos para o usuário.
- exemplo: DBA (Database Administrator, Administrador do Banco de Dados),
onde ele terá todos os privilégios para executar todas as ações possíveis em um banco de dados.

### c) Schema Privileges:

- nessa guia é possível atribuir ao usuário um ou vários privilégios a
determinados Schemas disponíveis no SGBD.
- significado de alguns privilégios:

<div align="center">

Privilégio | Descrição
------------|-------------
ALL [PRIVILEGES] | Todos os privilégios exceto GRANT OPTION
ALTER | Permite executar ALTER TABLE
CREATE | Permite executar CREATE TABLE
CREATE TEMPORARY TABLES | Permite executar CREATE TEMPORARY TABLE
DELETE | Permite executar DELETE
DROP | Permite executar DROP TABLE
EXECUTE | Permite executar stored procedures (MySQL 5.0)
FILE | Permite executar SELECT ... INTO OUTFILE e LOAD DATA INFILE
INDEX | Permite executar CREATE INDEX e DROP INDEX
INSERT | Permite executar INSERT
LOCK TABLES | Permite executar LOCK TABLES em tabelas que você tenha o privilégio SELECT
PROCESS | Permite executar SHOW FULL PROCESSLIST
REFERENCES | Ainda não está implementado
RELOAD | Permite executar FLUSH
REPLICATION CLIENT | Permite ao usuário obter a localização do Master ou Slave
REPLICATION SLAVE | Necessário para a replicação Slave (leitura dos eventos do log binário do Master)
SELECT | Permite executar SELECT
SHOW DATABASES | exibe todos os bancos de dados
SHUTDOWN | Permite executar mysqladmin shutdown
SUPER | Permite executar CHANGE MASTER, KILL , PURGE MASTER LOGS e SET GLOBAL<br>Permite conectar-se ao servidor uma vez, mesmo que o max_connections tenha sido atingido
UPDATE | Permite executar UPDATE
USAGE | Sinônimo para "no privileges''
GRANT OPTION | Permite ao usuário repassar os seus privilégios

</div>

## Sintaxe para:

### a) Criar um usuário:

~~~sql
create user 'novousuario'@'localhost' identified by 'password';
~~~

### b) Excluir um usuário:

~~~sql
drop user 'novousuario'@'localhost';
~~~

## Exemplificando:

> demonstração do uso de privilégios [aqui](https://www.youtube.com/watch?v=1UBu2xTCzrg).

- criar um usuário com o nome de 'teste', definindo como senha os números '12345':

~~~sql
create user teste@localhost identified by '12345';
~~~

- clicar em Home > MySQL Connections > + > informar Connection Name (Usuario teste), Username (teste) e senha (12345).
  - após a criação do usuário teste, ele ainda não terá permissão para fazer ações no SGBD.
  - ao criar uma conexão na Ferramenta Workbench, no quadro Schemas nenhum banco de dados estará disponível, além de não poder criar nenhum.

- para que um usuário possa executar alguma ação no SGBD, ele precisa ter permissão ou privilégios.

### Sintaxe para dar privilégios:

~~~sql
grant [tipo_de_permissão]
  on [nome_base_dados].[nome_tabela]
  to ‘[nome_usuário]’@'localhost’;
~~~

### Sintaxe para revogar privilégios:

~~~sql
revoke [tipo_de_permissão]
  on [nome_base_dados].[nome_tabela]
  to ‘[nome_usuário]’@'localhost’;
~~~

### Continuando o exemplo:

- atribuir os privilégios de select e update na view cliente_vw:

~~~sql
grant select, update on minimercado.cliente_vw to teste@localhost;
~~~

> IMPORTANTE: Após aplicar algum tipo de privilégio execute o `comando flush privileges`0 para que o MySQL possa atualizar os privilégios que estão em memória.

~~~sql
flush privileges;
~~~

- após conceder os privilégios o usuário teste passou a ter acesso ao banco de dados minimercado e a view cliente_vw.

---

## Você no Comando

> utilizar o banco de dados do consultório para desenvolver os exemplos.

<em>
"Para finalizar o projeto de integração dos Sistemas no Consultório da Dra. Ana Lúcia, Carlos, analista responsável, precisa disponibilizar o acesso dos aparelhos às estruturas worklist_aparelhos e integracao_aparelhos, nelas estão as informações necessárias para que o processo de integração seja executado por completo, trafegando as informações entre os Sistemas.<br>
Como Carlos fará isso?"
</em>

- ao analisarmos as estruturas envolvidas podemos chegar as seguintes conclusões:

<div align="center">

Nome da tabela: WORKLIST_APARELHOS

CAMPO | TIPO (Tamanho) | Obrigatório | Padrão | PK | Observação
------|---------------|-------------|---------|------|---------
worklist_id | int(6) | sim | &#32; | sim | auto incremento
agendamento_id | int(6) | sim | &#32; | não | &#32;
dt_exame | date | sim | &#32; | não | &#32;
paciente | varchar(80) | sim | &#32; | não | &#32;
dt_nascimento | date | sim | &#32; | não | &#32;
convenio | varchar(80) | sim | &#32; | não | &#32;
procedimento | varchar(100) | sim | &#32; | não | &#32;
aparelho | varchar(2) | sim | &#32; | não | RX ou US
integrado | varchar(1) | sim | N | não | &#32;

</div>

- worklist_aparelhos contém os registros dos agendamentos de exames de imagem recepcionados que deverão ser integrados aos aparelhos.
- neste caso, o Sistema dos aparelhos deverá ter privilégios de select e update
  - select: para obter os dados do agendamento e carregá-los.
  - update: para poder alterar o conteúdo do campo integrado de 'N' para 'S', não considerando o registro nas próximas execuções da integração.

<div align="center">

Nome da Tabela: INTEGRACAO_APARELHOS

CAMPO | TIPO (Tamanho) | Obrigatório | Padrão | PK | Observação
------|------------------|---------|-----------|-----|-----------
integracao_id | int(6) | sim | &#32; | sim | auto incremento
worklist_id | int(6) | sim | &#32; | não | &#32;
dt_realizacao | date | não | &#32; | não | &#32;

</div>

- integracao_aparelhos: utilizada para armazenar os registros dos exames que já foram integrados, e posteriormente, sua realização.
- o Sistema dos aparelhos deverá ter privilégios de insert e update:
  - insert: para incluir um registro, confirmando assim que as informações foram carregadas aos aparelhos.
  - update: para confirmar a realização do exame, preenchendo o conteúdo do campo dt_realizacao.

### Criando um usuário (chamado "teste"):

~~~sql
create user teste@localhost identified by '12345';
~~~

### Privilégios as estruturas worklist_aparelhos e integracao_aparelhos:

~~~sql
grant select, update on consultorio.worklist_aparelhos to teste@localhost;
grant insert, update on consultorio.integracao_aparelhos to teste@localhost;
~~~

### Utilizando a view:

- criar uma view sem os campos agendamendo_id e convenio da Tabela worklist_aparelhos, e dar os mesmos privilégios de select
e update ao usuário aparelho.

~~~sql
create or replace view worklist_ap as
  select worklist_id, dt_exame, paciente, dt_nascimento,
    procedimento, aparelho, integrado
  from worklist_aparelhos;

grant select, update on consultorio.worklist_ap to aparelho@localhost;
~~~

---

## Fichário

<em>
"Utilizar o banco de dados imobiliária para resolver os exercícios.

1. Desenvolva uma view que apresente o nome e o telefone de contato dos síndicos de cada condomínio.
2. Desenvolva uma view que apresente o total de apartamentos por condomínio.
3. Crie um usuário e conceda a ele o privilégio de select nas views nos exercícios anteriores."
</em>

---

[Voltar ao início!](https://github.com/monicaquintal)