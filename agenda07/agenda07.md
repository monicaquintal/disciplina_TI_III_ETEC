<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://www.dropreal.com/br/wp-content/uploads/2021/03/icones_VALENDO.png" /></a>
</a>
<h1>Estudando Segurança de Sistemas de Informação.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda07">
<h2>Agenda 07: Tipos de Invasões e Vulnerabilidades.</h2>
</div>

## 1. Introdução

- qual é a situação ideal para um crime
perfeito na internet?
  - de um lado, há o usuário desprevenido de redes sociais.
  - do outro, o agente malicioso que se aproveita da disseminação voluntária de informações e utiliza esse material para benefício próprio.

### Como funciona esse tipo de ataque?

- práticas clássicas de phishing (quando uma pessoa é “pescada” com um link malicioso enviado por e-mail) já não são mais tão eficazes quanto em outros tempos.
- `uso de personas virtuais`:
  - batedores escolhem suas vítimas, geralmente funcionários específicos de empresas, que geralmente possuem informações relevantes da corporação. 
  - com o alvo na mira, os crackers entram em ação e levam o contato para o WhatsApp.
  - com todas as informações disponíveis (e entregues deliberadamente pelas presas) em mãos, os criminosos criam golpes, que posteriormente são aplicados por e-mail.

### O que podemos aprender com isso?

- não se deve confiar cegamente nas redes sociais.
- a confiança implícita pode tornar os ataques de phishing de redes sociais mais bem-sucedidos.

### Engenharia Social:

- na engenharia social são utilizadas técnicas que tentam convencer o alvo do golpe, com técnicas
psicológicas, a fornecerem dados confidenciais
necessários a aplicação do golpe ou realizar ações
como envio de e-mails, cópia de arquivos sigilosos ou
transferências de fundos. O alvo primário é o ser
humano. 
- outro exemplo comum no Brasil é quando o criminoso liga para a vítima falando ser do banco na qual ela tem conta alegando que o seu cartão está com um problema qualquer e para a substituição é necessário que a vítima envie o cartão com a senha de volta para o banco por intermédio de um motoboy. 
- a Engenharia Social não está presente somente nos meios virtuais e eletrônicos. Por isso, sempre que alguém pedir uma informação por meios não usuais ou conte alguma história que soe estranha, cheque primeiro com a pessoa ou empresa solicitante, por um meio que seja comprovadamente seguro, se a  solicitação é real.

## 2. Ataques de Negação de Serviço

- ataques de negação de serviço (`Denial of Service – DoS`) geralmente se concentram tipicamente em servidores da Internet.
- são feitos com o intuito de congestionar os meios de comunicação até o servidor ou sobrecarregar o alvo para que a sua resposta fique lenta por consumir recursos de sistema (memória RAM, uso do processador etc.), forçando a sua reinicialização, fazendo com que o serviço oferecido não possa mais ser fornecido.
- o ataque do tipo DoS pode ser feito explorando-se falhas no protocolo TCP/IP (Transmission Control Protocol/Internet Protocol), sendo possível ocorrer em qualquer computador que o utilize. 
- atualmente os ataques DoS evoluíram para `DDoS (Distributed Denial of Service – Negação de Serviço Distribuído)`. 
  - em um ataque DDoS centenas ou até milhares de computadores, chamados de computadores zumbis, formam um “exército” com o intuito de atacar um único alvo. 
  - esses zumbis são comandados por um mestre que envia as ordens da investida.

### Como funciona o ataque DDoS?

1. um worm ou um phishing scan contamina uma máquina, tornando-a um zumbi, respondendo aos comandos enviados pelo mestre.
2. quando um ataque é iniciado, o mestre envia um comando que programa todos os zumbis para atacarem um mesmo alvo, geralmente um servidor, na mesma data e hora. 
3. quando o ataque DDoS é iniciado, o servidor atacado recebe um número de solicitações de serviços proveniente da rede zumbi muito superior à sua capacidade de trabalho, causando lentidão nas respostas e podendo evoluir para uma reinicialização do sistema ou travamento completo.
4. quando o servidor atacado trava ou reinicia, ocorre a negação do serviço: o cliente realiza requisição, e o servidor não responde.
5. exemplo de vírus que explora rotinas de negação de serviço:
MyDoom.

### Como prevenir ataques DoS e DDoS?

- é uma tarefa complicada, pois há várias ferramentas e técnicas diferentes para os ataques, que permitem disfarçar o pacote transmitido pela rede que contém ataque em um pacote de rede legítimo que trafega no servidor, dificultando a identificação por firewalls e softwares de monitoramento. 
- uma saída seria aumentar a capacidade dos servidores, mas isso nem sempre é viável economicamente.

## 3. SQL Injection

- funciona por meio de uma inserção ou manipulação (injection) de uma consulta SQL que é enviada diretamente a um banco de dados quando não
existe uma validação dos dados antes da realização desta consulta.
- exemplo: quando acessamos o Ambiente Virtual de Aprendizagem do curso, a primeira informação solicitada é o nome do usuário e senha. Que pode gerar um comando SQL da seguinte forma:

~~~sql
select * from usuario where login = 'user' and password = 'senha';
~~~

- o problema começa se o sistema não realiza nenhuma verificação nos dados que o usuário digitou, pois se o site for mal intencionado, pode realizar uma Injection SQL ao substituir o campo user por admin’-- e uma
senha qualquer.

~~~sql
select * from usuario where login = 'admin'-- and password = 'senha';
~~~

- esse comando faria com que o banco de dados (BD) conectasse o usuário com a login admin, geralmente utilizado por administradores, com acesso privilegiado. 
- mesmo sem saber a senha, tendo somente o nome de usuário (login), é possível acessar o BD, pois o comando "--" faz com que o SGBD ignore o resto do comando, como a senha. 
- para prevenir os Injections SQL, realizar tratamento nos dados inseridos no sistema: parametrizar as consultas, utilizar "stored procedures" em SQL, limitar os privilégios no acesso ao BD, seja por programas desenvolvidos ou por interfaces WEB, de modo a garantir que os comandos SQL executados pelo SGBD sejam seguros.

## 4. Prevenção de ataques e invasões

### a) Testes de Varredura e análise:
- varredura e a análise do sistema como um todo, para identificar as  ulnerabilidades do sistema.
- depois de instalar os firewalls, seja por software ou hardware, e instalar os antivírus, deve-se utilizar programas específicos chamados `scanners` para a varredura de vulnerabilidade na rede. 
- os scanners analisarão os softwares instalados, a infraestrutura e a políticas de segurança em busca de vulnerabilidades, realizando uma classificação por nível (baixo, médio e alto risco).
- exemplos de programas que realizam a varredura: netsparker, aconetix,
openvas, Nexpose e Wireshark.
- de acordo com o resultado do teste de varredura, o analista de TI realizará a análise dos dados para sanar as vulnerabilidades detectadas, priorizando as mais críticas (alto risco).

### b) Teste de Penetração e vulnerabilidades:
- dependendo do tamanho da empresa, organização e ramo de atividade, somente a varredura e a análise podem não ser suficientes, pois apenas identifica as vulnerabilidades. 
- em um `teste de penetração` ou pentest (penetration test), além da identificação da vulnerabilidade, os testadores tentam explorá-la (invadir o sistema), avaliando os danos que a invasão bem sucedida pode causar na empresa, podendo mensurar financeiramente com os sistemas que foram afetados ou paralisados. 
- costumam ser contratadas empresas terceirizadas para realizar um pentest.
- um pentest pode ser ***classificado de três formas***:
  - `White-box`: quando as informações sobre a infraestrutura da empresa são fornecidas, facilitando e otimizando a busca por vulnerabilidades.
  - `Black-box`: quando nenhum tipo de informação é fornecido e os testes são conduzidos de fora do ambiente da empresa.
  - `Grey-box`: quando, de dentro da empresa, o testador tenta invadir outros ambientes corporativos internos. Interessante para testar e auditar processos de segurança internos.
- o processo de um pentest, em geral, conta com os seguintes ***passos***:
  - 1. `Footprint`:
    - fase inicial de um pentest.
    - são pesquisadas informações como endereços de IP, informações de colaboradores das empresas, endereços de correio eletrônico, versões dos softwares ativos na rede, sistemas operacionais utilizados (finger-print) e números de telefones.
    - muitas dessas informações podem ser descobertas em serviços de busca na internet como Google, Whois etc.
  - 2. `Varredura e Descoberta`:
    - nessa fase, o pentester tem um contato direto com o sistema a ser testado utilizando ferramentas de escaneamento de rede como Nmap e ZenMap para identificar portas, serviços ativos, ranges de IP etc.
  - 3. `Identificação de Vulnerabilidades`:
    - ferramentas de escaneamento de vulnerabilidades são usadas para detectar possíveis brechas no sistema, como programas de segurança mal configurados ou atualizações de falhas de segurança conhecidas em programas não realizadas.
  - 4. `Ataque ou Exploração`:
    - o pentester tentará invadir o sistema por meio das explorações de brechas de segurança conhecidas ou identificadas na fase anterior, sempre tentando passar despercebido pelos administradores de sistema, ocultando os seus rastros.
  - 5. `Análise de Risco e Remediação`:
    - após a invasão, os riscos são analisados e são recomendadas as atualizações e/ou modificações nos sistemas, com a devida documentação para o contratante.
  - 6. `Relatórios`:
    - elaborado um relatório com a metodologia utilizada, vulnerabilidades encontradas, ataques realizados e correções necessárias.

---

## Exercitando e aprimorando

### 1. Defina Engenharia Social.
A Engenharia social pode ser definida como um conjunto de métodos psicológicos de persuasão ao usuário, muitas vezes contando com a ingenuidade deste, para ganhar a sua confiança, fazendo com que a vítima revele informações sensíveis para serem utilizadas em um ataque aos sistemas de uma empresa.

### 2. Como funciona um ataque do tipo DDoS?
Um ataque do tipo DDoS funciona com centenas ou milhares computadores de uma rede “zumbi” infectados com um malware controlado pelo criminoso no qual em uma mesma data e hora atacam um único alvo com o intuito de tentar derrubar o serviço oferecido por este servidor causando a negação de serviço.

### 3. O que é uma SQL Injection?
Consiste na inserção de um código em linguagem SQL em uma query de um programa ou aplicação WEB, com o intuito de obter dados sigilosos ou ganhar acesso não autorizado para a manipulação de um Banco de Dados.

### 4. Uma Varredura e análise de um sistema é o mesmo que realizar um Pentest?
- A varredura ou análise do sistema realiza somente uma identificação das vulnerabilidades do sistema testado para que sejam corrigidas. 
- Já um pentest, além da execução da varredura e análise, também realiza testes de invasão efetiva do sistema, indicando as brechas para a intrusão do sistema.

### 5. O que é Footprint? E Fingerprint?
- Footprint consiste na análise inicial de um sistema alvo com a intenção de obter dados de forma segura sem ser detectado. Essa investigação inicial inclui pesquisas em mecanismos de busca, consultas ao Whois, visitas as páginas da internet da empresa, saber os domínios e endereços de IP, informações sobre os funcionários da empresa, endereços de e-mail etc.
- Fingerprint é uma parte do footprint que identifica o sistema operacional e demais softwares do alvo. Para isso, são utilizadas ferramentas de scanner de rede.

---

## Fichario

- Estudamos sobre diversos tipos de ataques que podem ser realizados, tendo as empresas como alvos. Muitos desses ataques podem ter fins políticos, ideológicos ou simplesmente com o intuito de paralisar um serviço ou toda uma empresa. Os ataques do tipo SQL Injection podem ser executados por qualquer pessoa com um pouco de conhecimentos de páginas HTML, PHP, ASP.net, JavaScript e banco de dados pode executar.
- Para sintetizar os conhecimentos sobre esse tipo de ataque, pesquise, exemplifique e explique passo a passo, como podemos obter dados não autorizados de um BD qualquer utilizando SQL Injection.
- O exercício deve ser entregue em documento do formato Word no ambiente virtual de aprendizagem. Observação: explique como cada comando em SQL se comporta ao ser executado pelo SGBD.

---

[Voltar ao início!](https://github.com/monicaquintal)