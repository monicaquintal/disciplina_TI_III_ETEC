<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original-wordmark.svg" /></a>
</a>
<h1>Estudando Sistemas Embarcados - Arduino.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agendas14e15">
<h2>Agenda 16: Módulo IV - Motores.</h2>
</div>

## 1. [Motores elétricos](https://www.youtube.com/watch?v=JWkfyPr82PQ&t=4s)

### a) `Motor de Corrente Contínua` (CC):

- converte energia elétrica em energia mecânica, como qualquer motor.
- possui uma característica individualizada: deve ser alimentado com tensão contínua, que pode vir de pilhas e baterias (no caso de pequenos motores) ou de uma rede alternada após retificação (no caso de motores maiores).
- principais componentes:
  - ***estrator***: contém um enrolamento (chamado campo), que é alimentado diretamente por uma fonte de tensão contínua. No caso de pequenos motores, o estrator pode ser um simples ímã permanente.
  - ***rotor***: contém um enrolamento (chamado armadura), que é alimentado por uma fonte de tnsão contínua através do comutador e escovas de grafite.
  - ***comutador***: dispositivo mecânico (tubo de cobre axialmente segmentado) no qual estão conectados os terminais de espirais da armadura, e cujo papel é inverter sistematicamente o sentido ca corrente contínua que circula na armadura.

### b) `Experimentos`:

- [Experimento: Motor](https://youtu.be/GeriN5P5NV8)
- [Experimento: Motor com potenciômetro](https://youtu.be/TUqSKYsBw7M)

---

## Fichário

Entregar o certificado de conclusão do Curso de Arduino!

<details>
<summary>Avaliação</summary>
<br>

Desenvolver um projeto, utilizando o Arduino UNO que respeite as seguintes condições:
1. acionar um alarme sonoro e luminoso quando a temperatura do ambiente ultrapassar 30°C.
2. devemos utilizar um sensor NTC para realizar a leitura da temperatura.
3. o alarme luminoso será realizado através de um LED, ou seja, toda vez que a temperatura ultrapassar 30°C, o LED acende.
4. o alarme sonoro deverá ser realizado por um buzzer, ou seja, toda vez que a temperatura ultrapassar 30°C, o buzzer acionará.

> Levando em consideração o projeto e o hardware do Arduino UNO, responda se a afirmação é Verdadeira (V) ou Falsa (F).

1. Utilizamos para trazer a informação de temperatura do NTC uma entrada digital.
> Falso.
Parabéns, sua reposta está correta, pois utilizamos para trazer a informação de temperatura do NTC uma entrada digital
A resposta correta é 'Falso'.

2. Para acionar o LED podemos utilizar qualquer pino de saída digital, como por exemplo, o pino 13.
> Verdadeiro.
Parabéns, sua reposta está correta, pois para acionar o LED podemos utilizar qualquer pino de saída digital, como por exemplo o pino 13.
A resposta correta é 'Verdadeiro'.

3. Para acionar o buzzer numa certa frequência podemos utilizar qualquer pino de saída digital, como por exemplo, o pino 8.
> Falso.
Parabéns, sua reposta está correta, pois para acionar o buzzer numa certa frequência podemos utilizar qualquer pino de saída digital, como por exemplo o pino 8.
A resposta correta é 'Falso'.

4. Temos que inserir um resistor em série com o LED para limitar a corrente elétrica.
> Verdadeiro.
Parabéns, sua reposta está correta, pois temos que inserir um resistor em série com o led para limitar a corrente elétrica.
A resposta correta é 'Verdadeiro'.

5. Quando desejamos ler a tensão no sensor de temperatura do projeto proposto, devemos utilizar o seguinte comando:
> analogRead
Parabéns, sua reposta está correta, pois quando desejamos ler a tensão no sensor de temperatura do projeto proposto, devemos utilizar o comando analogRead.

6. No projeto proposto devemos acionar o Led quando a temperatura ultrapassar o limite de 30°C. O comando para acender o Led é denominado de:
> digitalWrite 
Parabéns, sua reposta está correta, pois no projeto proposto devemos acionar o Led quando a temperatura ultrapassar o limite de 30°C. O comando para acender o Led é denominado digitalWrite.

7. No projeto de acionamento do alarme sonoro, temos que enviar uma frequência para acionar o buzzer. O comando utilizado para esse acionamento é:
> tone
Parabéns, sua reposta está correta, pois no projeto de acionamento do alarme sonoro, temos que enviar uma frequência para acionar o buzzer. O comando utilizado para esse acionamento é tone.

8. Nesse projeto devemos criar uma situação que verifique se o alarme vai ser acionado ou não. O comando que produz essa condição é:
> if
Parabéns, sua reposta está correta, pois nesse projeto devemos criar uma situação que verifique se o alarme vai ser acionado ou não. O comando que produz essa condição é if.

9. Levando em consideração as linhas de código do programa do Arduino UNO, preencha as lacunas:

int le = 0;
int temp = 0;
const int led = 12;
const int buzzer = 5;

void _______ ()
{
   pinMode ( led , _______ );
   pinMode ( buzzer , _______ );
}
void loop()
{
   le = _______(A0);
   temp  =  ( le * 0,064 ) + 8;
   _______ ( temp > 30 )
   {
      digitalWrite ( led , _______ );
      _______ ( 5, 1000, 1000 );
   } else
   {
      digitalWrite ( led , _______ );
      _______ ( 5, 0000, 1000 );

   }
}

> setup, OUTPUT, OUTPUT, analogRead, if, HIGH, tone, LOW, tone

</details>

---

[Voltar ao início!](https://github.com/monicaquintal)