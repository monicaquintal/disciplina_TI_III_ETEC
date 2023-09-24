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
- mesmo sem saber a senha, tendo somente o nome de usuário (login), é possível acessar o BD, pois o comando “--” faz com que o SGBD ignore o resto do comando, no exemplo ignorando a senha. 
- para prevenir os Injections SQL é fundamental que seja realizado um tratamento nos dados inseridos no sistema: parametrizar as consultas, utilizar “stored procedures” em SQL, limitar os privilégios no acesso ao
BD, seja por programas desenvolvidos ou por interfaces WEB de modo a garantir que os comandos SQL executados pelo SGBD sejam seguros.









---

[Voltar ao início!](https://github.com/monicaquintal)