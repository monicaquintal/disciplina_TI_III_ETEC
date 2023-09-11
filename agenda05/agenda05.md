<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://www.dropreal.com/br/wp-content/uploads/2021/03/icones_VALENDO.png" /></a>
</a>
<h1>Estudando Segurança de Sistemas de Informação.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda05">
<h2>Agenda 05: Conceitos De Segurança Da Informação.</h2>
</div>

> "O único sistema verdadeiramente seguro é aquele que está desligado, preso a um bloco de concreto, trancado em uma sala revestida de chumbo com guardas armados." - Eugene H. Spafford, Professor na Purdue University.

## 1. Introdução

- o conceito de segurança da informação é bastante amplo e complexo. 
- a segurança da informação possui vários níveis e tipos distintos desde a proteção de um dado ou senha pessoal, passando pela segurança corporativa até questões envolvendo a segurança nacional de um país.

> ***Podemos definir Segurança da Informação como a preservação tríade Confidencialidade, Integridade e Disponibilidade das informações*** - sigla CID em português ou CIA em inglês (Confidentiality, Integrity and Availability).

1. `confidencialidade`:
- consiste na privacidade dos dados. 
- é a garantia que somente as pessoas que tenham autorização ou privilégios necessários possam acessar as informações que estão armazenadas ou em processamento em um sistema ou que são transmitidas por meio das redes de comunicação.

2. `integridade`:
- corresponde à consistência, precisão e confiabilidade das informações. 
- refere-se ao grau de confiabilidade da informação garantindo que não foram manipuladas sem as devidas permissões.

3. `disponibilidade`:
- garante que as informações estejam acessíveis as pessoas autorizadas sempre que forem necessárias garantindo a prestação do serviço sem interrupções.

### Mas que tipo de informação devemos proteger?

- devemos proteger todas as informações pessoais ou de uma organização que estão armazenadas em sistemas computacionais (servidores, discos, pen drives) ou impressas (papéis, microfilmes), que são transmitidas por meios de comunicação (e-mail, fax, comunicação de dados).
- protegemos todas as informações que podem causar danos, seja para uma única pessoa (dados pessoais) quanto para uma corporação.

### Por que devemos proteger as informações?

- para nos prevenirmos dos mais variados golpes e fraudes presentes na internet, se pensarmos como pessoas físicas. 
- pensando como uma pessoa jurídica ou empresa, protegemos as informações de espionagem industrial, hackers, gravações de comunicação, acessos
não permitidos, empregados que agem de má fé, entre outros.

### Alguns conceitos e terminologias:

1. `Vulnerabilidade`: 
- é uma fraqueza de um ativo ou sistema que podem ser exploradas para fins espúrios.
- pode ser física (hardware), lógica (software) ou envolvendo algum processo falho que comprometa o sistema. 
- exemplo: um datacenter localizado em uma área potencialmente sujeita a desastres naturais, senhas fracas, falta de criptografia nos dados ou controle de acesso físico etc.

2. `Ameaça`: 
- modo como uma vulnerabilidade pode ser descoberta, causando um incidente de segurança.
- exemplo: falha de hardware, roubo.

3. `Risco`: 
- probabilidade de comprometimento da segurança por parte de uma ameaça aproveitando-se de uma vulnerabilidade em um ativo.

4. `Proteção`: 
- procedimento utilizado para diminuição de um risco.
- exemplo: antivírus, firewall.

5. `Incidente`: 
- quando um ou mais propriedades da tríade CIA foram violados.

## 2. Mecanismos de Segurança

### a) Segurança física

- devemos proteger o equipamento físico ou hardware, pois sem essa proteção de nada adiantará protegermos a parte lógica.
- o objetivo de protegermos fisicamente o equipamento e as informações contidas neles é ***impedir o acesso não autorizado aos recursos de hardware***.
- `tipos de controles de acesso físico`:
  - identificação pessoal por meio de catracas, utilização de crachás, biometria, sala-cofre para a entrada em área restrita.
  - a área onde fica a infraestrutura da sala de comunicação e armazenamento de dados de uma empresa deva ser uma área com acesso físico restrito com controle estrito de entrada e saída de equipamentos, inclusive dispositivos móveis como notebooks, celulares e pen-drives. 
  - controle de intrusão e monitoramento por CFTV (Circuito Fechado de Televisão).
  - deve-se pensar também que catástrofes podem acontecer, portanto, é preciso avaliar e tomar precauções quanto ao risco de inundações, incêndios, problemas elétricos, climatização.

### b) Segurança Lógica

- inclui tudo que está relacionado ao sistema lógico como os dados que estão contidos no hardware e são acessados por pessoas ou outros sistemas.
- controle de acesso deve ser feito por meio da utilização de senhas, listas de controle de acesso, criptografia, firewall. 
- as ações realizadas no sistema devem ser monitoradas por meio da utilização de arquivos de registros de atividades (logs).

> O ideal para um maior nível de segurança é que seja feita uma convergência entre segurança física e lógica, criando dessa forma uma série de procedimentos institucionalizados que devem ser divulgados para todos os colaboradores da empresa. Apesar de tomar todas as precauções físicas e lógicas, quem garante a segurança do sistema implementado são as pessoas, logo, devem ser o alvo da conscientização!

## 3. Políticas de Segurança (PS) da Informação

- são um conjunto de procedimentos e regras que gerenciam as informações e equipamentos de uma empresa. 
- devem ser seguidas por todos os funcionários, colaboradores sejam eles internos ou externos como prestadores de serviços.
- `objetivo`: proteger a confidencialidade a integridade e disponibilidade das informações empresariais, evitando riscos desnecessários provenientes da má utilização dos equipamentos. Com a redução dos riscos, tenta-se também minimizar os eventuais danos provocados por algum incidente que ocorra. 
- o ambiente do sistema de informação deve ser monitorado constantemente para verificar se está sendo utilizado corretamente e, também para procurar falhas e correções o mais breve possível, mesmo que isso inclua uma alteração nas políticas de segurança.
- a PS deve ser coordenada e implementada, preferencialmente, por especialistas da área de segurança de informação em conjunto com os administradores da empresa.
  - a PS não deve ficar restrita somente a área de Tecnologia da Informação, mas deve abranger a empresa como um todo.
  - deve se integrar à visão, à missão, as metas e os valores do negócio como um todo!!!

### Para elaborarmos uma boa política de segurança devemos nos atentar aos seguintes itens:

- Definição dos processos ou recursos prioritários para definir as prioridades de segurança.
- Classificação das informações como confidenciais ou públicas.
- Definição dos objetivos de segurança da informação da instituição.
- Realização de análise de risco.
- Padronização de qualidade que os sistemas devem atender.
- Controle de acesso aos recursos e sistemas computacionais
- Uso da rede, incluindo intranet e internet.
- Normatização dos procedimentos dos usuários.
- Definição dos direitos e deveres dos usuários.
- Instalação de programas de computador.
- Utilização de e-mails, sejam eles corporativos ou pessoais.
- Regras para criação e utilização de senhas de acesso.
- Regras para utilização de equipamentos pessoais como notebooks, telefones celulares, pen-drives, mídias externas, entre outros na rede interna.
- Utilização de antivírus.
- Métodos de supervisão das violações da PS estabelecida.
- Estabelecimento claro das punições relativas a violação da PS vigente.
- Auditoria.
- Backup das informações.
- Princípio da continuidade de negócio em casos adversos.

> Uma vez elaborada a PS, é preciso garantir que seja amplamente divulgada e que todos os colaboradores internos e externos da instituição tenham amplo acesso a ela, bem como o treinamento adequado quanto aos seus direitos, deveres e procedimentos a serem seguidos cotidianamente, a fim de se evitar futuros questionamentos legais. E, uma vez criada, definida e divulgada a política de segurança, essa não deve ser esquecida: deve ser constantemente atualizada, conforme as necessidades da organização.

## 4. Backup

- é uma cópia de segurança dos dados de um dispositivo em algum outro como um HD externo, em outro computador ou servidor ou atualmente
na famosa nuvem (internet).
- as empresas devem ter sempre um ou mais de um backup para garantir a continuidade de seus negócios em caso de um desastre, evitando dessa forma a perda de informações.
- outra recomendação é que a cópia de segurança não seja feita nunca na mesma máquina onde se situam os dados originais. Se possível, deve ser feita em outro local (outra mídia removível como um HD externo, outro servidor ou outro data center) com uma boa distância física para salvaguardar as informações.
- ***tipos***:
  - backup normal: copia todos os arquivos selecionados, e marca cada um desses arquivos para identificar que já foram copiados.
  - backup de cópia: copia todos os arquivos selecionados, porém não marca os arquivos copiados.
  - backup incremental: copia somente arquivos criados ou modificados, e marca os arquivos copiados.
  - backup diferencial: copia somente arquivos criados ou modificados, e mas NÃO marca os arquivos.
  - backup diário: copia somente os arquivos criado ou modificados hoje, e não marca.

## 5. Criptografia e Firewall

### a) `Firewall`:
- traduzindo livremente para o português: parede de fogo.
- pode ser um hardware, um software ou uma combinação de ambos.
- é um dispositivo de segurança da rede que monitora o tráfego de rede de entrada e saída, decidindo se permite ou bloqueia a passagem dos dados de acordo com as regras definidas para o seu funcionamento.
- é o responsável por analisar o tráfego da rede bloqueando a entrada de possíveis conteúdos maliciosos. 
- protegem as redes internas colocando uma barreira antes de atingir a rede externa como a internet.
- usuários domésticos estão habituados a utilizar soluções do tipo Internet Security que englobam um antivírus e um firewall e está de bom tamanho para a proteção doméstica; porém, para as empresas é necessário um controle mais estrito do tráfego das informações e por isso muitas
vezes elas utilizam uma combinação de um firewall por hardware e software. 
- firewall por hardware é um equipamento físico projetado especificamente para isso podendo atuar com softwares instalados na rede ou nos computadores locais individuais.

> O próprio Windows possui um firewall embutido e ativado por padrão chamado Windows Defender Firewall.

### b) `Criptografia`:
- a palavra criptografia vem da junção das palavras gregas "kryptós" que significa oculto com "Gráphein" que quer dizer escrita. 
- trata-se de uma técnica onde uma mensagem original é codificada utilizando um artifício, ou atualmente um algoritmo matemático, para que, se caso ela seja interceptada não seja possível a sua leitura sem a sua decodificação.
- é usada também para manter o sigilo no armazenamento de dados sensíveis e nas telecomunicações para o envio de senhas, transações bancárias, mensagens instantâneas etc.
- é importante uma empresa armazenar, transportar ou transferir osseus dados sigilosos de modo criptografado, pois se ocorrer algum problema como perda de dispositivos ou ataques hackers essas informações não sejam comprometidas.

---

## Exercitando!

1. Defina os conceitos de Confidencialidade, Integridade e Disponibilidade.
- Confidencialidade é quando garantimos que a informação só pode ser acessada por pessoas autorizadas.
- Integridade é a proteção da exatidão da informação.
- Disponibilidade é a garantia de que a informação pode ser acessada sempre que requisitada pelas pessoas autorizadas
<br>

2. Qual é a importância do Backup para uma organização.
- Para uma empresa manter uma rotina ou política de backup é fundamental, pois caso ocorra uma eventualidade com os dados originais o funcionamento não seja interrompido (continuidade de negócios).
<br>

3. O que é criptografia.
- A criptografia é uma técnica utilizada para se codificar uma mensagem ou dados a fim de que estes não sejam
entendidos caso sejam interceptados por terceiros.
<br>

4. É importante uma instituição possuir uma política de segurança. Por que?
- Para uma empresa ser segura no âmbito digital é importante ter uma política de segurança robusta, pois é ele que definirá quais são as normas e procedimentos que serão utilizados com os recursos de TI da empresa garantindo a tríade da CIA. 
- Ela estabelece também o que deve ser feito em casos de inconformidades no sistema, estabelecendo inclusive punições aos infratores.
<br>

5. Cite exemplos de segurança física de uma instalação de TI.
- Alguns exemplos que podemos citar de segurança física de um ambiente de TI são controle de acesso utilizando crachás, senhas de acesso ou biometria, sala-cofre, circuito fechado de monitoramento por câmeras de segurança (CFTV).

---

## Fichário

<em>
"Sabemos que a criptografia é uma técnica utilizada para codificar uma mensagem de modo que esta não possa ser facilmente entendida por quem não deve ter acesso. Utilizando a linguagem de programação JAVA, elabore um programa simples de criptografia. O programa deve ler uma sequência de caracteres (String), converter essa String para um vetor de caracteres e depois para um vetor de números inteiros seguindo a tabela ASCII. Para realizar a criptografia o software deve somar 10 unidades aos números e apresentá-los em uma String de saída criptografada.
<br>

Dicas:
- Para saber se a conversão de um caractere para um número inteiro está correta acesse o site www.asciitable.com. Ex.: caractere C = 67. Note que letras maiúsculas e minúsculas possuem códigos diferentes logo C ≠ c, c = 99.
- Utilize a função &lt;variável&ht;.length; para determinar o tamanho de uma String, onde variável é um tipo String. Ex.: String a; a.lengh;
- A conversão de um caractere para um número inteiro da tabela ascii é uma conversão de tipo simples de char para integer.
- O mesmo vale para a conversão de volta de um número inteiro para caractere na saída final da mensagem criptografada, porém com conversão de integer para char.
- Utilize o JOption Pane para realizar a entrada e saída de dados.

Exemplo:

- Ao entrarmos com a String: “CPS”, o programa deve converter para números, que segundo a tabela ascii ficarão: 67, 80 e 83, somar 10 unidades: 77, 90 e 93 e convertê-los novamente para uma String, resultando em “MZ]”.
<em>

---

[Voltar ao início!](https://github.com/monicaquintal)