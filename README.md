# Lab01 - Comparación de tecnologías CMOS y TTL

## Integrantes

[Sergio Andrés Bolaños Penagos](https://github.com/sergiosinlimites)
<br>
[Juan José Rincón Monsalve](https://github.com/)
<br>
[Johan Camilo Patiño Mogollon](https://github.com/)


## Informe
# Informe de Práctica I: Electrónica Digital I

## Objetivos

El objetivo de esta práctica es estudiar las características de dispositivos lógicos fabricados en tecnologías TTL y CMOS mediante el análisis teórico de sus especificaciones. Posteriormente, se implementará una operación lógica para observar diferencias en parámetros como tiempo de respuesta, disipación de potencia y fan-out.

## Resumen Teórico

La electrónica digital utiliza diferentes tecnologías para construir circuitos lógicos, y entre las más comunes están las tecnologías **TTL (Transistor-Transistor Logic)** y **CMOS (Complementary Metal-Oxide-Semiconductor)**. Cada tecnología tiene características específicas que afectan el rendimiento y las aplicaciones de los circuitos. En esta práctica se examinan dos negadores:

- **Negador TTL 74LS04**
- **Negador CMOS 74HCT04 compatible TTL**

Estas tecnologías difieren en términos de voltaje de operación, disipación de potencia, tiempos de retardo y capacidad de carga (fan-out), lo que afecta su idoneidad en diferentes aplicaciones electrónicas.

## Circuitos Equivalentes
### Circuito de: 74HCT04

CMOS:<br>
La tecnología CMOS tiene como principio de funcionamiento interno el estar conformada por dos transistores MOSFET, uno de canal N y otro de canal P, los cuales se encuentran complementados, es decir que mientras uno se encuentra activo el otro no. 

Transistor MOSFET canal N:<br>
EL MOSFET de canal N se caracteriza por permitir el paso de corriente cuando el voltaje VGS (Diferencia de potencial entre la puerta y la fuente) es mayor al Voltaje de umbral.
Este es implementado como la conexión entre GND y la salida de la compuerta cuando se encuentra activo.<br>
Transistor MOSFET canal P:<br>
EL MOSFET de canal P se caracteriza por permitir el paso de corriente cuando el voltaje VSG (Diferencia de potencial entre la fuente y la puerta) es mayor al valor absoluto del Voltaje de umbral.
Este es implementado como la conexión entre el voltaje de alimentación y la salida de la compuerta cuando se encuentra activo.

Cuando la entrada está a un voltaje alto, el NMOS se activa (porque V_GS > V_th) y conecta la salida a tierra, lo que da como resultado un cero logico. El PMOS se apaga porque V_GS es demasiado positivo o en otras palabras (V_SG < ∣Vt_h∣). Cuando la entrada está a un voltaje bajo, el PMOS se activa y conecta la salida a VDD (alimentación), mientras que el NMOS se apaga.

CIRCUITO:

 <img src="./Imagenes/74HCT04 circuito.png" width="100%">

 SIMULACIÓN:

  <img src="./Imagenes/74HCT04-SIMULACION.png" width="100%">

#### Circuito equivalente de: 74HCT04
 
AQUI TOCA HACER LAS COMPUERTAS CMOS EN LTSPICE

### Circuito de: 74LS04 


TTL:<br>
La tecnología TTL tiene como principio de funcionamiento interno el estar conformada por un transistor BJT NPN, aunque dependiendo de la configuración se pueden incluir mas componentes. 

Transistor BJT NPN:<br>
EL BJT NPN en un TTL basico se utiliza como interruptor en donde al recibir un 1 logico (Voltaje superior al de umbral) este se activa y se conecta a GND entregando un 0 logico 

En otras configuraciones se puede incluir un segundo transistor NPN (Q2) que cumple la función de "limitador" con el objetivo de evitar que el transistor Q1 (es decir el principal) alcance un voltaje muy elevado.


<b>CIRCUITO:</b>

<img src="./Imagenes/74LS04 circuito.png" alt="VIH CMOS" width="100%">

<b>SIMULACIÓN:</b>

<img src="./Imagenes/74LS04-SIMULACION.png" alt="VIH CMOS" width="100%">

#### Circuito equivalente de: 74LS04

<img src="./Imagenes/NOT-TTL.JPG" width="100%">
 
## Comparación de Dispositivos TTL y CMOS

### Características Generales

| Característica               | TTL (74LS04)                    | CMOS (74HCT04)                  |
|------------------------------|----------------------------------|--------------------------------|
| Voltaje de operación         | 5V                              | 5V                      |
| Rango de temperatura         | 0 °C a 70 °C                   | -40 °C a 85 °C                |
| Tiempo de retardo de propagación | 10 ns | 0-500 ns           |
| Disipación de potencia       | 1 mW - 20 mW por compuerta     | 0.2 mW - 10 mW                 |
| Corriente de salida          | 8 mA | 20 mA mA                         |
| Número de compuertas         | 6 | 6 |
| Número de pines              | 14 | 14 |

### Voltajes de entrada y salida

Cada dispositivo tiene niveles de voltaje de entrada y salida para distinguir entre estados lógicos de "0" y "1". A continuación, se muestran los voltajes requeridos:

| Parámetro                       | TTL (74LS04)                     | CMOS (74HCT04)                 |
|---------------------------------|----------------------------------|-------------------------------|
| **Input High Voltage (VIH)**    | Min 2V | Min 2V |
| **Input Low Voltage (VIL)**     | Máx 0.8V | Máx 0.8V |
| **Output High Voltage (VOH)**   | Mín 2.7V (típico 3.4V) | Mín 4.4 (Típico 4.5V) |
| **Output Low Voltage (VOL)**    | Máx 0.5V (típico 0.35V)| Máx 0.1V |

### Fan-in y Fan-out

El **fan-out** es la cantidad de dispositivos que una puerta lógica puede controlar en su salida sin pérdida de funcionalidad, mientras que el **fan-in** es la cantidad de entradas que puede manejar una puerta sin degradar la señal. Estos parámetros difieren entre TTL y CMOS:

| Característica             | TTL (74LS04)                 | CMOS (74HCT04)                      |
|----------------------------|------------------------------|------------------------------------|
| **Fan-out**                | Hasta 10 puertas TTL         | Más de 50 puertas CMOS             |
| **Fan-in**                 | Limitado a 1-2 entradas      | Número alto de entradas debido a alta impedancia |


### Disipación de Potencia

La disipación de potencia es un parámetro crucial para entender la eficiencia energética de un dispositivo. La tecnología TTL tiene un consumo de energía constante, mientras que la CMOS consume principalmente durante los cambios de estado.

- **TTL (74LS04)**: Disipación de potencia entre 1 mW y 20 mW por compuerta.
- **CMOS (74HCT04)**: Disipación de potencia de 0.2 mW a 10 mW, dependiendo de la frecuencia de operación.
  

## Simulación de circuito ante señales de entrada

Se va a realizar la simulación de ambas compuertas con valores entre los 100Hz y los 1MHz.

### Con 100Hz:
Para HCT:
<img src="./Imagenes/simulacion-100hz.png" width="100%">
Para LS:
<img src="./Imagenes/simulacion-100Hz-ls.png" width="100%">

### Con 1000Hz:
Para HCT:
<img src="./Imagenes/simulacion-1000Hz-hct.png" width="100%">

Para LS:
<img src="./Imagenes/simulacion-1000Hz-ls.png" width="100%">

### Con 10kHz:
Para HCT:
<img src="./Imagenes/simulacion-10khz-hct.png" width="100%">

Para LS:
<img src="./Imagenes/simulacion-10khz-ls.png" width="100%">

### Con 100kHz:
Para HCT:
<img src="./Imagenes/simulacion-100khz-hct.png" width="100%">

Para LS:
<img src="./Imagenes/simulacion-100khz-ls.png" width="100%">

### Con 1MHz:
Para HCT:
<img src="./Imagenes/simulacion-1mhz-hct.png" width="100%">

Para LS:
<img src="./Imagenes/simulacion-1mhz-ls.png" width="100%">

### Con 10MHz:
Para HCT:
<img src="./Imagenes/simulacion-10mhz-hct.png" width="100%">

Para LS:
<img src="./Imagenes/simulacion-10mhz-ls.png" width="100%">


##  Funciones de transferencias

Las funciones de transferencia para los circuitos montados fueron las siguientes:

* A partir de esta curva, determinar $V_{IH}​$, $V_{IL}​$, $V_{OH}$, $V_{OL}$.

Para HCT:
<img src="./Imagenes/ft-hct-1khz.png" width="100%">

V<sub>IL</sub> = 2,513 V

V<sub>IH</sub> = 2,480 V

V<sub>OH</sub> = 4,850 V

V<sub>OL</sub> = 0,050 V

Para LS:
<img src="./Imagenes/ft-ls-1khz.png" width="100%">


V<sub>IL</sub> = 2,503 V 

V<sub>IH</sub> = 2,487 V

V<sub>OH</sub> = 4,850 V

V<sub>OL</sub> = 0,050 V

## Estimación de tiempos de conmutación:
* Obtenier tiempos de subida ($t_r$), bajada ($t_f$) y retardo ($t_{PLH}$, $t_{PHL}$ y $t_{P}$) para cada tecnología.

##Tiempo de Bajada y Subida TTL

Se desarrollaron instrucciones en LTSpice para calcular estos valores automaticamente. Los resultados son los siguiente

<img src="./Imagenes/Tiempos para compuertas.png" width="100%">


## Estimación del consumo de potencia
**Estimar teóricamente y en simulación la potencia estática y la potencia dinámica de cada dispositivo durante la operación.**

La potencia estática se puede calcular como 
$P_{s}$ $=$ $V_{in}$*$I_{in}$

Mientras que la potencia dinámica se puede calcular como:

$P_{d}=C_{L}*V_{in}^2*f$

Donde $C_{L}$ es un parámetro dependiente de la cantidad de compuertas y su tipo, y $f$ está asociado a la frecuencia.
Este cálculo sirve principalmente para compuerta CMOS, ya que para compuertas TTL, se añade un término asociado a la corriente de cortocircuito media por flanco.


<img src="./Imagenes/potencia-estatica-dinamica.png" width="100%">

La potencia estática se puede ver en la gráfica anterior como la que se queda al realizar la conmutación después del pico inicial.
Para el TTL es de aproximadamente 36.4uW, mientras que el de CMOS es de aproximadamente 25uW.
Para el caso de la potencia dinámica, para la tecnología TTL da un valor de aproximadamente 38.6uW, mientras que para CMOS da un valor de }30uW.

**Analizar cómo varía el consumo de potencia en función de la frecuencia de operación y el tipo de tecnología (TTL vs CMOS), considerando las características de cada tecnología.**

Como se puede ver según la ecuación, en general, la potencia dinámica aumenta con respecto a la frecuencia en que opera el circuito. Esto se puede ver para ambos por ejemplo, cambiando la frecuencia de 1kHz que es la que se utilizó en la gráfica de potencia anterior a 100kHz.

Como se puede ver, el pico de potencia que llega el TTL es de aproximadamente 258uW, y para el CMOS es de aproximadamente 525uW.

<img src="./Imagenes/potencia-estatica-dinamica-100khz.png" width="100%">


## Circuito implementado
Para esta práctica los circuitos implementados fueron los siguiente:

<img src="./Imagenes/CIRCUITOS-UNIDOS.png"  width="100%">


Para el caso del CMOS, basta con cambiar la compuerta, el resto del montaje permanece igual.
Estos circuito son compuertas negadoras, las cuales poseen una señal cuadrada como entrada, está constituido por dos LEDS que permiten apreciar de una manera más visual el comportamiento de dicho circuito, y las resistencias utilizadas se escogieron con el fin de evitar pérdidas en la amplitud de la señal de salida.

Las simulaciones para esta sección con el TTL fue la siguiente:

<img src="./Imagenes/Entrada-Salida HCT.png" width="100%">

Mientras que con el CMOS fue la siguiente:

<img src="./Imagenes/Entrada-Salida LS.png" width="100%">

## Procedimiento

### Parte 1
### Graficas del osciloscopio

**CMOS:**

<img src="./Imagenes/CMOSFT.jpg" width="100%">

<img src="./Imagenes/CMOSdatos.jpg" width="100%">


### Graficas del osciloscopio

**TTL:**

<img src="./Imagenes/TTLFT.jpg" width="100%">

<img src="./Imagenes/TTLDatos.jpg" width="100%">



**Los datos experimentales obtenido del CMOS se encuentran en las siguientes tablas:**

### Parámetros característicos del inversor (CMOS)

**Los datos experimentales obtenido del CMOS se encuentran en la siguiente tabla:**
| Parámetro      | Valor estimado                  |
|----------------|----------------------------------|
| VIL         | **1.2 V**  |
| VIH         | **3.0 V**  |
| VOL         | **0.0 V**                        |
| VOH         | **5.060 V**                      |
| tr (Rise)   | **0.412 ms**                     |
| tf (Fall)   | **0.412 ms**                     |


## Parámetros característicos del inversor (TTL)

| Parámetro      | Valor estimado     |
|---------------|---------------------|
| V_IL`         | **1.4 V**          |
| V_IH         | **2.6 V**          |
| V_OL         | **78 mV**           |
| V_OH         | **5.00 V**          |
| t_r (Rise)   | **0.408 ms**        |
| t_f (Fall)    | **0.410 ms**        |



### Parte 2



<img src="./Imagenes/parte2-1.jpg" width="100%">

1. **Determinar el fan-in y fan-out de cada uno de los dispositivos.**

**Fan-in_TTL = 1**

I_OL = 8 mA
I_IL = 0.4 mA

I_OH = 0.4 mA
I_IH = 20 µA

Fan-out_bajo = I_OL / I_IL = 8 mA / 0.4 mA = 20
Fan-out_alto = I_OH / I_IH = 0.4 mA / 20 µA = 20

Fan-out_TTL = min(20, 20) = 20

2. **Determinar el consumo de potencia de cada dispositivo.**
 
### CMOS

Vcc = 5 V
Icc = 1 µA 

P_CMOS_por_inversor = 5 V × 1 µA = 5 µW
P_CMOS_total (6 inversores) = 6 × 5 µW = 30 µW

### TTL 

Vcc = 5 V
Icc = 2 mA 

P_TTL_por_inversor = 5 V × 2 mA = 10 mW
P_TTL_total (6 inversores) = 6 × 10 mW = 60 mW


3. **Proponer e implementar un circuito de entrada y de salida para cada uno de los dispositivos teniendo en cuenta los parámetros de cada tecnología para observar el comportamiento del mismo.**





### Parte 3

###Oscilador en anillo basado en la compuerta NOT

Los osciladores en anillo que utilizan compuertas NOT se distinguen por su capacidad para generar señales oscilatorias de alta frecuencia sin requerir una señal de entrada externa. Este tipo de oscilador se construye conectando un número impar de inversores en un lazo cerrado.

Su principio de funcionamiento se basa en la realimentación que se produce al unir la salida del último inversor con la entrada del primero. Debido al retardo inherente en la propagación de señal a través de cada compuerta, el circuito no puede estabilizarse en un único estado lógico. Esto provoca una conmutación continua, generando así la oscilación.

#### Oscilador en anillo con 3 compuertas NOT
<img src="./Imagenes/Circuito Anillo 3.png" alt="VIH CMOS" width="50%">
<img src="./Imagenes/Esquematico_Anillo_3.png" alt="VIH CMOS" width="50%">
<img src="./Imagenes/Osciloscopio Anillo 3.jpg" alt="VIH CMOS" width="50%">

#### Oscilador en anillo con 5 compuertas NOT
<img src="./Imagenes/Circuito Anillo 5.png" alt="VIH CMOS" width="50%">
<img src="./Imagenes/Esquematico_Anillo_5.png" alt="VIH CMOS" width="50%">
<img src="./Imagenes/Osciloscopio Anillo 5.jpg" alt="VIH CMOS" width="50%">

####Análisis Osciladores

En esta práctica se implementó un oscilador en anillo compuesto por tres y 5 inversores, tanto en un entorno de simulación (LTspice) como de forma experimental en laboratorio. El objetivo fue observar el comportamiento oscilatorio del sistema y comparar los resultados obtenidos.

En la simulación con LTspice, la señal generada no fue una onda cuadrada ideal como se podría esperar teóricamente. En su lugar, se observó una señal oscilatoria de forma irregular, con picos de diferente amplitud y una especie de modulación superpuesta. Esta distorsión puede deberse a las características internas del modelo de las compuertas utilizadas, el tipo de simulación transitoria, o incluso a la ausencia de una carga adecuada o de componentes adicionales como resistencias de polarización.

Por otro lado, en la implementación práctica, si bien tampoco se obtuvo una onda perfectamente cuadrada, la señal resultó ser más estable y reconocible en cuanto a su patrón de conmutación, mostrando la típica alternancia de un oscilador en anillo. Sin embargo, las amplitudes medidas en laboratorio fueron considerablemente más bajas que las obtenidas en la simulación. Esto es coherente con las limitaciones reales de los componentes físicos, como el retardo de propagación de las compuertas, la capacitancia parasitaria, y las condiciones de alimentación.

Aunque ambos entornos confirmaron el comportamiento oscilatorio básico, ni la forma ni los valores de la señal coincidieron plenamente. La simulación produjo una señal más rápida pero con distorsión, mientras que la implementación real ofreció una señal más definida pero con una tensionmenor. Esto pone de manifiesto las diferencias inherentes entre el comportamiento idealizado en simuladores y las condiciones reales en hardware.



