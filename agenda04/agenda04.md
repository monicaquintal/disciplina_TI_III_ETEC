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







---

[Voltar ao início!](https://github.com/monicaquintal)