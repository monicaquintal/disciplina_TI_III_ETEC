<div align="center">
<a href="https://github.com/monicaquintal" target="_blank"><img align="left" height="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/arduino/arduino-original-wordmark.svg" /></a>
</a>
<h1>Estudando Sistemas Embarcados - Arduino.</h1>
<p>Tecnologia da Informação III - ETEC</p>
</div>

<div id="agendas14e15">
<h2>Agendas 14 e 15: Módulo III - Sensores.</h2>
</div>

## 1. [Sensores](https://youtu.be/tnicaP18ZVg)

### a) `Sensor LDR` (Light Dependent Resistor):

- é um Resistor Dependente de Luz ou Fotoresistência.
- componente eletrônico passivo do tipo resistor variável.
- é um resistor cuja resistência varia conforme a intensidade da luz (iluminamento) que incide sobre ele.
    - quanto maior a luminosidade, menor a resistência.
    - a resistência é inversamente proporcional à luminosidade.
    - uma resistência deve **sempre** ser colocada em paralelo a ele, porque se não tiver e sua resistência tender a 0, pode gerar um curto (portanto, devemos limita a corrente)!

### b) `Sensor Infravermelho`:

- existem sensores de infravermelho ativos e passivos.
    - ***ativo***: composto pot um emissor de luz infravermelha (fotodiodo/LED) e um receptor (fototransistor), que reage a essa luz.
    - ***passivo***: não emite luz infravermelha, apenas capta esse tipo de luz no ambiente.

### c) `Termistor NTC e PTC`:

- a resistência elétrica dos termistores pode variar tanto de forma proporcional ou inversa com o aumento da temperatura ao qual o sensor for exposto.
- devido a essa característica, é feita uma classificação dos termistores, sendo:
    - **NTC**: Negative Temperature Coeficiente (quanto maior a temperatura, **menor** a resistência).
    - **PTC**: Positive Temperature Coeficiente (quanto maior a temperatura, **maior** a resistência).

## 2. [Display de 7 segmentos](https://youtu.be/v8StUbkRnc4)

- também chamado de "LED de 7 segmentos".
- é um display constituído por 7 LEDs retangulares dispostos de forma que, com uma combinação de LEDs acesos e apagados, possa ser mostrada informação alfanumérica, não só em decimal, como também em binário e hexadecimal.
- há dois tipos de display:

### a) ***Ânodo comum***:

- ânodo comum com todos os ânodos do diodo emissor de luz (LED) conectados juntos.
- estes necessitam de um nível lógico 0 para acender.
- conectar o ânodo comum no `+Vcc` (pinos 3 e 8); entradas a a f.

### b) ***Cátodo comum***:

- cátodo comum com todos os cátodos do diodo emissor de luz (LED) conectados juntos.
- estes necessitam de um nível lógico 1 para acender.
- conectar o cátodo comum no `GND`

## 3. Display de LCD (Liquid Crystal Display):

- representam uma forma prática e de baixo custo para exibir informações.
- apresentam os seguintes pinos:
    - VSS: 0V (terra).
    - VDD ou VCC: 3.3V ou 5V (valores típicos).
    - Vo ou Ve: tensão de contraste.
    - RS: pino de seleção de envio de comando ou dados.
    - R/W: pino de leitura ou escrita de dados.
    - E: habilita o display para leitura/escrita.
    - D0~D7: 8 pinos de dados.
    - Backlight Anodo: 3.3V ou 5V (valores típicos). 
    - Backlight Catodo: 0V (terra).

## 4. Experimentos:

### a) [Controle remoto](https://youtu.be/nhveczTZByk).
### b) [Caminho de LED com sensor de luz](https://youtu.be/God0LxaedHI).
### c) [Display de 7 segmentos com sensor de boia](https://youtu.be/vtG8IZ438G8).

---

## Fichário

- Vamos debater com os colegas da sala sobre IoT - Internet das Coisas?
- Pesquise na internet o uso dos elementos/componentes de arduino para viabilizar os projetos baseados em IOT. Descrevam exemplos de como poderiam ser utilizados os projetos de arduino dentro desse conceito, por exemplo, o uso destes em eletrodomésticos conectados na internet para serem programados a realizarem uma tarefa, sistemas de seguranca controlados por uma rede, dentre outros.
- Aproveite este momento e compartilhe com os colegas a sua pesquisa.

---

[Voltar ao início!](https://github.com/monicaquintal)
