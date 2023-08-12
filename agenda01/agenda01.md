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

### Contexto do exemplo:
- O funcionário faz uma solicitação de manutenção de um ou vários equipamentos;
- A solicitação permanece com status “SOLICITADA” até ser liberada;
- O responsável pelo setor de engenharia libera a solicitação, agendando a manutenção.

Neste caso, uma saída seria a criação de um processo de liberação de solicitação, pois nenhum agendamento de manutenção de equipamento é realizado enquanto a solicitação não for liberada.
<br>
Passos:

- Atualização do status da solicitação;
- Atualização do status dos equipamentos da solicitação;
- Agendar manutenção dos equipamentos.

> Há pelo menos três instruções de atualização e/ou inserção. Poderíamos agrupar essas três instruções no corpo de um procedimento e chamá-lo a partir da aplicação uma única vez. As ações de update/insert/delete, a partir daí, ficariam por conta do servidor.

Pontos positivos | Pontos negativos
-----------------|------------------
- Simplificação da execução de instruções SQL pela aplicação.<br>- Transferência de parte da responsabilidade de processamento para o servidor.<br>- Facilidade na manutenção, reduzindo a quantidade de alterações na aplicação. | - Necessidade de maior conhecimento da sintaxe do banco de dados para escrita de rotinas em SQL.<br>- As rotinas ficam mais facilmente acessíveis. Alguém que tenha acesso ao banco poderá visualizar e alterar o código.

## Criando e invocando Stored Procedures no MySQL:

### Sintaxe para criação de Stored Procedures no MySQL:

~~~sql
delimiter $$
create procedure nome_procedimento ([parâmetros])
begin
 /*corpo do procedimento*/
end $$
delimiter ;
~~~

Observações:
- nome_procedimento: nome que identificará o procedimento armazenado;segue as mesmas regras para definição de variáveis, não podendo iniciar com número ou caracteres especiais (exceto o underline “_”).
- parâmetros: são opcionais e, caso não sejam necessários, devem permanecer apenas os parênteses vazios na declaração do procedure. Para que um procedimento receba parâmetros, é necessário utilizar a seguinte sintaxe (dentro dos parênteses):

### Sintaxe de declaração de parâmetros em Stored Procedures:

~~~sql
(modo nome tipo, modo nome tipo, modo nome tipo)
~~~

- nome: nome do parâmetro, segue as mesmas regras de definição de variáveis.
- tipo: tipo de dado do parâmetro (int, varchar, decimal, etc).
- modo: indica a forma como o parâmetro será tratado no procedimento, se será apenas um dado de entrada, de saída ou ambas as funções. Os valores possíveis para o modo são:
  - in: indica que o parâmetro é apenas para entrada/recebimento de dados, não podendo ser usado para retorno.
  - out: para parâmetros de saída. Para esse tipo não pode ser informado um valor direto (como ‘teste’, 1 ou 2.3), deve ser passada uma variável “por referência”.
  - inout: usado para os dois fins (entrada e saída de dados). Nesse caso também deve ser informada uma variável e não um valor direto.

### Uso do comando `delimiter`:

- por padrão o MySQL utiliza o sinal de ponto e vírgula como delimitador de comandos, separando as instruções a serem executadas. 
- porém, dentro do corpo do Stored Procedure será necessário separar algumas instruções internamente utilizando esse mesmo sinal, por isso é preciso inicialmente ***alterar o delimitador padrão do MySQL*** (para `$$`) e ao fim da criação do procedimento, restaurar seu valor padrão.

### Sintaxe para chamar um Stored Procedure:

~~~sql
call nome_procedimento([parâmetros]);
~~~

## Aplicando exemplos

1. Download do script de criação do banco de dados minimercado:

~~~sql
create database minimercado;

use minimercado;

create table cliente (
  cpf_cliente varchar(11) not null,
  nome varchar(80) not null,
  endereco varchar(80) not null,
  primary key (cpf_cliente)
);

insert into cliente values ('11122233370','manuel barbosa','avenida rui barbosa, nÃºmero 435, jardim aeroporto, sÃ£o paulo'),('22233344480','joana nascimento','avenida 7, numero 1765, alvorada, sÃ£o paulo'),('44422211110','leandro goes','alameda 25, nÃºmero 324, fortaleza, sÃ£o paulo'),('55588833320','carlos lacerda','travessa milÃªnio, nÃºmero 134, celina, sÃ£o paulo'),('77766699940','paulo carvalho','praÃ§a centenÃ¡rio, nÃºmero 500, california, sÃ£o paulo');

create table produto (
  codigo_produto int(5) not null auto_increment,
  descricao varchar(40) not null,
  quantidade_estoque double(10,1) not null default '0.0',
  primary key (codigo_produto)
); 

insert into produto values (1,'arroz pct 5 kg',100.0),(2,'feijÃ£o pct 2 kg',50.0),(3,'macarrÃ£o pct 1 kg',80.0),(4,'molho de tomate',40.0),(5,'sal pct 500 gr',100.0);

create table compra (
  codigo_compra int(11) not null auto_increment,
  data date not null,
  cpf_cliente varchar(11) not null,
  primary key (codigo_compra),
  key fk_compra_cpf_cliente (cpf_cliente),
  constraint fk_compra_cpf_cliente foreign key (cpf_cliente) references cliente (cpf_cliente)
);

insert into compra values (1,'2019-10-01','77766699940'),(2,'2019-10-10','44422211110');

create table compra_produto (
  id_compra_produto int(11) not null auto_increment,
  codigo_compra int(11) not null,
  codigo_produto int(5) not null,
  quantidade double(10,1) not null default '1.0',
  preco double(10,2) not null,
  primary key (id_compra_produto),
  key fk_compprod_codigo_compra (codigo_compra),
  key fk_compprod_codigo_produto (codigo_produto),
  constraint fk_compprod_codigo_compra foreign key (codigo_compra) references compra (codigo_compra),
  constraint fk_compprod_codigo_produto foreign key (codigo_produto) references produto (codigo_produto)
); 

insert into compra_produto values (1,1,1,2.0,8.90),(2,1,2,2.0,5.40),(3,2,3,1.0,2.45),(4,2,4,2.0,3.30),(5,2,5,1.0,4.70);
~~~

2. Executá-lo em uma janela do SQL Workbench.

