<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original-wordmark.svg" /></a>
</a>
<h1>Estudando Sistemas Embarcados - Arduino.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agendas10e11">
<h2>Agendas 10 e 11: Módulo I - Estruturas Básicas.</h2>
</div>

- antes de iniciar a aula, acesse o [site](https://mooc.cps.sp.gov.br/ead/course/view.php?id=10) para fazer a inscrição, clicando em Criar uma conta.
- realizado o cadastro e acesso no curso, clicar em "Apresentação" e no menu percorra pelas abas: 1- Boas-vindas,  2- Apresentação, 3- Temas, 4- Baixe aqui.
- iniciar os estudos clicando na imagem e acessando o Módulo I - Estruturas Básicas e percorra pelas abas: - Introdução - Protoboard - Resistores, potenciômetros e leds - Introdução a Lógica de Programação - Estrutura de Programação - Instruções de entrada e saída - Ambiente de Desenvolvimento Arduíno - Experimento 1 finalizando em Experimento 2.
- curso totalmente a distância, com duração de 30 horas, divididas em quatro módulos e uma prova on-line final, obrigatória.

## 1. Apresentação

- `Arduíno` é uma plataforma de prototipagem eletrônica que permite, a partir de uma linguagem de programação, desenvolver eletronicamente objetos inteligentes.
- o curso de Arduino trata-se de uma formação inicial que tem o intuito de capacitá-lo(a) para compreender um pouco mais sobre o universo da programação aplicada a objetos.
- os módulos estão divididos em três partes:
  - 1. Hardware: explica, em detalhes, os componentes eletrônicos.
  - 2. Programação: aborda a introdução à lógica de programação.
  - 3. Aplicação: demonstra os experimentos com o simulador on-line e com o kit físico do Arduino.

## 2. Temas:

### Módulo 1 - Estruturas Básicas

1. Introdução ao Arduino
2. Protoboard
3. LED, resistores e potenciômetro
4. Introdução à lógica de programação
5. Estruturas de programação
6. Instruções de entrada e saída
7. Baixando o software para o ambiente de desenvolvimento Arduino
8. Acendendo e piscando um LED
9. LED com comando

### Módulo 2 - Chaveamento

1. Buzzer e Push Button
2. Estruturas de decisão
3. Estruturas de repetição
4. Semáforo
5. Piano

### Módulo 3 - Sensores

1. Sensores
2. Display de 7 segmentos
3. Controle remoto
4. Caminho de LED com sensor de luz
5. Display de 7 segmentos com sensor de boia

### Módulo 4 - Motores

1. Motores elétricos
2. Motor
3. Motor com potenciômetro

## 3. Baixando:

- se tiver o Kit Arduino Uno e o protoboard, você pode elaborar os projetos fisicamente. 
- caso não tenha, também poderá elaborar todos os experimentos do curso, utilizando o [simulador de Arduino Uno on-line](https://youtu.be/6pvwCNw3zao): [TinkerCad](https://www.tinkercad.com/).
- disponibilizada [apostila](./assets/apostila_Arduino.pdf) para estudos.

---

<div align="center">
<h2>Módulo I - Estruturas Básicas.</h2>
</div>

## 1. [Introdução](https://www.youtube.com/watch?v=5CrIR7qwpOU)

### a) O que é o Arduino?
- pequeno computador com hardware limitado (consome pouca energia elétrica), livre e de placa única.
- é uma plataforma de prototipagem.
- trabalha com código aberto.
- programação em C (mais rústica, comando simples de serem trabalhados).
- pode ser utilizado por qualquer pessoa interessada em produzir equipamento eletrônico de automação.

### b) Estrutura:

<div align="center">
<img src="./assets/images/estrutura-arduino.png" width="50%">
<p><em>Placa do Arduino.</em></p><br>
</div>

1. ***Pinos digitais***:
  - tensão de 5V.
  - funciona como entrada ou como saída de dados.
  - trabalha com dados binários: 0 (low - 0V) ou 1 (High - 5V).
  - exemplo: se ligar um LED num pino digital, ele acende e apaga.

2. ***Pinos digitais PWM***:
  - tensão de 5V.
  - funciona como entrada ou como saída de dados.
  - trabalha com variação de sinais digitais entre 0 e 255.
  - exemplo: se ligar um LED num pino digital PWM, é possível fazerf uma variação da tensão enviada, e o LED vai aumentando ou diminuindo a luminosidade de acordo com o comando.
  - precisam ser programadas para que enviem o sinal.

3. ***Pinos analógicos***:
  - funcionam apenas como entradas de sinal.
  - quando recebem 5V, o valor da conversão para digital será de 1023, ou seja, é possível ober uma variação de 0 a 1023.

4. ***Botão de Reset***:
  - permite que toda programação implementada pelo usuário (chamada "latente") na placa seja apagada.

5. ***Conector USB***:
  - faz ligação do computador com a placa Arduino.
  - permite a gravação de programas e fornece alimentação elétrica para o funcionamento da placa.

6. ***Conector de alimentação***:
  - permite a alimentação da placa por fonte ou bateria pelo pino Jack.

7. ***Pinos de alimentação*** (portas):
  - **RES**: conectado ao pino Reset; pode ser utilizado para um reset externo da placa (apaga toda a menmória da placa).
  - **3.3V**: fornece tensão de 3,3V para alimentação de shield e módulos externos. Diferente dos pinos digitais, já há alimentação direta na placa, sem se preocupar com a programação.
  - **5V**: fornece tensão de 5V para alimentação de shield e circuitos externos. Diferente dos pinos digitais, já há alimentação direta na placa, sem se preocupar com a programação.
  - **GND**: terra (negativo) - dias embaixo e uma ao lado da porte 13 digital, em cima da placa.
  - **VIN**: alimentação da placa através de shield ou bateria externa. Se alimentada pelo pino Jack, a tensão da fonte estará nesse pino.

## 2. [Protoboard](https://youtu.be/ISTSIdiP2jw):

### a) Multímetro:
- tem a capacidade de medir as ***grandezas elétricas***:
  - tensão elétrica - Volts (V).
  - corrente elétrica - Amperes (A).
  - resistência elétrica - Ohms (Ω).
- o multímetro possui um seletor, onde escolhemos o que desejamos medir (e medições básicas: VOLTS DC, AMPERES DC, VOLTS AC e OHMS).
- possui as pontas de prova (conectores externos ao multímetro que farão a conexão entre o local da medição e o multímetro) e bornes (onde conecta as pontas de prova).
- observação: 
  - AC ou CA (corrente alternada ~).
  - CC (corrente contínua =).

<div align="center">
<img src="./assets/images/formas-medicao-multimetro.png" width="70%">
<p><em>Formas de medição do multímetro.</em></p><br>
</div>

### b) Protoboard:
- uma placa de ensaio ou matriz de contato.
- é uma placa com furos e conexões condutoras para montagem de circuitos elétricos experimentais.
- a grande vamtagem da placa de ensaio na montagem de circuitos eletrônicos é a facilidade de inserção de componentes, uma vez que não necessita de soldagem.
- placa de circuito impresso (PCI): é a placa definitiva, feita após o protótipo realizado no protoboard! Nela, são criadas as trilhas e soldados componentes, sendo definitiva.

<div align="center">
<img src="./assets/images/exemplo-ligacao-arduino.png" width="70%">
<p><em>Exemplos de usos do Protoboard.</em></p><br>
</div>

## 3. [LED, resistores e potenciômetro](https://youtu.be/aajFyefjleY)

### a) Resistores:

- componentes que têm por finalidade oferecer uma oposição (resistência elétrica - unidade ohm Ω) à passagem de corrente elétrica, através de seu material.
- causam queda de tensão em um circuito elétrico e limitma a corrente.
- é possível utilizar os resistores para controlas a corrente elétrica sobre os componentes desejados (provocam diferença de potencial).
- Lei de Ohm = V (tensão) = R (resistência) * I (intensidade).

<div align="center">
<img src="./assets/images/codigo-de-cores-resistores.png" width="50%">
<p><em>Código de cores dos Resistores.</em></p><br>
</div>

- normalmente utilizamos resistores de 4 e 5 faixas.
  - 1ª e 2ªs faixas: algarismo. (1 a 3, caso seja de 5 faixas)
  - 3ª faixa: multiplicador (4, caso seja de 5 faixas).
  - 4ª faixa: tolerância (5, caso seja de 5 faixas). 

### b) Potenciômetro:

- componente eletrônico usado para variar a resistência.
- pode ser definido como um tipo especial de resistor, pois é uma resistência elétrica variável (resistor variável).
- possui uma trilha de carvão que, dependendo da posição do cursor (W), determinará uma resistência.

<div align="center">
<img src="./assets/images/potenciometro.png" width="70%">
<p><em>Potenciômetro.</em></p><br>
</div>

- usado para controlar a intensidade da luminosidade de uma lâmpada, por exemplo (dimmer), controlar a velocidade do ventilador, volume de rádio.

### c) LED (Light Emitting Diode ou Diodo Emissor de Luz):

- a intensidade da luz produzida pelo Led é diretamente proporcional à corrente que flui através dele.
- o anodo (+) do Led pode ser identificado pelo terminal mais longo do Led.
- o catodo (-) do Led é o terminal menor e também possui um chanfro (marca chata).
- a cor da luz emitida depende do material utilizado no cristal e também do nível de dopagem.
- os LEDs suportam, normalmente, no máximo 2V / 20mA (momento que calcularemos com a resistência que utilizaremos no LED, para não queimá-lo - exemplificado a partir de 10 min [no vídeo](https://www.youtube.com/watch?v=aajFyefjleY)).

## 4. [Introdução à lógica de programação](https://www.youtube.com/watch?v=1LvvZek7LXY)

### a) Lógica de programação:

  - problema inicial = automação de um processo.
  - algoritmo = modelo lógico e eletrônico.
  - ambiente + linguagem = IDE + linguagem PROCESSING, baseada na linguagem C.
  - solução!

### b) Estrutura de programação para o Arduino:

- `Sketch`: 
  - é um programa (conjunto de instruções em uma linguagem, nesse caso, chamada processing).
  - possui 2 rotinas principais em seu modelo:
    - `inicialização`: inicialização de postas e componentes.
    - `looping infinito`: contém o conjunto principal de comandos.
  - enquanto não substituir o sketch na memória interna do Arduino, ele continuará executando esses mesmos processos dentro da mesma ordem!

~~~
// inicialização:

void setup()
{
  configurações do ambiente físico do Arduino
}

// loop infinito:

void loop() {
  instruções de execução do projeto
  o que queremos que processe durante seu funcionamento
  metodologia top-down: ocorre na ordem de leitura, de cima para baixo!
}
~~~

## 5. [Estruturas de programação](https://www.youtube.com/watch?v=9pDKzc4H1Vo)

### a) Exemplo de estrutura de programação para piscar um LED (aceso e apagado):

~~~
void setup() 
{
  pinMode(13, OUTPUT); 
    // ou seja, porta/pino n° 13 confugurado como saída (output)
}

void loop() 
{
  digitalWrite(13, HIGH);
    // HIGH, sinal 1
  delay(1000);
  digitalWrite(13, LOW);
    // LOW, sinal 0
  delay(1000);
}
~~~

## 6. [Instruções de entrada e saída](https://www.youtube.com/watch?v=FyNjgKS78XY)

### a) Exemplo:

~~~
void setup() 
{
  pinMode(13, OUTPUT); 
  Serial.begin(9600);
}

void loop() 
{
  digitalWrite(13, HIGH);
  delay(1000);
  digitalWrite(13, LOW);
  delay(1000);
}
~~~

### b) Como esses comandos agirão?

- o Arduino possui portas de comunicação chamas **pinos** (digitai ou analógicos), responsáveis por conectar o programa aos componentes físicos.

~~~
pinMode(numero, entrada/saída)
~~~

- exemplos:

~~~
// push button (pino 7)
pinMode(7, INPUT)

// LED (pino 8)
pinMode(8, OUTPUT)

//digitalWrite = saída (HIGH/LOW)
~~~

## 7. [Ambiente de desenvolvimento de Arduino](https://www.youtube.com/watch?v=dFktfWuO0SY)

- acessar o [site oficial do Arduino](https://www.arduino.cc/).
- baixar o Software na aba de mesmo nome.

## 8. [Experimento 1: Acendendo e piscando um LED](https://www.youtube.com/watch?v=kBmgG4gmGaw)

### a) O que será utilizado?

- placa do Arduino.
- uma placa Protoboard.
- um LED (neste caso, vermelho).
- um resistor (neste caso, de 330Ω).
- dois cabos de jumper.

### b) Acendendo um LED:

- no simulador, posicionar os equipamentos e componentes.
- calcular o valor da resistência:
  - a placa trabalha com 5V, e o LED, 2V. Se ligar diretamente o LED na placa, queimará. Por isso é colocado o resistor:
  - cálculo: R (resistência) = V (tensão) / I (corrente) -> R = (5V - 2V) / 20mA ou 0,02A -> R = 3 / 0,02 -> R = 150Ω.
- ligar o catodo do LED ao terra (GND), e o anodo à porta 13.
- ajustar a programação em bloco!

<div align="center">
<img src="./assets/images/acendendo-um-LED.png" width="70%">
<p><em>Acendendo um LED.</em></p><br>

<img src="./assets/images/acendendo-um-LED-programacao.png" width="70%">
<p><em>Programação na IDE, para o exemplo de acender um LED (caso o experimento seja feito fora do simulador, com o equipamento).</em></p><br>
</div>

### c) Piscando um LED:

<div align="center">
<img src="./assets/images/piscando-um-LED.png" width="70%">
<p><em>Piscando um LED.</em></p><br>

<img src="./assets/images/piscando-um-LED-programacao.png" width="70%">
<p><em>Programação na IDE, para o exemplo de piscar um LED (caso o experimento seja feito fora do simulador, com o equipamento).</em></p><br>
</div>

## 9. [Experimento 2: LED com comando](https://www.youtube.com/watch?v=Tzan4_BxH2Y)

### a) O que será utilizado?

- mesmos componentes do exemplo anterior:
  - placa do Arduino.
  - uma placa Protoboard.
  - um LED (neste caso, vermelho).
  - um resistor (neste caso, de 330Ω).
  - dois cabos de jumper e...
- 1 chave tátil ou push button.
- resistor de 10kΩ.
- 3 jumpers.

### b) Experimento:

- tirar o jumper verde do exemplo anterior, e ligá-lo do terra (GND) ao negativo da Protoboard.
- ligar o jumper do negativo da Protoboard ao catodo do LED.
- inserir o push button e o novo resistor, ligá-los ao terra e à porta 7.
- iniciar a programação:
  - criar a variável Botao.
  - selecionar Blocks + Text.
  - criar a programação conforma abaixo.

<div align="center">
<img src="./assets/images/LED-com-comando.png" width="70%">
<p><em>LED com comando/push button.</em></p><br>

<img src="./assets/images/LED-com-comando-programacao.png" width="70%">
<p><em>Programação do LED com comando/push button.</em></p><br>
</div>

---

## Fichário

<p><em>

"Enviar no word, em um único arquivo as imagens dos experimentos 1 e 2 no simulador ou no Arduino, e os códigos programados neste mesmo arquivo, sem compactar. 

- Experimento 1 - Acendendo e piscando um LED
- Experimento 2 - LED com comando"

</p></em>

---

[Voltar ao início!](https://github.com/monicaquintal)