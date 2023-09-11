<div align="center">
<a href="https://github.com/monicaquintal" target="_blank">
<img align="right" height="100" src="https://observatoriodabicicleta.org.br/uploads/2020/09/bancos-de-dados-nova-600.png" />
</a>
<h1>Estudando Banco de Dados</h1>
<p>Disciplina: Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda01">
<h2>Agenda 01: Blocos de Linguagem de Consulta Estruturada.</h2>
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

## Aplicando exemplos:

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

insert into cliente values ('11122233370','manuel barbosa','avenida rui barbosa, número 435, jardim aeroporto, são paulo'),('22233344480','joana nascimento','avenida 7, numero 1765, alvorada, são paulo'),('44422211110','leandro goes','alameda 25, número 324, fortaleza, são paulo'),('55588833320','carlos lacerda','travessa milânio, número 134, celina, são paulo'),('77766699940','paulo carvalho','praça centenário, número 500, california, são paulo');

create table produto (
  codigo_produto int(5) not null auto_increment,
  descricao varchar(40) not null,
  quantidade_estoque double(10,1) not null default '0.0',
  primary key (codigo_produto)
); 

insert into produto values (1,'arroz pct 5 kg',100.0),(2,'feijão pct 2 kg',50.0),(3,'macarrão pct 1 kg',80.0),(4,'molho de tomate',40.0),(5,'sal pct 500 gr',100.0);

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

> Vídeo tutorial [aqui](https://www.youtube.com/watch?v=5ogiIxVZ1o0).

### Exemplo 1 - Usando parâmetro de entrada:

~~~sql
delimiter $$
create procedure selecionar_produtos(in quantidade int)
begin
 select * from produto
 limit quantidade;
end $$
delimiter ;
~~~

> Vídeo tutorial [aqui](youtube.com/watch?v=sPPfCG5r7ZQ).

- função do procedimento: fazer um select na tabela PRODUTO, limitando a quantidade de
registros pela quantidade recebida como parâmetro. 
- caso desejássemos selecionar dois registros dessa tabela, poderíamos usar o procedure como mostra o código a seguir, chamando procedure com parâmetro de entrada:

~~~sql
call selecionar_produtos(2);
~~~

- **ou** podemos criar um procedure utilizando a interface gráfica do Workbench: 
  - clicando com botão direito em "Stored Procedures" e acessando a opção "Create Store Procedure".
  - será apresentada a interface para criação de procedures, onde você podemos definir `nome` (alterando "new_procedure" para "selecionar_produtos", e o name do procedure será alterar automaticamente após sua geração), `parâmetros` (dentro dos parênteses) e `instruções` que deverão ser executadas (entre BEGIN e AND).
  - clicar no botão Apply e confirmar.

> Para excluir ou alterar um procedure, utilizar as opções `Alter Stored Procedure` ou `Drop Stored Procedure`, do quadro SCHEMA.

- exemplo do procedimento completo [aqui](https://www.youtube.com/watch?v=t2Y3hiXk8-0)!

### Exemplo 2 - Usando parâmetro de saída:

~~~sql
delimiter $$
create procedure verificar_quantidade_produtos(out quantidade int)
begin
 select count(*) into quantidade from produto;
end $$
delimiter ;
~~~

- a função desse procedimento é retornar a quantidade de registros da tabela PRODUTO, passando esse valor para a variável de saída “quantidade”. Para isso foi utilizada a `palavra reservada into`.
- para chamá-lo, usamos um símbolo de arroba (@) seguido do nome da variável que receberá o valor de saída. Feito isso, a variável poderá ser usada posteriormente, como
demonstrado a seguir:

~~~sql
call verificar_quantidade_produtos(@total);
select @total;
~~~

- ao executar a segunda linha, teremos como retorno o valor da variável @total, que será preenchida no procedure.

### Exemplo 3 - Usando parâmetro de entrada e saída

~~~sql
delimiter $$
create procedure elevar_ao_quadrado(inout numero int)
begin
 set numero = numero * numero;
end $$
delimiter ;
~~~

- criado o Stored Procedure chamado elevar_ao_quadrado, que recebe uma variável e a altera, definindo-a como o seu próprio valor elevado à segunda potência.
- nesse caso, a mesma variável é usada como entrada e saída, como demonstrado a seguir, chamando procedure com parâmetro de entrada e saída:

~~~sql
set @valor = 5;
call elevar_ao_quadrado(@valor);
select @valor;
~~~

### Exemplo 4 - Usando variáveis no corpo do procedimento:

- é possível declarar variáveis no corpo dos Stored Procedures.
- sintaxe:

~~~sql
declare nome_variável tipo default valor_padrao;
~~~

- onde:
  - declare: obrigatória, responsável por indicar que uma variável será declarada com o nome “nome_variavel” (mesmas regras de nomeação de variáveis).
  - tipo: tipo de dados da variável (int, decimal, varchar, etc). A palavra reservada `default`` é opcional e deve ser usada quando se deseja definir um valor inicial (valor_padrao) para a variável.

- a declaração das variáveis deve ser feita logo no início do corpo do procedure, para aquelas que serão utilizadas em todo o procedimento, ou dentro de um bloco begin-end específico que limite seu escopo.
- para definir um valor para uma variável, usamos as palavras reservadas `set` (para passagem direta de valor, como no Exemplo 2) ou into (no caso de associação de valores dentro de consultas, como no Exemplo 3).
- outro ponto importante de se citar é o `ESCOPO` das variáveis, que define em que pontos elas são reconhecidas. Uma variável definida dentro de um bloco begin/end é válida somente dentro dele, ou seja, após o end ela já não é mais reconhecida. Assim, é possível definir várias variáveis com o mesmo nome, mas dentro de blocos begin/end distintos.
- variáveis cujo nome inicia com arroba (@), são chamadas `variáveis de sessão`, e são válidas enquanto durar a sessão (demonstrado em Chamando procedure com parâmetro de entrada e saída).

---

## Praticando...

> Para dar início ao processo de integração do Sistema que gerencia o consultório de Ana Lúcia com os aparelhos adquiridos, foi enviado a ela um manual de integração, onde constava todos os passos para envio e recebimento de informações dos aparelhos.

Com o arquivo do Banco de Dados do consultório abaixo, executar em uma janela SQL do Workbench.

~~~sql
/* CRIACAO DO BANCO DE DADOS */
create database consultorio;

use consultorio;

/* CRIACAO DAS ESTRUTURAS DO BANCO DE DADOS */
create table tipo_pessoa (
  tipo_pessoa_id int(3) not null auto_increment,
  descricao varchar(20) not null,
  primary key (tipo_pessoa_id)
);

create table pessoa (
  pessoa_id int(5) not null auto_increment,
  nome varchar(80) not null,
  dt_nascimento date not null,
  logradouro varchar(50) not null,
  numero varchar(10) default null,
  bairro varchar(30) not null,
  cidade varchar(40) not null,
  uf varchar(2) not null,
  cep varchar(9) not null,
  cns varchar(20) not null,
  cpf varchar(11),
  primary key (pessoa_id)
); 

create table pessoa_telefone (
  pessoa_fone_id int(10) not null auto_increment,
  pessoa_id int(5) not null,
  numero varchar(15) not null,
  primary key (pessoa_fone_id),
  unique key uk_pt_pesid_tel (pessoa_id, numero),
  constraint fk_pt_pesid foreign key (pessoa_id) references pessoa (pessoa_id)
);

create table pessoa_tipo (
   pessoa_tipo_id int(5) not null auto_increment,
   pessoa_id int(5) not null,
   tipo_pessoa_id int(3) not null,
   primary key(pessoa_tipo_id),
   unique key uk_ptp_pesid_ctppes (pessoa_id, tipo_pessoa_id),
   constraint fk_ptp_pes_id foreign key (pessoa_id) references pessoa (pessoa_id),
   constraint fk_ptp_tppesid foreign key (tipo_pessoa_id) references tipo_pessoa (tipo_pessoa_id)
);

create table convenio (
   convenio_id int(3) not null auto_increment,
   razao_social varchar(80) not null,
   cnpj varchar(14) not null,
   primary key(convenio_id)
);

create table procedimento (
   pro_id int(5) not null auto_increment,
   descricao varchar(50) not null,
   tipo varchar(1) not null,
   aparelho varchar(2),
   primary key(pro_id)
);

create table convenio_procedimento_valor (
	conv_proc_val_id int(5) not null auto_increment,
    convenio_id int(3) not null,
    pro_id int(5) not null,
    valor double(10,2) default 0,
    primary key (conv_proc_val_id),
    unique key uk_cpv_convid_proid (convenio_id, pro_id),
    constraint fk_cpv_conv_id foreign key (convenio_id) references convenio (convenio_id),
    constraint fk_cpv_pro_id foreign key (pro_id) references procedimento (pro_id)
);

create table agendamento (
	agendamento_id int(6) not null auto_increment,
    dt_agenda date not null,
    horario varchar(5) not null,
    pessoa_id int(5) not null,
    convenio_id int(3) not null,
    med_pessoa_id int(5) not null,
    pro_id int(5) not null,
    valor double(10,2) default 0,
    chegou varchar(1) default 'N',
    realizado varchar(1) default 'N',
    faturado varchar(1) default 'N',
    primary key (agendamento_id),
    unique key uk_ag_dta_hor (dt_agenda, horario),
    constraint fk_ag_pes_id foreign key (pessoa_id) references pessoa (pessoa_id),
    constraint fk_ag_conv_id foreign key (convenio_id) references convenio (convenio_id),
    constraint fk_ag_medpes_id foreign key (med_pessoa_id) references pessoa (pessoa_id),
    constraint fk_ag_pro_id foreign key (pro_id) references procedimento (pro_id)
);

create table worklist_aparelhos (
	worklist_id int(6) not null auto_increment,
    agendamento_id int(6) not null,
    dt_exame date not null,
    paciente varchar(80) not null,
    dt_nascimento date,
    convenio varchar(80) not null,
    procedimento varchar(100) not null,
    aparelho varchar(2) not null,
    integrado varchar(1) default 'N',
    primary key (worklist_id)
);

create table integracao_aparelhos (
	integracao_id int(6) not null auto_increment,
    worklist_id int(6) not null,
    dt_realizacao date,
    primary key (integracao_id)
);

/* INSERINDO REGISTROS NAS ESTRUTURAS */
insert into tipo_pessoa (descricao) values ('COLABORADOR');
insert into tipo_pessoa (descricao) values ('MEDICO');
insert into tipo_pessoa (descricao) values ('PACIENTE');

insert into pessoa 
	(nome, dt_nascimento, logradouro, numero, bairro, cidade, uf, cep, cns, cpf)
values 
	('Ana Maria', '1976-06-14', 'Alameda Dom Predro I', '432', 'IndependÃªncia', 'SÃ£o Paulo', 'SP', '04470-010', '230099165770018','18233799157');
    
insert into pessoa 
	(nome, dt_nascimento, logradouro, numero, bairro, cidade, uf, cep, cns, cpf)
values 
	('Marilda Dutra', '1979-01-23', 'Rua Adolfo Belini', '621', 'SÃ£o Francisco', 'SÃ£o Paulo', 'SP', '01005-020', '778693370540008','24698752183');    
    
insert into pessoa 
	(nome, dt_nascimento, logradouro, numero, bairro, cidade, uf, cep, cns, cpf)
values 
	('AcÃ¡cio Moura', '1985-04-29', 'Avenida General Costa e Silva', '908', 'Vila Militar', 'SÃ£o Paulo', 'SP', '06442-007', '234736304680008','71558660402');  

insert into pessoa 
	(nome, dt_nascimento, logradouro, numero, bairro, cidade, uf, cep, cns, cpf)
values 
	('Gustavo Camilo', '1983-08-25', 'Avenida Siqueira Campos', '2784', 'Centro', 'Barueri', 'SP', '06411-210', '270832524070006','82251731717');

insert into pessoa 
	(nome, dt_nascimento, logradouro, numero, bairro, cidade, uf, cep, cns, cpf)
values 
	('JosÃ© de Souza', '1991-03-17', 'Avenida Joao Paulo II', '3425', 'Oliveira', 'SÃ£o Pedro', 'SP', '06172-200', '169963985310004','94652218800');
    
insert into pessoa_telefone (pessoa_id, numero) values (1, '(11) 3235-4567');
insert into pessoa_telefone (pessoa_id, numero) values (2, '(11) 3212-3456');
insert into pessoa_telefone (pessoa_id, numero) values (3, '(11) 3879-2123');
insert into pessoa_telefone (pessoa_id, numero) values (4, '(11) 3902-9856');
insert into pessoa_telefone (pessoa_id, numero) values (5, '(11) 3574-9271');
insert into pessoa_telefone (pessoa_id, numero) values (1, '(11) 3213-5890');
 
insert into pessoa_tipo (pessoa_id, tipo_pessoa_id) values (1, 2);
insert into pessoa_tipo (pessoa_id, tipo_pessoa_id) values (2, 1);
insert into pessoa_tipo (pessoa_id, tipo_pessoa_id) values (3, 2);
insert into pessoa_tipo (pessoa_id, tipo_pessoa_id) values (4, 3);
insert into pessoa_tipo (pessoa_id, tipo_pessoa_id) values (5, 3);

insert into convenio (razao_social, cnpj) values ('UNIMED','88638266000105');
insert into convenio (razao_social, cnpj) values ('AMIL','33202172000105');
insert into convenio (razao_social, cnpj) values ('SULAMERICA','87015579000144');

insert into procedimento (descricao, tipo, aparelho) values ('RAIO X DE TORAX', 'I', 'RX');
insert into procedimento (descricao, tipo, aparelho) values ('ULTRASSONOGRAFIA DE ABDOMEN TOTAL', 'I', 'US');
insert into procedimento (descricao, tipo) values ('CONSULTA MÃ‰DICA', 'C');

insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (1, 1, 50);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (2, 1, 52.5);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (3, 1, 51.45);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (1, 2, 65);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (2, 2, 62.6);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (3, 2, 61.30);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (1, 3, 90);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (2, 3, 91.2);
insert into convenio_procedimento_valor (convenio_id, pro_id, valor) values (3, 3, 90.25);

insert into agendamento (dt_agenda, horario, pessoa_id, convenio_id, med_pessoa_id, pro_id)	values ('2019-01-15', '08:00', 4, 1, 1, 3);
insert into agendamento (dt_agenda, horario, pessoa_id, convenio_id, med_pessoa_id, pro_id)	values ('2019-01-15', '08:30', 5, 2, 1, 3);
insert into agendamento (dt_agenda, horario, pessoa_id, convenio_id, med_pessoa_id, pro_id)	values ('2019-01-15', '09:00', 4, 1, 3, 1);
insert into agendamento (dt_agenda, horario, pessoa_id, convenio_id, med_pessoa_id, pro_id)	values ('2019-01-15', '09:30', 5, 2, 3, 2);

create table worklist_aparelhos (
  worklist_id int(6) not null auto_increment,
  agendamento_id int(6) not null,
  dt_exame date not null,
  paciente varchar(80) not null,
  dt_nascimento date default null,
  convenio varchar(80) not null,
  procedimento varchar(100) not null,
  aparelho varchar(2) not null,
  integrado varchar(1) default 'N',
  primary key (worklist_id)
);

delimiter $$
create procedure incluir_worklist (in agend_id int)
begin
    /*1. Passo: busca os dados do agendamento */
    select a.dt_agenda
         , p.nome
         , p.dt_nascimento
         , c.razao_social
         , pr.descricao
         , pr.aparelho
	  into @dt_agenda
         , @nome
         , @dt_nascimento
         , @convenio
         , @descricao
         , @aparelho
     from agendamento a 
          inner join pessoa p on p.pessoa_id = a.pessoa_id
          inner join convenio c on c.convenio_id = a.convenio_id
          inner join procedimento pr on pr.pro_id = a.pro_id
	where a.agendamento_id = agend_id;
    
    insert into worklist_aparelhos (agendamento_id, dt_exame, paciente, dt_nascimento, convenio, procedimento, aparelho)
		values (agend_id, @dt_agenda, @nome, @dt_nascimento, @convenio, @descricao, @aparelho);

end $$	  
delimiter ;

delimiter $$
create procedure confirmar_realizacao_exame (in workl_id int)
begin
    
    select wa.agendamento_id
         , cpv.valor
	  into @agend_id
         , @valor
      from worklist_aparelhos wa
           inner join agendamento a on a.agendamento_id = wa.agendamento_id
           inner join convenio_procedimento_valor cpv on cpv.pro_id = a.pro_id and cpv.convenio_id = a.convenio_id
	 where wa.worklist_id = workl_id;
     
    update agendamento a
       set a.realizado = 'S',
          a.valor = @valor
	 where a.agendamento_id = @agend_id;

end $$	  
delimiter ;

call incluir_worklist(3);

select * from worklist_aparelhos;

call confirmar_realizacao_exame(1);

select * from agendamento;

select * from convenio_procedimento_valor cpv where cpv.pro_id = 1 and cpv.convenio_id = 1;

truncate worklist_aparelhos;

alter table worklist_aparelhos auto_increment = 1;
~~~

- após entender como era o processo de atendimento de pacientes no consultório, Carlos analisou o
manual e identificou as primeiras atividades que terá que realizar para conseguir implementar essa integração:

1. Implementar uma estrutura no banco de dados do consultório para receber os dados do paciente e do exame que ele irá realizar conforme a especificação a seguir:

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

~~~sql
create table worklist_aparelhos (
 worklist_id int(6) not null auto_increment,
 agendamento_id int(6) not null,
 dt_exame date not null,
 paciente varchar(80) not null,
 dt_nascimento date default null,
 convenio varchar(80) not null,
 procedimento varchar(100) not null,
 aparelho varchar(2) not null,
 integrado varchar(1) default 'N',
 primary key (worklist_id)
);

~~~

2. Implementar uma estrutura no banco de dados do consultório que será utilizada pelo aparelho para confirmação da integração dos dados e que posterior será utilizada para que o aparelho retorne a realização do exame conforme a especificação a seguir:

<div align="center">

Nome da Tabela: INTEGRACAO_APARELHOS

CAMPO | TIPO (Tamanho) | Obrigatório | Padrão | PK | Observação
------|------------------|---------|-----------|-----|-----------
integracao_id | int(6) | sim | &#32; | sim | auto incremento
worklist_id | int(6) | sim | &#32; | não | &#32;
dt_realizacao | date | não | &#32; | não | &#32;

</div>

~~~sql
create table integracao_aparelhos (
 integracao_id int(6) not null auto_increment,
 worklist_id int(6) not null,
 dt_realizacao date,
 primary key (integracao_id)
);
~~~

3. Desenvolver um procedure que inclua um registro na Tabela WORKLIST_APARELHOS a partir de um agendamento.

~~~sql
delimiter $$
create procedure incluir_worklist (in agend_id int)
begin
 /*1. Passo: busca os dados do agendamento utilizando variáveis*/
 select a.dt_agenda
 , p.nome
 , p.dt_nascimento
 , c.razao_social
 , pr.descricao
 , pr.aparelho
 into @dt_agenda
 , @nome
 , @dt_nascimento
 , @convenio
 , @descricao
 , @aparelho
 from agendamento a
 inner join pessoa p on p.pessoa_id = a.pessoa_id
 inner join convenio c on c.convenio_id = a.convenio_id
 inner join procedimento pr on pr.pro_id = a.pro_id
where a.agendamento_id = agend_id;

 /*2. Passo: inserir os dados na worklist dos aparelhos */
 insert into worklist_aparelhos (agendamento_id, dt_exame, paciente, dt_nascimento, convenio, procedimento, aparelho)
values (agend_id, @dt_agenda, @nome, @dt_nascimento, @convenio, @descricao, @aparelho);
end $$
delimiter ;
~~~

4. Desenvolver um procedure para confirmar a realização do exame e valorizá-lo de acordo com o convênio no Sistema que gerencia o consultório atribuindo 'S' ao campo realizado, da Tabela AGENDAMENTO, a partir do número de identificação do worklist dos aparelhos, campo worklist_id.

~~~sql
delimiter $$
create procedure confirmar_realizacao_exame (in workl_id int)
begin
/*1. Passo: busca identificador do agendamento e o valor do
procedimento*/
 select wa.agendamento_id
 , cpv.valor
into @agend_id
 , @valor
 from worklist_aparelhos wa
 inner join agendamento a on a.agendamento_id =
wa.agendamento_id
inner join convenio_procedimento_valor cpv
on cpv.pro_id = a.pro_id
and cpv.convenio_id = a.convenio_id
where wa.worklist_id = workl_id;
/*2. Passo: confirma a realização do agendamento e valorização o
procedimento*/
 update agendamento a
 set a.realizado = 'S'
 , a.valor = @valor
where a.agendamento_id = @agend_id;
end $$
delimiter ;
~~~

### Para verificar o funcionamento dos procedures:

~~~sql
call incluir_worklist(3);
/* o valor 3 (três) corresponde ao identificador do agendamento passado como parâmetro para inclusão do registro na worklist dos aparelhos. */
~~~

~~~sql
select * from worklist_aparelhos;
~~~

~~~sql
call confirmar_realizacao_exame(1);
/* o valor 1 (um) corresponde ao identificador do registro de worklist dos aparelhos passado como parâmetro para realização e valorização do exame do agendamento vinculado a ele. */
~~~

~~~sql
select * from agendamento;
/*  neste processo são atualizados os conteúdos dos campos valor e realizado do agendamento vinculado ao registro da worklist dos aparelhos.*/ 
~~~

---

## Atividade

- script:

~~~sql
create database imobiliaria;

use imobiliaria;

create table sindico (
  matricula int(3) not null auto_increment,
  nome varchar(80) default null,
  endereco varchar(80) default null,
  telefone varchar(15) default null,
  primary key (matricula)
);

insert into sindico values (1,'antonio carlos','avenida santos dummont, numero 789, california, sao paulo','(11) 3456-6787'),
(2,'sidnei delgado','alameda xv de novembro, numero 123, jockey club, sao paulo','(11) 3452-4562');

create table condominio (
  codigo int(5) not null auto_increment,
  nome varchar(50) default null,
  endereco varchar(80) default null,
  matricula_sind int(3) default null,
  primary key (codigo),
  key fx_cond_sindico (matricula_sind),
  constraint fx_cond_sindico foreign key (matricula_sind) references sindico (matricula)
);

insert into condominio values (1,'condominio sao paulo','alameda getulio vargas, numero 897, centro, sao paulo',1),
(2,'condominio brasil','avenida general gusmao, numero 453, penha, sao paulo',2);

create table apartamento (
  numero varchar(5) not null,
  tipo varchar(20) default null,
  codigo_cond int(5) default null,
  valor double(10,2) default '0.00',
  primary key (numero),
  key fk_ap_cond (codigo_cond),
  constraint fk_ap_cond foreign key (codigo_cond) references condominio (codigo)
);

insert into apartamento values ('a101','padrao',1,100000.00),
('a201','padrao',1,115000.00),
('a301','padrao',1,125000.00),
('a401','padrao',1,135000.00),
('a501','cobertura',1,150000.00),
('b101','padrao',2,200000.00),
('b201','padrao',2,215000.00),
('b301','padrao',2,225000.00),
('b401','padrao',2,235000.00),
('b501','cobertura',2,250000.00);

create table garagem (
  numero int(3) not null auto_increment,
  tipo varchar(20) default null,
  numero_ap varchar(5) default null,
  primary key (numero),
  key fk_gar_apartamento (numero_ap),
  constraint fk_gar_apartamento foreign key (numero_ap) references apartamento (numero)
);

insert into garagem values (1,'padrao','a101'),
(2,'padrao','a201'),
(3,'padrao','a301'),
(4,'padrao','a401'),
(5,'coberta','a501'),
(6,'padrao','b101'),
(7,'padrao','b101'),
(8,'padrao','b201'),
(9,'padrao','b201'),
(10,'padrao','b301'),
(11,'padrao','b301'),
(12,'padrao','b401'),
(13,'padrao','b401'),
(14,'coberta','b501'),
(15,'coberta','b501');

create table proprietario (
  rg varchar(15) not null,
  nome varchar(80) default null,
  telefone varchar(15) default null,
  email varchar(50) default null,
  primary key (rg)
);

insert into proprietario values ('12345678-0','carlos eduardo','(11) 3256-7890','carloseduardoead@email.com.br'),
('32145678-4','oswaldo lima','(11) 2314-9876','oswaldolimaead@email.com.br'),
('32156788-0','pedro castro','(11) 3452-8743','pedroead@email.com.br'),
('46536267-3','maria luiza','(11) 2345-1627','marialuizaead@email.com.br'),
('54367281-2','joana darc','(11) 4563-2315','joanadarcead@email.com.br'),
('74853928-2','benedito goes','(11) 3427-4132','beneditogoesead@email.com.br'),
('76534126-4','matheus henrique','(11) 2234-1123','matheushenriqueead@email.com.br'),
('98635314-5','augusto silva','(11) 4122-2134','augustosilvaead@email.com.br'),
('99987271-1','marcos vinicius','(11) 2124-2427','marcosviniciusead@email.com.br');

create table proprietario_apartamento (
  prop_ap_id int(3) not null auto_increment,
  numero_ap varchar(5) default null,
  rg_prop varchar(15) default null,
  primary key (prop_ap_id),
  key fk_pa_apartamento (numero_ap),
  key fk_pa_proprietario (rg_prop),
  constraint fk_pa_apartamento foreign key (numero_ap) references apartamento (numero),
  constraint fk_pa_proprietario foreign key (rg_prop) references proprietario (rg)
);

insert into proprietario_apartamento values (1,'a101','12345678-0'),
(2,'a201','32145678-4'),
(3,'a301','32156788-0'),
(4,'a401','46536267-3'),
(5,'a501','54367281-2'),
(6,'b101','74853928-2'),
(7,'b201','76534126-4'),
(8,'b301','98635314-5'),
(9,'b401','99987271-1'),
(10,'b501','99987271-1');
~~~

1. Desenvolva um procedure que atualize o valor de todos os apartamentos de acordo com o identificador do condomínio e o percentual de aumento passados como parâmetro. O processo deverá alterar o valor dos apartamentos somente do condomínio e percentual definido por um valor inteiro (10% = 10), passados como parâmetros.


2. Desenvolva um procedure de efetivação de compra de apartamento de acordo com o identificador do proprietário comprador e o número do apartamento passados como parâmetro. O processo deverá atribuir ao apartamento o identificador do novo proprietário.

---

[Voltar ao início!](https://github.com/monicaquintal)