<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original-wordmark.svg" /></a>
</a>
<h1>Estudando Sistemas Embarcados - Arduino.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agenda10">
<h2>Agenda 11: Módulo II - Chaveamento.</h2>
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

### b) 






---

[Voltar ao início!](https://github.com/monicaquintal)