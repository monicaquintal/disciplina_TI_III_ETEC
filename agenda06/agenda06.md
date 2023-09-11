<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://www.dropreal.com/br/wp-content/uploads/2021/03/icones_VALENDO.png" /></a>
</a>
<h1>Estudando Segurança de Sistemas de Informação.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda05">
<h2>Agenda 06: Segurança em Redes de Computadores e Dispositivos Móveis.</h2>
</div>

## 1. Conceitos:

### a) `Vírus`:
- pode ser parte de um programa de computador ou um programa completo,
usualmente malicioso, que realiza cópias de si mesmo infectando outros arquivos ou programas do computador. 
- um vírus não se propaga sozinho: depende da ação do usuário executar o arquivo infectado para agir contaminando o computador.
  - antigamente, se propagavam por intermédio de disquetes contaminados.
  - atualmente, o principal meio de disseminação dessas pragas virtuais são os pen drives e cartões de memória. 
- os tipos mais comuns de vírus são os vírus de macro, de script, recebidos por anexos e e-mail. 

### b) `Worm ou verme`:
- é um malware capaz de se propagar sozinho, de forma automática, pela rede de comunicação enviando cópias de si mesmo automaticamente de computador para computador. 
- ou seja, não depende da ação do usuário! 
- ele explora vulnerabilidades dos sistemas para se propagar. 
- causa muitos transtornos uma vez que consome recursos como: tempo de processamento da CPU, memória do computador e largura de banda de redes de comunicação, dependendo da quantidade de cópias ativas simultâneas na rede.
- após a infeção do computador, o worm identifica os computadores alvos para a sua replicação, depois realiza a tentativa de o envio das suas cópias para os alvos e para a ativação das cópias enviadas. 
  - podem acontecer algumas ocorrências: como a utilização de brechas de
segurança no sistema para a ativação automática, a execução de um
arquivo infectado pelo usuário ou algum evento específico, como a
utilização de mídias removíveis, como pen drive.

### c) `Bot`:
- abreviação proveniente de roBOT (robô).
- é um programa de computador que pode ser controlado a distância.
- seu mecanismo de infeção é semelhante ao do worm:
  - quando um computador é infectado por um bot ele é, geralmente, chamado de zumbi, pois pode ser controlado remotamente, sem que o seu utilizador tenha conhecimento disso.
- apessoa que controla os bots pode formar uma rede com milhares ou milhões desses em conjunto, aí temos uma botnet. 
- `Botnets` são frequentemente utilizadas para a realização de ataques em larga escala contra um alvo (computador, servidor ou instituição privada ou governamental) para retirá-lo de serviço.

### d) `Spywares` (ou programas espiões):
- programas desenvolvidos especificamente para monitorar as atividades que o usuário desenvolve no computador.
- trabalham coletando dados e informações e posteriormente enviando-as para terceiros. 
- podem funcionar capturando o que digitamos no teclado (chamados `keyloggers`), capturando telas do nosso computador (`screenloggers`) ou apresentando anúncios de propagandas (`Adwares`).
  - ***keyloggers*** e ***screenloggers*** são muito perigosos, porque podem capturar os nomes de usuários e senhas que digitamos. 
  - ***adwares*** exibem propagandas e anúncios para o desenvolvedor do programa obter um retorno financeiro de um software que é distribuído de uma forma gratuita na internet, por exemplo. Podem ser classificados como uma ameaça porque se utilizam de mecanismos pouco confiáveis para realizar suas tarefas como: se esconder no sistema instalado para dificultar a sua remoção, enviar dados de navegação na internet e utilizar o computador sem o consentimento do usuário para direcionar os anúncios exibidos no programa e tentar melhorar a eficiência dos produtos que estão sendo ofertados.

## 2. Como isso ocorre se não instalei nenhum programa?

- quando navegamos na internet por meio dos browsers, algumas as páginas visitadas podem armazenar arquivos individuais no nosso computador, chamados `cookies`. 
- cookies armazenam informações sobre onde clicamos no site, o que visitamos nele etc., podendo armazenar também o histórico de pesquisa e, sem o nosso consentimento, alguns sites realizam a leitura desses cookies e utilizam as informações para direcionamento de propagandas e outros fins.

### a) Cavalo de Troia, Trojan Horse ou Trojan:

- geralmente são programas gratuitos mal intencionados que executam as funções para as quais foi desenvolvido e anunciado como um disfarce. 
- realizam funções fraudulentas, agindo como os vírus, worms, bots e outros. 
- muitos trojans são distribuídos por e-mails falsos.
- vídeo [Os Invasores](https://www.youtube.com/watch?v=0Zxt7kS5miQ).

### b)  Spam:

- e-mails indesejados que são enviados em massa, automaticamente, por empresas ou pessoas, a fim de divulgar uma empresa ou um serviço.
- podem ser fonte de invasões também, porque os trojans são frequentemente enviados por Spam.
- além de causar perda de tempo, geram um aumento de tráfego  desnecessário nas redes de comunicação.
- frequentemente possuem conteúdos impróprios, podem provocar erros na rede e outros tipos de problemas.
- para se proteger dos spams, ativar AntiSpam da caixa de correio eletrônico, não fornecer o e-mail a sites que não considerar confiáveis, criar filtros para os e-mails e não clicar em links suspeitos de e-mails ou páginas de internet.

### c)  Ransomware:

- surgiu como outra modalidade de ataque. E
- malware que torna os dados do equipamento atacado inacessíveis, geralmente com a utilização de criptografia dos dados. 
- para reaver o acesso às informações, é exigido o pagamento de um resgate em criptomoedas.
- um computador pode ser infectado por um Ransomware ao se clicar em links que instalam programas contendo um código malicioso ou por meio de vulnerabilidades de sistema como quando uma empresa inteira foi
infectada via rede.
- quando um computador é infectado por um ransomware, raramente se tem acesso aos dados novamente, a não ser que você ou sua empresa tenha uma cópia de segurança (backup) dos dados.

## 3. Prevenção e proteção contra as ameaças virtuais

### a) Extensões/plugins

- extensões e plugins aumentam a produtividade e facilitam a vida no
cotidiano, poupando tempo e aborrecimentos. 
- contudo, ao adicionar uma extensão ao navegador, em geral, ela tem acesso a todas as informações que acessamos ou digitamos, inclusive o acesso a dados sigilosos. 
- por esse motivo, deve-se ter muito cuidado ao instalar plugins!
- nunca se deve instalar extensões que não são adquiridas das lojas oficiais dos desenvolvedores dos browsers, porque essas extensões não são verificadas quanto a presença de malwares.
- o mesmo se aplica em relação a apps de celular!

### b) Focar no usuário:

- instruir a pessoa que utiliza um computador a não adotar um comportamento de risco, e segurar o seu impulso de curiosidade, principalmente em relação a links ou ofertas suspeitas.
- numa empresa, deve-se assegurar que os empregados tenham conhecimento da sua Política de Segurança.
- algumas das soluções mais adotadas para combater as ameaças virtuais: 

1. Invista comportamentos preventivos dos usuários:
    - oriente os usuários a não clicar em links estranhos recebidos por e-mails ou em páginas suspeitas na internet. 

2. Caso tenha dúvidas da autenticidade de uma mensagem, confirme com o remetente antes de abrir qualquer link ou arquivo em anexo.
  - muitos vírus e worms se utilizam da lista de contato dos usuários para se propagar com maior efetividade.

3. Invista em um bom antivírus.

4. Instale um programa de firewall.
  - o firewall tem a função de tentar impedir ataques pela rede de computadores. 
  - considerar também a utilização de uma solução integrada de antivírus mais firewall, conhecidas como “Internet Security”, que facilitam a utilização por todos as funcionalidades estarem agrupadas em um único programa.

5. Sempre mantenha os seus programas atualizados.
  - desenvolvedores de software estão constantemente atualizando os programas com novas funcionalidades e corrigindo falhas e vulnerabilidades detectadas após o lançamento.

6. Utilize senhas de acesso complexas.
  - evitar a utilização de senhas fáceis como datas de nascimento, números de documentos pessoais, telefones, nomes de parentes, e palavras presentes em dicionário.
  - para criar senhas fortes e , utilizar letras minúsculas e maiúsculas, números e caracteres especiais (quando o sistema permite a utilização); também não podem ser curtas com menos de oito caracteres.

7. Troque as suas senhas periodicamente e não utilize a mesma para serviços diferentes.
  - otempo recomendado para a troca das senhas é de três em três meses.

8. Evite o compartilhamento desnecessário de informações pessoais.
  - não publique em redes sociais informações sobre onde mora, telefones de contatos, seus hábitos cotidianos.

9. Utilize sites de compras conhecidos na internet.
  - se estiver na dúvida sobre a autenticidade da oferta de um site, digite o endereço do site manualmente na barra de endereços do navegador e procure pela oferta/produto ao invés de clicar na oferta recebida por um link, pois muitos golpistas se utilizam de endereços quase idênticos ao site original com a diferença de um ponto ou uma letra que induza ao erro.
  
10. Não utilize o armazenamento automático de senhas oferecidos pelos navegadores de internet ou sistemas operacionais.

11. Não esqueça de sair do sistema.

12. Cuidado com as crianças.
  - oriente e supervisione o que as crianças e adolescentes fazem durante o uso da internet. 

13. Faça um backup dos dados regularmente.

14. Tenha bom senso.

--- 

## Exercitando

### 1. Diferencie um vírus de um worm.
- `Vírus` é um programa de computador malicioso que realiza cópias de si mesmo infectando programas e arquivos; depende que um programa ou arquivo seja executado pelo usuário.
- `Worm` pode fazer isso automaticamente enviando cópias de si mesmo pela rede explorando vulnerabilidades do sistema.

### 2. Como funciona um Ransomware?
- um ransomware é um programa malicioso que criptografa algumas regiões do disco rígido ou até mesmo o HD inteiro e, geralmente, exige um resgate pago em criptomoedas para ter os dados restaurados.

### 3. O que faz um keylogger? E um screenlogger?
- `Keylogger` é um software capaz de capturar tudo que digitamos no teclado de um dispositivo.
- `Screenlogger` tem a finalidade de capturar as telas do dispositivo,

### 4. Por que uma simples extensão para um browser pode ser perigosa para a privacidade?
- Um simples complemento ou extensão para um browser pode ser perigoso pois este pode ter acesso e coletar tudo que realizamos durante a navegação pela internet. Por isso devemos sempre ler quais privilégios essa extensão terá e sempre termos certeza de que a fonte e o desenvolvedor da extensão são confiáveis para evitarmos
problemas de roubo de dados.

### 5. Como podemos nos prevenir de ameaças virtuais?
- Algumas simples medidas já previnem muitas dores de cabeça quando o assunto são pragas virtuais. Podemos instalar antivírus, firewall, utilizarmos senhas complexas, não clicarmos em links suspeitos, desconfiar de promoções irreais, entre outros.

---

[Voltar ao início!](https://github.com/monicaquintal)