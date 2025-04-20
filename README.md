# Sistema de Sensado y Transmisión de Temperatura vía LoRa utilizando PIC16F887

Este proyecto consiste en el diseño e implementación de un sistema de adquisición de temperatura en un entorno sin conectividad, utilizando un microcontrolador **PIC16F887** y un módulo **LoRa SX1278**. Fue desarrollado como trabajo final de la materia **Electrónica Digital II** de la Facultad de Ciencias Exactas, Físicas y Naturales de la Universidad Nacional de Córdoba.

## Autores

- **Giuliano Matías Palombarini** – giuliano.palombarini@mi.unc.edu.ar  
- **Marcos Raimondi** – marcosraimondi1@mi.unc.edu.ar  
- **Gastón Marcelo Segura** – gastonsegura2908@mi.unc.edu.ar

## Descripción general

El objetivo fue desarrollar un **nodo de sensado remoto** capaz de adquirir datos de temperatura a partir de un sensor analógico **LM35**, procesarlos mediante el PIC16F887 y transmitirlos a un **gateway LoRa** implementado con una **ESP32**, desde donde los datos pueden subirse a Internet.

El sistema permite establecer configuraciones iniciales desde una PC mediante puerto serie, como:
- Intervalo entre muestras (1 a 255 segundos).
- Límite superior e inferior de temperatura para envío forzado.

## Funcionamiento del sistema

- El PIC arranca en **modo configuración**, recibiendo parámetros desde la PC.
- Al presionar un botón (RB0), se pasa al **modo transmisión**, donde:
  - Se toman muestras con el **ADC del PIC** desde el LM35.
  - Se calcula el promedio de las muestras.
  - Se transmite el valor promedio por UART a un **Arduino UNO** que se encarga de enviarlo por **LoRa**.
- El gateway, compuesto por un **ESP32 + módulo LoRa**, recibe los datos para su posterior uso o envío a Internet.

## Interrupciones utilizadas

- **Timer0**: genera eventos cada segundo para controlar el tiempo entre transmisiones.
- **ADC**: al completar una conversión, actualiza registros y evalúa si se superaron los umbrales.
- **Puerto Serie (UART)**: permite configuración desde PC y transmisión de datos hacia el Arduino.
- **RB0**: entrada para pulsador que alterna entre los modos de operación (configuración/transmisión).

## Hardware del sistema

### Nodo transmisor

- PIC16F887
- Sensor LM35
- Arduino UNO
- Módulo LoRa SX1278
- Conversor UART-USB
- Pulsador (modo de cambio)
- PC (solo para configuración)

### Gateway receptor

- ESP32
- Módulo LoRa SX1278

## Software e interfaz

- **PIC16F887** programado en lenguaje Assembly.
- **Arduino UNO y ESP32** programados utilizando el framework de desarrollo Arduino.
- **Interfaz gráfica en Python** para configurar el PIC desde la PC vía puerto serie.
  - Permite definir el tiempo de muestreo y límites de temperatura.
  - Muestra por consola (Serial Monitor) los datos recibidos.

## Conclusiones

Este proyecto permitió aplicar los conceptos teóricos de la materia para abordar un problema real, combinando electrónica digital, microcontroladores, adquisición de datos y comunicaciones inalámbricas. El sistema es funcional, estable y escalable.
