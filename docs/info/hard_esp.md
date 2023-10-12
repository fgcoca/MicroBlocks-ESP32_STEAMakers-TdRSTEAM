# <FONT COLOR=#8B008B>Hardware de la ESP32 STEAMakers</font>

## <FONT COLOR=#007575>**Generalidades sobre ESP32**</font>
En este apartado vamos a realizar algunas consideraciones sobre los siguientes aspectos de las placas ESP32:

* Pines
* Entradas analógicas
* Entradas y salidas digitales
* Salidas PWM en ESP32

### <FONT COLOR=#AA0000>Pines en ESP32</font>
En general los pines en ESP32 son de tipo GPIO (General Purpose Input/Output, Entrada/Salida de Propósito General). Algunos pines GPIO pueden tener un comportamiento no esperado durante el arranque del sistema o en el reinicio del mismo. Esto se debe a que durante el arranque de la placa ESP32 se deben realizar procesos internos que ponen en alto ciertos pines o incluso hacen que emitan señales, y esto puede provocar esos efectos no deseados.

El pin GPIO1 del microcontrolador es el pin Tx del puerto UART de depuración y cuando la placa arranca, se reinicia o cuando nosotros hacemos uso del puerto serie, este pin emite datos. Por este motivo es un pin que no conviene usar como entrada o salida.

El GPIO3 tiene un problema similar al GPIO1 ya que se trata del pin Rx del micocontrolador.

Los pines GPIO34, GPIO35, GPIO36 y GPIO39 solamente pueden utilizarse como entradas porque no disponen de resistencia pull-up.

### <FONT COLOR=#AA0000>Entradas analógicas</font>
Las señales analógicas son las que pueden tomar diferentes valores de tensión en un determinado periodo de tiempo, siendo su forma mas característica la senoidal. Cuando hablamos de entradas analógicas estamos hablando de pines del microcontrolador que pueden leer esas señales. En el caso de ESP32 todo son pines GPIO y por lo tanto se requiere de un conversor analógico a digital que sea capaz de transformar esas señales analógicas en digitales. El chip ESP32 que monta la placa ESP32 STEAMakers dispone de 2 convertidores Digital-Analógico (DAC) de 8 bits y 16 convertidores Analógico-Digital (ADC) de 12 bits. Estos conversores se asocian a los pines IO1 hasta IO20.

La resolución de los conversores ADC es de 12 bits (2^12 = 4096) por lo que la transformación de los valores digitales va a ser de mucha precisión. Pero cuidado con el uso de estas entradas, porque en realidad su comportamiento es que están leyendo valores digitales y no valores analógicos por lo que cambios de valores analógicos muy pequeños pueden no ser detectados.

Los canales ADC se dividen en dos puertos denominados ADC1 y ADC2. Las entradas analógicas del puerto ADC2 solamente las podemos usar como tales si el controlador WiFi no ha sido iniciado, ya que este puerto es el que utiliza el controlador del WiFi que integra la placa.

### <FONT COLOR=#AA0000>Entradas y salidas digitales</font>
Una señal digital solamente puede tomar dos valores o estados lógicos, alto y bajo, High y Low, 0 y 1 siendo su representación característica una onda cuadrada. El estado bajo se asocia a cero voltios y el estado alto a 3.3V (5V en el caso de placa tipo UNO).

Las entradas permiten recibir señales con los valores digitales descritos, como por ejemplo leer el estado de un pulsador.

Debemos saber que ESP32 lleva unas resistencias de pull-up (1) o pull-down (0) que nos permiten establecer el estado que tiene la entrada cuando está en reposo. Estas resistencias están disponibles en todos los pines excepto el 34 y 39. Estas resistencias internas se pueden activar por código.

Las salidas digitales nos van a servir para realizar acciones sobre los elementos conectadas en ellas, como por ejemplo encender un LED o activar un relé.

En principio todos los pines que se pueden utilizar como salida en ESP32 pueden usarse con PWM excepto los pines que no disponen de resistencia de pull-up interna.

## <FONT COLOR=#007575>**ESP32 Plus STEAMakers**</font>
La placa ESP32 Plus STEAMakers nos ofrece una gran cantidad de prestaciones al estar basada en un microcontrolador de 32 bits con conectividad WiFi y Bluetooth integradas en la propia placa y también un zócalo para tarjetas µSD para el almacenamiento de datos. También dispone de conexiones para todas las entradas y salidas con posibilidad de tener la alimentación adjunta y puertos de expansión I2C para poder conectar diferentes dispositivos directamente en la placa. En la figura siguiente vemos su aspecto.

<center>

![Aspecto de la placa ESP32 Plus STEAMakers](../img/info/Aspecto_STEAMakers.png)  
*Aspecto de la placa ESP32 Plus STEAMakers*

</center>

La placa está basada en el microcontrolador ESP32-WROOM-32 y sus principales especificaciones técnicas son:

* Microcontrolador Tensilica Xtensa 32-bit LX6 a 160MHz.
* Conectividad WiFi 802.11 b/g/n/e/i.
* Conectividad Bluetooth 4.2 y modo BLE.
* Zócalo para tarjetas µSD.
* 14 entradas y salidas digitales con alimentación.
* Conector serie hembra con alimentación.
* Conector I2C para conectar hasta 5 dispositivos a la vez sobre la misma placa.
* Conector hembra I2C para conexión de una pantalla OLED.
* Botón de Reset.
* Conector de 5V
* Conector de 3.3V
* Interruptor 3.3-5V para cambiar entre estas dos tensiones en algunos pines de alimentación.
* Entradas y salidas analógicas.
* Sensor Hall y de temperatura integrado.
* 2 convertidores Digital-Analógico (DAC) de 8 bits.
* 16 convertidores Analógico-Digital (ADC) de 12 bits.
* 16 canales PWM.
* 2 UART.
* 2 canales I2C.
* 4 canales SPI.
* 448Kb ROM.
* 520 KB SRAM.
* 8KB+8KB SRAM en RTC.
* 1kbit eFUSE.
* 512 bytes Memoria Flash (EEPROM).
* 10 sensores táctiles.
* 4 temporizadores internos de 64 bits.

En la ESP32 ST$EAMakers no están disponibles todas las características del controlador ESP-WROOM-32, ya que algunos pines tienen funciones dobles y se utilizan en la placa de forma específica (como, por ejemplo, para controlar la tarjeta SD). Pero la mayoría de funciones se pueden utilizar, además de disponer la placa ESP32 Plus STEAMakers de una mejor conexión de elementos debido a los pines para conectores tipo Dupont de entrada y salida, de I2C y de alimentación. Además, algunos pines de alimentación pueden cambiar su valor (3,3V o 5V) mediante un interruptor en función de nuestras necesidades.

En la figura siguiente vemos un momento del [video descriptivo de la placa ESP32 STEAMakers](https://www.youtube.com/watch?v=MQjIEI7I4ik&list=PL1pKD-Bz2QBAgfy580m8OaQ2Z60v6DOhC) que se aloja en el [canal Youtube de ArduinoBlocks](https://www.youtube.com/c/ArduinoBlocks).

<center>

![Comparativa de la ESP32 STEAMakers con otras placas populares](../img/info/comparativa.png)  
*Comparativa de la ESP32 STEAMakers con otras placas populares*

</center>

En la figura siguiente vemos los elementos que componen la placa ESP32 Plus STEAMakers:

<center>

![Elementos en la placa ESP32 Plus STEAMakers](../img/info/elementos.png)  
*Elementos en la placa ESP32 Plus STEAMakers*

</center>

### <FONT COLOR=#AA0000>Relación conexiones tipo UNO</font>
Las conexiones de la placa Imagina TDR STEAM con la placa ESP32 Plus STEAMakers son las mismas que si utilizamos cualquier placa compatible con Arduino UNO. En la tabla siguiente se establece la relación entre los elementos de la placa Imagina TdR STEAM y las conexiones de una placa ESP32 Plus STEAMakers.

<center>

| Pin UNO | Uso en TdR STEAM | Descripción |
|:|---|---|
| D0 | Rx | Pin de recepción Bluetooth y WiFi |
| D1 | Tx | Pin de transmisión Bluetooth y WiFi |
| D2 | Pulsador SW1 | Entrada digital |
| D3 | Conector para entrada/salida digital externa | Entrada/salida digital |
| D4 | Sensor de Temperatura y Humedad DHT11 | Entrada digital |
| D5 | Conector para entrada/salida digital externa | Entrada/salida digital |
| D6 | Color rojo del LED RGB | Salida digital |
| D7 | Pulsador SW2 | Entrada digital |
| D8 | Zumbador o buzzer | Salida digital |
| D9 | Color verde del LED RGB | Salida digital |
| D10 | Color azul del LED RGB | Salida digital |
| D11 | Sensor IR | Entrada digital |
| D12 | LED rojo | Salida digital |
| D13 | LED azul | Salida digital |
| A0 | Potenciómetro | Entrada analógica |
| A1 | Sensor de luz (LDR) | Entrada analógica |
| A2 | Sensor de temperatura (LM35) | Entrada analógica |
| A3 | Conector para entrada analógica externa | Entrada analógica |
| A4 | SDA (Serial DAta.) | Datos I2C |
| A5 | SCL (Serial CLock) | Señal de reloj I2C |

</center>

### <FONT COLOR=#AA0000>Compatibilidad y descripción de pines ESP32 STEAMakers</font>
**Importante**: Todos los pines IOxx son entradas y salidas digitales, algunas con más funciones. Utilizando la comunicación WiFi no funciona el ADC2.

En la tabla siguiente tenemos relacionados todos los pines entre los tipos de placas UNO, Imagina TdR STEAM y ESP32 STEAMakers.

<center>

| UNO | TdR STEAM | ESP32 |||
|:|---|---|---|---|
| Pin | Función | Pin | Función | Ampliación |
| D0 | Rx | IO03 | Rx | UART 0 RX |
| D1 | Tx | IO01 | Tx | UART 0 TX |
| D2 | Pulsador SW1 | IO26 | ADC2 CH9 | DAC2 |
| D3 | Libre | IO25 | ADC2 CH8 | DAC1 |
| D4 | DHT11 | IO17 | | UART 2 TX |
| D5 | Libre | IO16 | | UART 2 RX |
| D6 | Color rojo del LED RGB | IO27 | ADC2 CH7 | ADC2-7 / TOUCH7 |
| D7 | Pulsador SW2 | IO14 | ADC2 CH6 | ADC2-6 / TOUCH6 |
| D8 | Zumbador o buzzer | IO12 | ADC2 CH5 | ADC2-5 / TOUCH5 |
| D9 | Color verde del LED RGB | IO13 | ADC2 CH4 | ADC2-4 / TOUCH4 |
| D10 | Color azul del LED RGB | IO05 | | VSPI CSO |
| D11 | Sensor IR | IO23 | |  VSPI MOSI |
| D12 | LED rojo | IO19 | |  VSPI MISO |
| D13 | LED azul | IO18 | |  VSPI CLK |
| GND |  | GND |  | |
| AREF | | Reset | |
| SDA | I2C | IO21 | |
| SCL | I2C | IO22 | |
| A0 | Potenciómetro | IO02 | ADC2 CH2 | |
| A1 | Sensor de luz (LDR) | IO04 | ADC2 CH0 | |
| A2 | Sensor de temperatura (LM35) |IO36 | ADC1 CH0 | |
| A3 | Libre | IO34 | ADC1 CH6 | |
| A4 | I2C | IO38 | | |
| A5 | I2C | IO39 | ADC1 CH3 | |
| VIN | | VIN | |
| GND |  | GND |  | |
| GND |  | GND |  | |
| 5V |  | 5V |  | |
| 3.3V |  | 3.3V | | |
| RST | | Reset | | |
| 5V |  | 5V |  | |
| | | IO00 | ¡ No conectar ! | |
| - | | IO32 | D0 - uSD | |
| - | | IO15 | CLK - uSD | |
| - | | IO33 | CMD - uSD | |
| - | | IO35 | IOUT | Medidor de corriente |
| - | | IO37 | VOUT |  Medidor de tensión |

</center>
