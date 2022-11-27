# Game//Cat ::: Revisión R3 :: Versión 3.50

![](https://github.com/trunksx64/GAME_CAT_R3_KICAD/blob/main/Images/front.png)

## Razón de Ser e Inspiración

Este Control se basa en la Idea Original del Game//Cat Version R2, el cual a su vez se inspira en el diseño del joystick y botones del Arduino Esplora. El primer Control se implemento para ser usado como parametrizador y las siguientes revisiones se presento como Tesis de Grado de Especialización de Instrumentación Industrial que curse. Se Utilizo principalmente como Herramienta de Programación para Tarjeta de Control de Ascensores Usando Un Firmware de Codito Cerrado. Se Implemento FREERTOS para su uso, así como librerías Básicas en MPLABX y XC16. La idea principal es usar los Microcontroladores de 16Bits de Microchip con periféricos listos y configurados. Es pequeño y Portable, ideal para llevar a todo lado, no intenta competir con controles similares a Arduino. Se desea implementar a futuro un Bootloader tanto por USB, RS232, SD y CAN.

Inicialmente se Requiere un Programador Basado en PICKIT2/ICD3, MPLAB C30 Y MPLAB V4.0 como mínimo. 

En la Actualidad se recomienda el MPLAB SNAP, XC16 y MPLABX V6.0 

Algunos Elementos "Footprints" y "Symbols" están basados en mis librerías, cuales encontraran en este mismo Repositorio.

## Características del Hardware

  * Microcontrolador PIC24HJ128GP504.
  * Pantalla LCD PCD8544 (Based Nokia GLCD) - SPI.
  * Joystick Análogo de 2 ejes + Botón Digital.
  * 4 Botones Digitales.
  * Accelerometro - MMA8452Q - I2C. 
  * Sensor de Temperatura (LM61).
  * Sensor de Luz (LDR).
  * Memoria Eeprom 24LCXXX - I2C.
  * Memoria Ram 23KXX - SPI.
  * Ranura Memoria Micro-SD - SPI.
  * Buzzer por PWM.
  * Conexión USB - FTDI-RL232/UART - 5V.
  * Conexión CAN 5V.
  * 2 LED´s de Actividad.
  * Salidas Para PWM y UART - Con figurables - 3.3V.
  * Conexión ICSP con linea AUX, para control extra de puerto.
  * Cargador de Batería Lipo (MCP73831) con Indicador LED.

## Características Especificas

  * Debido a que el PIC trabaja a 3.3V, el uso del PCA82C251 y el FTDI-RL232 esta a 5V, alimentado directamente por el Control USB, el FTDI-RL232 se encarga de "gestionar" la alimentación del sistema proporcionando un arranque suave en la tensión, luego se pasa por un regulador de 3,3V para alimentar el resto de componentes.
  * Para Potabilidad he agregado un control para la carga de Baterías de tipo Lipo, este gobernado el con el CI MCP73831, el cual mediante el uso del Mosfet DMP1045, intercambia la alimentación proveniente del FTDI-RL232 y la Batería según el estado de conexión USB, se puede usar Baterías de 3,7V en adelante hasta un máximo de 6V, cuando el Game//Cat esta usando la Batería, el FTDI-RL232 se deshabilita.
  * Para el Manejo del Joystick, Botones, Sensor de Temperatura y Luz. he usado el CI-74HC4051, que es un Multiplexor Análogo para leer los Valores por el Modulo ADC, el cual puede usarse de 10 o 12Bits en conjunto con un canal DMA si fuere necesario.
  * La Comunicación UART, es una Salida/Entrada dedicada con un conversor de tensión de 3.3V a 5V de forma bidireccional con transistores Mosfet, con el fin de proteger y poder comunicar el PIC24H con cualquier tipo de dispositivo.
  * La Comunicación USB se hace por medio del CI FTDI-RL232, esto es porque el PIC no posee dicho Modulo y ademas permite ahorrar en la Memoria del PIC el Stack del USB, esto permite que sea Conectar y Usar, puesto que los Drives de este USB son reconocidos de forma inmediata por Windows y Linux sin problemas.
  * La Comunicación CAN la he Incluido porque en estos momentos trabajo con esta interface y su popularidad ha crecido bastante, por experiencia este BUS es muy robusto y fácil de usar, en el PIC se hace uso de dos canales DMA teniendo una respuesta bastante rápida y sin sacrificar la memoria RAM principal, su conexión se hace por medio del Transeiver PCA82C251, ademas he agregado un par de diodos TVH para proteger dicho CI.
  * La Ranura para la Tarjeta Micro-SD, posee conexión Modulo SPI la cual esta compartida con la Memoria Ram 23Kxxx, Ademas la pantalla posee también una conexión al segundo Modulo SPI, que puede usarse para "colgar" otros dispositivos si no vamos ha usar la Pantalla.
  * El control del Buzzer se ha dejado por un Pin que puede ser usado tanto por el Modulo PWM o un pin Común, su uso dependerá del Programa o Aplicación.
  * Posee una Memoria I2C en conjunto con un Accelerometro, con comunicación directa.
  * La programación se hace por medio de la conexión ICSP o Bootloader por USB, usando cualquier programador, PICKIT2-3 y/ó ICD2-3, igual estas salidas pueden usarse como cualquier puerto, teniendo presente que no poseen ninguna protección a tensiones superiores de 3,3V.
  * Ya por Ultimo, he dejado dos visualiza-dores, que son libres de uso.

Básicamente esto es el GAME//CAT, una tarjeta mas que un sistema de control para usuarios avanzados, es una tarjeta de entrenamiento para los principiantes, puesto que todo lo que incluye hace uso forzoso de todo los controles que el PIC24HJ128GP504 incorpora.

## Microcontrolador

* Architecture 16-bit.
* CPU Speed Max. 40 MIPS.
* Memory Type Flash.
* Program Memory 128Kb.
* RAM 8,192 Bytes.
* Temperature Range C -40 to 150.
* Operating Voltage Range (V) 3 to 3.6.
* I/O Pins 35 & Pin Count    44.
* Internal Oscillator 7.37 MHz, 32.768 kH.
* Digital Communication Peripherals 2-UART, 2-SPI,1-I2C, 1-CAN.
* Comparators 2, Capture/Compare/PWM Peripherals 4/4, PWM Resolution bits 16.
* Timers 5 x 16-bit 2 x 32-bit.
* Parallel Port PMP(No Usado), Hardware RTCC-1 (No Usado).
* Chanel DMA-8.
* Cap Touch Channels-13 (No Usado).

## Versiones

* 2017 : 1.0.0 : Primera Versión en Kicad 4
* 2017 : 1.2.0 : Se Agrego Conversión de Tensión 5V a 3.3V Bidireccional en salida UART y PWM, se elimino conexión DC externa.
* 2018 : 2.0.0 : Se Migro completamente a Kicad 5, el Led control se removió para dar opción de selección de Periférico SPI (Ram y SD).
* 2018 : 2.1.0 : Se re-diseño y corrigió error en botón del Joystick, se corrigió el trucado de lineas de Programación PGM y PGD.
* 2018 : 2.2.0 : Se Agrego Resistencias de protección (0Ohm) en entradas Jack RJ11 de Programación.
* 2018 : 2.1.0 : Se Agrego y Calibro Resistencia del Botón de Reset, se agrego control se Carga para Bateria Lipo 3.3V.
* 2018 : 2.5.0 : Se Actulizaron Logos de la Marca y de Hardware Libre, se Actualizo a licencia Creative Commons V4.
* 2018 : 2.7.0 : Se Actualizaron las Librerías de Módulos de Kicad, basadas en Progetti Walter.
* 2018 : 2.9.0 : Se Agregaron condensadores de filtrado al multiplexor análogo, se cambiaron los botones por diseño con poste.
* 2019 : 2.9.1 : Se Organizaron los Archivos para Hospedarlos en Github, Se Ordenaron condensadores y Cristal del PIC.
* 2021 : 2.9.1 : Se Actualiza a KiCad 6 todos los archivos y Librerías.
* 2022 : 3.0.0 : Se Actualizaron los Valores de las resistencias del conversor de 5V-3.3V de un 1K a 10K.
* 2022 : 3.1.0 : Se reestructuro completamente los esquemáticos y se usaron paginas separadas para cada Modulo.
* 2022 : 3.2.0 : Se corrigieron errores en los anchos de pista y reubicaron varios elementos como Seregrafia.
* 2022 : 3.3.0 : Se Actualizaron los conectores Moles para cuatros Salidas, sumando VCC y GND para alimentar controles externos.
* 2022 : 3.5.0 : Se Actualizaron los Logos y posiciones de Seregrafia de Varios componentes.


## ERRATAS

* Debido a tolerancia de tensión del MCP2551, no es posible usarlo para tensiones de 3.3V, cual hacer imposible usar el CANBUS, se reconocidos usar el PCA82C251 cual soportar desde 1.8V hasta 24V.

## Créditos

![](https://github.com/trunksx64/GAME_CAT_R3_KICAD/blob/main/Images/banner_game_cat.png)

xDNA Electronics & Desing es una Micro-empresa Personal, que se dedica y encarga de elaborar proyectos de Control y Automatización por pedido, su idea es colaborar y ayudar a quines a si lo requieran, el proyecto se hizo principalmente como Hobby el cual gracias a terceros se pudo implementar y hacer su creación, por lo cual se da la libertad de usarlo para experimentar sin hacer uso comercial del mismo.

## Licencia

![](https://github.com/trunksx64/GAME_CAT_R3_KICAD/blob/main/Images/creative_commons.png)

Licensed under Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)
