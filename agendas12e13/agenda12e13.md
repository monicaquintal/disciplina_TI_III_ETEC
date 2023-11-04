<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original-wordmark.svg" /></a>
</a>
<h1>Estudando Sistemas Embarcados - Arduino.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agendas12e13">
<h2>Agendas 12 e 13: Módulo II - Chaveamento.</h2>
</div>

## 1. Buzzer e Push Button

### a) Buzzer:
- componente eletrônico.
- composto por 2 camadas de metal e uma terceira camada interna de cristal piezoelétrico.
- esse elemento recebe uma fonte de energia e, através dela, emite uma frequência sonora.
- no circuito, geralmente há uma fonte (VF), uma resistência (R) e um Buzzer. 
  - Resistência = (tensão da fonte - tensão do buzzer) / corrente do buzzer.

### b) Push Button:
- é um botão de pressão elétrico.
- tem o mesmo funcionamento que o interruptor, fechando ou abrindo o circuito.
- a principal diferença em relação ao interruptor é:
  - a força para **acionar um botão** é sempre exercida no mesmo sentido.
  - a força para **acionar um interruptor** varia em função do estado atual e do estado pretendido.

## 2. Estruturas de decisão

### a) Desvio condicional:
- permite que você construa uma sequência de instruções, onde cada instrução ocorrerá dependendo de uma ação específica (condição verdadeira ou falsa).
- o bloco para o caso de a condição ser F é opcional.
- é possível utilizar encadeamento de if/else.
- sintaxe na linguagem do Arduino:

~~~
if (condição)
{
  instruções;
}
else
{
  instruções;
}
~~~

- exemplo:

~~~
if (x >= 10)
{
  digitalWrite(ledPin, HIGH);
}
else 
{
  digitalWrite(ledPin, LOW);
}
~~~

## 3. Estruturas de repetição (vetores e comandos de repetição)

### a) Vetor:
- é um tipo de agregação de valor em variável.
- é uma variáxel indexada com múltiplos espaços de armazenamento.
- o primeiro índice do vetor é de n°. 0. 
- sintaxe:

~~~
int vetor [quantidade de espaços];
~~~

- para atribuir valores:

~~~
vetor[0] = 1;
vetor[1] = 2;
vetor[2] = 3;
vetor[3] = 4;
vetor[4] = 5;

// ou

int vetor[] = {1, 2, 3, 4, 5};
~~~

### b) Comando de repetição: `FOR`/PARA
- utilizadas para automatizar instruções que devem ser repetidas por um determinado número de vezes.
- sintaxe:

~~~
// for (valor inicial, condição, contador)

for (x = 1; x <= 10; x = x + 1)
{
  bloco de comandos;
}
~~~

- no arduino: 

~~~
int vetorled[] = {8, 9, 10, 11, 12};
int i;

void setup()
{
  for (i = 0; i < 5; i++) 
  {
    pinMode(vetorled[i], OUTPUT);
  }
}

void loop() 
{
  for (i = 0; i < 5; i++)
  {
    digitalWrite(vetorled[i], HIGH);
    delay(1000);
  }
}
~~~

## 4. Experimentos

### a) Experimento 3 - Semáforo.
- serão necessários: placa arduino, protoboard, 3 resistores, 3 leds (vermelho, verde e amarelo) e 7 cabos jumper.

~~~
void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
}

void loop()
{
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(LED_BUILTIN, LOW);
  digitalWrite(12, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(12, LOW);
  digitalWrite(11, HIGH);
  delay(1000); // Wait for 1000 millisecond(s)
  digitalWrite(11, LOW);
}
~~~

### b) Experimento 4 - Piano.
- serão necessários: placa arduino, protoboard, 4 push buttons, 4 LEDs, buzzer.

~~~
const int led4=13;
const int led3=12;
const int led2=11;
const int led1=10;
const int ch1=6;
const int ch2=7;
const int ch3=8;
const int ch4=9;
const int tom=5;

void setup() {
  pinMode (led1, OUTPUT);
  pinMode (led2, OUTPUT);
  pinMode (led3, OUTPUT);
  pinMode (led4, OUTPUT);
  pinMode (ch1, INPUT);
  pinMode (ch2, INPUT);
  pinMode (ch3, INPUT);
  pinMode (ch4, INPUT);
}

void loop() {
  if(digitalRead(ch1) == HIGH)
  {
    tone (tom,600,100);
    digitalWrite(led1, HIGH);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  }
  if(digitalRead(ch2) == HIGH)
  {
    tone (tom,650,100);
    digitalWrite(led1, LOW);
    digitalWrite(led2, HIGH);
    digitalWrite(led3, LOW);
    digitalWrite(led4, LOW);
  }
  if(digitalRead(ch3) == HIGH)
  {
    tone (tom,700,100);
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, HIGH);
    digitalWrite(led4, LOW);
  }
  if(digitalRead(ch4) == HIGH)
  {
    tone (tom,750,100);
    digitalWrite(led1, LOW);
    digitalWrite(led2, LOW);
    digitalWrite(led3, LOW);
    digitalWrite(led4, HIGH);
  }    
}
~~~

---

[Voltar ao início!](https://github.com/monicaquintal)