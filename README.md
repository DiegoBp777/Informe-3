# Práctica 3 - Control de un LED mediante un pulsador con PIC18F45K22

## Integrantes

- **Jareth Santiago Escamilla Marquez** - [@jarethescamilla](https://github.com/jarethescamilla)
- **Diego Alexander Baron Pacheco** - [@DiegoBp777](https://github.com/DiegoBp777)
- **Fredy Vicente Patiño Garzon** - [@fredyvipatinoga-crypto](https://github.com/fredyvipatinoga-crypto)

---

## Tabla de contenido

- [1. Introducción](#1-introducción)
- [2. Objetivos](#2-objetivos)
  - [2.1. Objetivo general](#21-objetivo-general)
  - [2.2. Objetivos específicos](#22-objetivos-específicos)
- [3. Planteamiento del problema](#3-planteamiento-del-problema)
- [4. Análisis del problema](#4-análisis-del-problema)
- [5. Entradas, proceso y salidas](#5-entradas-proceso-y-salidas)
- [6. Algoritmo](#6-algoritmo)
- [7. Pseudocódigo](#7-pseudocódigo)
- [8. Diagrama de flujo](#8-diagrama-de-flujo)
- [9. Marco teórico](#9-marco-teórico)
- [10. Materiales y herramientas](#10-materiales-y-herramientas)
- [11. Diseño del circuito](#11-diseño-del-circuito)
- [12. Conexiones del PIC18F45K22](#12-conexiones-del-pic18f45k22)
- [13. Implementación del programa](#13-implementación-del-programa)
- [14. Código utilizado](#14-código-utilizado)
- [15. Simulación en Proteus](#15-simulación-en-proteus)
- [16. Evidencias](#16-evidencias)
  - [16.1. Código desarrollado en MPLAB X IDE](#161-código-desarrollado-en-mplab-x-ide)
  - [16.2. Circuito implementado en Proteus](#162-circuito-implementado-en-proteus)
  - [16.3. Simulación con el pulsador sin presionar](#163-simulación-con-el-pulsador-sin-presionar)
  - [16.4. Simulación con el pulsador presionado](#164-simulación-con-el-pulsador-presionado)
  - [16.5. Funcionamiento completo](#165-funcionamiento-completo)
- [17. Pruebas y resultados](#17-pruebas-y-resultados)
- [18. Dificultades encontradas](#18-dificultades-encontradas)
- [19. Análisis crítico](#19-análisis-crítico)
- [20. Conclusiones](#20-conclusiones)

---

# 1. Introducción

En esta práctica se realizó la implementación de un sistema básico de entrada y salida digital utilizando el microcontrolador **PIC18F45K22**.

El objetivo principal consiste en utilizar un **pulsador como dispositivo de entrada** para controlar un **LED conectado a una salida digital del microcontrolador**.

El funcionamiento requerido es que, mientras el pulsador se encuentre presionado, el LED permanezca encendido. Al dejar de presionar el pulsador, el LED debe apagarse.

Para el desarrollo de la práctica se utilizó **MPLAB X IDE con el compilador XC8** para realizar la programación del microcontrolador y **Proteus** para realizar el diseño y la simulación del circuito.

Esta práctica permite comprender los conceptos básicos de configuración de entradas y salidas digitales, lectura del estado de un pulsador y control de un dispositivo de salida mediante el PIC18F45K22.

---

# 2. Objetivos

## 2.1. Objetivo general

Implementar un circuito utilizando el **PIC18F45K22**, en el cual un pulsador conectado a una entrada digital controle el encendido y apagado de un LED conectado a una salida digital.

## 2.2. Objetivos específicos

- Configurar el oscilador interno del PIC18F45K22 a 1 MHz.
- Configurar un pin del microcontrolador como entrada digital.
- Configurar un pin del microcontrolador como salida digital.
- Utilizar un pulsador para generar una señal de entrada.
- Detectar el estado del pulsador mediante el programa.
- Encender el LED mientras el pulsador se encuentre presionado.
- Apagar el LED cuando el pulsador sea liberado.
- Implementar el programa utilizando MPLAB X IDE y XC8.
- Comprobar el funcionamiento del circuito mediante una simulación en Proteus.

---

# 3. Planteamiento del problema

Se requiere diseñar un sistema utilizando el microcontrolador **PIC18F45K22**, en el cual una entrada digital sea controlada mediante un pulsador y una salida digital controle un LED.

El sistema debe funcionar de la siguiente manera:

### Pulsador sin presionar

Cuando el pulsador no está presionado, la entrada del microcontrolador debe encontrarse en un estado lógico alto:

```text
Pulsador = 1
```
En este estado el LED debe permanecer apagado:
```text
LED = 0
```
**Pulsador presionado**

Cuando el pulsador es presionado, la entrada del microcontrolador se conecta a tierra y pasa a un estado lógico bajo:

Pulsador = 0

El microcontrolador debe detectar este estado y encender el LED:
```text
LED = 1
```
Por lo tanto, el funcionamiento general del sistema es:
```text
Sin presionar → LED apagado

Presionado → LED encendido

Soltar → LED apagado
```
---
# 4. Análisis del problema

Para solucionar el problema se identifican tres elementos principales:
```text
ENTRADA → PROCESO → SALIDA
```
**Entrada**

La entrada corresponde al pulsador conectado al pin:
```text
RA0
```
El pulsador utiliza una resistencia de 10 kΩ conectada a +5 V, funcionando como resistencia de polarización o pull-up.

Cuando el pulsador no está presionado:
```text
RA0 = 1
```
Cuando el pulsador está presionado:
```text
RA0 = 0
```
**Proceso**

El PIC18F45K22 lee continuamente el estado de RA0.

Si RA0 es igual a `0`, significa que el pulsador está presionado y el microcontrolador debe colocar RD0 en `1` para encender el LED.

Si RA0 es igual a `1`, significa que el pulsador está liberado y el microcontrolador debe colocar RD0 en `0` para apagar el LED.

**Salida**

La salida corresponde al LED conectado al pin:
```text
RD0
```
El funcionamiento es:
```text
RD0 = 1 → LED encendido

RD0 = 0 → LED apagado
```
---
# 5. Entradas, proceso y salidas

El sistema puede representarse de la siguiente manera:
```text
┌────────────────────┐
│       ENTRADA      │
│                    │
│      Pulsador      │
│         ↓          │
│        RA0         │
└─────────┬──────────┘
          │
          ↓
┌────────────────────┐
│       PROCESO      │
│                    │
│    PIC18F45K22     │
│                    │
│  Lee el estado de  │
│      la entrada    │
└─────────┬──────────┘
          │
          ↓
┌────────────────────┐
│       SALIDA       │
│                    │
│        RD0         │
│         ↓          │
│        LED         │
└────────────────────┘
```
**Tabla de funcionamiento**

| Estado del pulsador    | RA0 | RD0 | Estado del LED |
| ---------------------- | --: | --: | -------------- |
| Sin presionar          |   1 |   0 | Apagado        |
| Presionado             |   0 |   1 | Encendido      |
| Se mantiene presionado |   0 |   1 | Encendido      |
| Se suelta              |   1 |   0 | Apagado        |
---
# 6. Algoritmo

El algoritmo desarrollado para resolver el problema es el siguiente:

1. Iniciar el programa.
2. Configurar el oscilador interno del PIC18F45K22 a 1 MHz.
3. Desactivar las funciones analógicas de los puertos utilizados.
4. Configurar RA0 como entrada digital.
5. Configurar RD0 como salida digital.
6. Inicializar el LED apagado.
7. Leer continuamente el estado de RA0.
8. Comprobar si el pulsador está presionado.
9. Si RA0 es igual a 0, encender el LED mediante RD0.
10. Si RA0 es igual a 1, apagar el LED mediante RD0.
11. Repetir continuamente el proceso.
---
# 7. Pseudocódigo
```text
INICIO

Configurar oscilador a 1 MHz

Configurar RA0 como entrada

Configurar RD0 como salida

Apagar LED

MIENTRAS verdadero HACER

    Leer RA0

    SI RA0 = 0 ENTONCES
        Encender LED
    SINO
        Apagar LED
    FIN SI

FIN MIENTRAS

FIN
```
---
# 8. Diagrama de flujo

El funcionamiento del programa puede representarse mediante el siguiente diagrama:

                 ┌───────────────┐
                 │    INICIO     │
                 └───────┬───────┘
                         │
                         ↓
              ┌─────────────────────┐
              │ Configurar           │
              │ oscilador a 1 MHz    │
              └──────────┬──────────┘
                         │
                         ↓
              ┌─────────────────────┐
              │ Configurar RA0 como  │
              │ entrada digital      │
              │                     │
              │ Configurar RD0 como  │
              │ salida digital       │
              └──────────┬──────────┘
                         │
                         ↓
                  ┌─────────────┐
                  │  Leer RA0   │
                  └──────┬──────┘
                         │
                         ↓
                  ┌─────────────┐
                  │ ¿RA0 = 0?   │
                  │ ¿Pulsador   │
                  │ presionado? │
                  └──────┬──────┘
                     SI  │  NO
                         │
              ┌──────────┘ └──────────┐
              ↓                       ↓
       ┌───────────────┐      ┌───────────────┐
       │ RD0 = 1       │      │ RD0 = 0       │
       │ Encender LED  │      │ Apagar LED    │
       └───────┬───────┘      └───────┬───────┘
               │                      │
               └──────────┬───────────┘
                          │
                          ↓
                   ┌─────────────┐
                   │ Volver a    │
                   │ leer RA0    │
                   └──────┬──────┘
                          │
                          └───────────↺
                          
---
# 9. Marco teórico
## 9.1. Microcontrolador PIC18F45K22

El PIC18F45K22 es un microcontrolador de la familia PIC18 que permite desarrollar sistemas electrónicos mediante la programación de sus entradas, salidas, temporizadores y diferentes periféricos.

Para esta práctica se utilizan principalmente los puertos A y D para realizar la comunicación entre el pulsador, el microcontrolador y el LED.

## 9.2. Entrada digital

Una entrada digital permite detectar dos estados lógicos:
```text
0 → LOW

1 → HIGH
```
En esta práctica se utiliza el pin RA0 como entrada digital.

El estado de esta entrada depende de la posición del pulsador.

## 9.3. Salida digital

Una salida digital permite controlar dispositivos externos utilizando niveles lógicos.

En esta práctica se utiliza el pin RD0 como salida para controlar el LED.
```text
RD0 = 1 → LED encendido

RD0 = 0 → LED apagado
```
## 9.4. Resistencia Pull-Up

La resistencia de 10 kΩ conectada entre +5 V y RA0 permite mantener la entrada en un estado lógico alto cuando el pulsador está abierto.

La conexión utilizada es:

             +5 V
               │
              10kΩ
               │
               ├──────── RA0
               │
           ┌───┴───┐
           │Pulsador│
           └───┬───┘
               │
              GND

De esta forma:
```text
Pulsador abierto  → RA0 = 1

Pulsador cerrado  → RA0 = 0
```
Por esta razón, el programa considera que el pulsador está presionado cuando RA0 tiene un valor lógico `0`.
---
# 10. Materiales y herramientas
**Materiales**
PIC18F45K22.
* Pulsador.
* LED.
* Resistencia de 10 kΩ.
* Resistencia limitadora para el LED.
* Fuente de alimentación de 5 V.
* Protoboard.
* Cables de conexión.
**Software**
* MPLAB X IDE.
* Compilador XC8.
* Proteus Design Suite.

---
  
# 11. Diseño del circuito

El circuito fue diseñado en Proteus utilizando el microcontrolador PIC18F45K22.

Para la entrada se utilizó el pin:
```text
RA0 → Pulsador
```
Para la salida se utilizó:
```text
RD0 → LED
```
La conexión general del circuito es:

                 +5 V
                  │
                 10kΩ
                  │
                  ├──────────── RA0
                  │
              ┌───┴───┐
              │Pulsador│
              └───┬───┘
                  │
                 GND


              PIC18F45K22
                   │
                  RD0
                   │
                Resistencia
                limitadora
                   │
                  LED
                   │
                  GND
---
# 12. Conexiones del PIC18F45K22

Las principales conexiones utilizadas en la práctica son:

| Pin del PIC | Función                |
| ----------- | ---------------------- |
| RA0         | Entrada del pulsador   |
| RD0         | Salida para el LED     |
| MCLR        | Configuración de reset |
| VDD         | Alimentación +5 V      |
| VSS         | Tierra (GND)           |

**Conexión del pulsador**

El pulsador se conecta entre RA0 y GND.

Además, se utiliza una resistencia de 10 kΩ entre RA0 y +5 V.
```text
+5 V
 │
10 kΩ
 │
 ├──── RA0
 │
Pulsador
 │
GND
```
**Conexión del LED**

El LED se conecta a RD0 mediante una resistencia limitadora de corriente:
```text
RD0
 │
Resistencia
 │
LED
 │
GND
```
---
# 13. Implementación del programa

El programa fue desarrollado en MPLAB X IDE utilizando el compilador XC8.

Se mantuvo la configuración del oscilador interno utilizada en la práctica anterior:
```text
#pragma config FOSC = INTIO67
```
El oscilador interno se configura a 1 MHz mediante:
```text
OSCCON = 0b10000000;
```
Posteriormente se desactivan las funciones analógicas de los puertos utilizados:
```text
ANSELA = 0;
ANSELD = 0;
```
Esto permite utilizar RA0 y RD0 como pines digitales.

RA0 se configura como entrada:
```text
TRISAbits.TRISA0 = 1;
```
RD0 se configura como salida:
```text
TRISDbits.TRISD0 = 0;
```
Finalmente, dentro del ciclo principal se comprueba continuamente el estado del pulsador.

Si RA0 es igual a 0, se enciende el LED:
```text
LATDbits.LATD0 = 1;
```
Si RA0 es igual a 1, se apaga:
```text
LATDbits.LATD0 = 0;
```
---
# 14. Código utilizado
```text
/*
 * File:   main.c
 * Author: LOS MAKIAS
 *
 * Practica 3
 * Control de LED mediante pulsador
 */

#include <xc.h>

// Configuracion del oscilador interno a 1MHz
#pragma config FOSC = INTIO67
#pragma config WDTEN = OFF
#pragma config LVP = OFF

#define _XTAL_FREQ 1000000

void main(void) {

    // Configurar el oscilador interno a 1MHz
    OSCCON = 0b10000000;

    // Desactivar entradas analogicas
    ANSELA = 0;
    ANSELD = 0;

    // RA0 como entrada
    TRISAbits.TRISA0 = 1;

    // RD0 como salida
    TRISDbits.TRISD0 = 0;

    // LED inicialmente apagado
    LATDbits.LATD0 = 0;

    while(1)
    {
        // Verificar si el pulsador esta presionado
        if(PORTAbits.RA0 == 0)
        {
            // Encender LED
            LATDbits.LATD0 = 1;
        }
        else
        {
            // Apagar LED
            LATDbits.LATD0 = 0;
        }
    }

    return;
}
```
---
# 15. Simulación en Proteus

Después de realizar el programa en MPLAB X IDE, se realizó la compilación del proyecto para generar el archivo `.hex`.

Posteriormente, este archivo se cargó en las propiedades del PIC18F45K22 dentro de Proteus.

Una vez iniciado el circuito se realizaron las pruebas correspondientes.

**Estado 1: Pulsador sin presionar**

Cuando el pulsador está abierto, la resistencia de 10 kΩ mantiene la entrada RA0 en un nivel lógico alto:
```text
RA0 = 1
```
El programa ejecuta:
```text
LATDbits.LATD0 = 0;
```
Por lo tanto:
```text
LED = APAGADO
Evidencia
```
**Estado 2: Pulsador presionado**

Cuando se presiona el pulsador, RA0 se conecta a tierra:
```text
RA0 = 0
```
El programa detecta esta condición y ejecuta:
```text
LATDbits.LATD0 = 1;
```
Por lo tanto:
```text
LED = ENCENDIDO
```
**Estado 3: Pulsador liberado**

Cuando se deja de presionar el pulsador, la resistencia pull-up vuelve a colocar RA0 en nivel alto:
```text
RA0 = 1
```
El programa apaga nuevamente el LED:
```text
LATDbits.LATD0 = 0;
```
Por lo tanto:
```text
LED = APAGADO
```
---
## 16. Evidencias

En esta sección se presentan las evidencias correspondientes al desarrollo de la práctica, incluyendo la programación realizada en MPLAB X IDE, el montaje del circuito en Proteus y las diferentes pruebas de funcionamiento del sistema.

### 16.1. Código desarrollado en MPLAB X IDE

En la siguiente evidencia se muestra el código desarrollado en MPLAB X IDE para controlar el LED mediante el pulsador conectado al PIC18F45K22.

El programa configura el oscilador interno del microcontrolador a 1 MHz, establece RA0 como entrada digital para el pulsador y RD0 como salida digital para el LED. Posteriormente, el programa verifica continuamente el estado del pulsador y controla el LED de acuerdo con dicha entrada.

![Código desarrollado en MPLAB](imagenes/codigo_mplab.png)

---

### 16.2. Circuito implementado en Proteus

En esta evidencia se presenta el circuito implementado en Proteus. Se utilizó un microcontrolador PIC18F45K22, un pulsador conectado a la entrada RA0 y un LED conectado a la salida RD0 mediante una resistencia para limitar la corriente.

El pulsador utiliza una resistencia de 10 kΩ como resistencia de pull-up, por lo que la entrada RA0 permanece en nivel lógico alto cuando el pulsador no está presionado y pasa a nivel lógico bajo cuando se presiona.

![Circuito realizado en Proteus](imagenes/circuito_proteus.png)

---

### 16.3. Simulación con el pulsador sin presionar

En esta prueba el pulsador se encuentra en estado de reposo, es decir, sin ser presionado. Debido a la resistencia de pull-up, la entrada RA0 se encuentra en nivel lógico alto.

El programa detecta que el pulsador no está presionado y mantiene la salida RD0 en nivel lógico bajo, por lo que el LED permanece apagado.

![Pulsador sin presionar - LED apagado](imagenes/led_apagado.png)

---

### 16.4. Simulación con el pulsador presionado

En esta prueba se presiona el pulsador conectado a la entrada RA0. Al realizar esta acción, la entrada pasa a nivel lógico bajo.

El microcontrolador detecta esta condición y establece la salida RD0 en nivel lógico alto, provocando que el LED se encienda mientras el pulsador permanezca presionado.

![Pulsador presionado - LED encendido](imagenes/led_encendido.png)

---
---
# 17. Pruebas y resultados

Se realizaron diferentes pruebas para verificar el funcionamiento del sistema.

| Prueba | Estado del pulsador    | RA0 | RD0 | LED       |
| ------ | ---------------------- | --: | --: | --------- |
| 1      | Sin presionar          |   1 |   0 | Apagado   |
| 2      | Presionado             |   0 |   1 | Encendido |
| 3      | Se mantiene presionado |   0 |   1 | Encendido |
| 4      | Se suelta              |   1 |   0 | Apagado   |

Los resultados obtenidos corresponden al funcionamiento esperado.

El LED permanece encendido mientras el pulsador se encuentra presionado y se apaga inmediatamente después de liberar el pulsador.
---
# 18. Dificultades encontradas

Durante el desarrollo de la práctica se presentaron algunas dificultades relacionadas con la configuración de los pines del PIC18F45K22 y la conexión del pulsador.

Una de las principales consideraciones fue comprender el funcionamiento de la resistencia de 10 kΩ utilizada como pull-up.

Debido a esta conexión, el estado lógico de la entrada es:
```text
Pulsador sin presionar → RA0 = 1

Pulsador presionado → RA0 = 0
```
Por esta razón, la condición utilizada en el programa es:
```text
if(PORTAbits.RA0 == 0)
```
También fue necesario desactivar las funciones analógicas mediante:
```text
ANSELA = 0;
ANSELD = 0;
```
para garantizar que los pines utilizados funcionaran correctamente como entradas y salidas digitales.

Otra consideración importante fue utilizar los registros `LATD` para controlar la salida del LED y `PORTA` para leer el estado de la entrada.
---
# 19. Análisis crítico

La práctica permitió comprobar el funcionamiento de un sistema básico de entrada, procesamiento y salida utilizando el PIC18F45K22.

El problema planteado fue solucionado mediante una lectura continua del estado del pulsador. El pin RA0 funciona como entrada digital, el microcontrolador procesa la información recibida y el pin RD0 controla el LED como salida.

Uno de los aspectos más importantes de la práctica fue comprender que la entrada utiliza una resistencia pull-up. Debido a esto, el estado lógico de RA0 es `1`  cuando el pulsador está libre y cambia a `0` cuando el pulsador es presionado.

Esta característica fue tenida en cuenta al momento de desarrollar la condición del programa.

El funcionamiento obtenido cumple con el objetivo planteado: el LED se enciende mientras el pulsador está presionado y se apaga cuando el pulsador deja de presionarse.

La simulación en Proteus permitió comprobar el comportamiento del circuito y verificar la relación entre la entrada y la salida antes de realizar una implementación física.

Como limitación, el sistema desarrollado solamente utiliza una entrada y una salida digital, por lo que corresponde a una aplicación básica de control. Sin embargo, la estructura utilizada puede servir como base para sistemas más complejos con múltiples entradas y salidas.
---
# 20. Conclusiones

* Se implementó correctamente un sistema de entrada y salida digital utilizando el microcontrolador PIC18F45K22.
* Se configuró el pin RA0 como entrada digital para detectar el estado del pulsador.
* Se configuró el pin RD0 como salida digital para controlar el LED.
* Se comprobó que al presionar el pulsador el LED se enciende.
* Se comprobó que al soltar el pulsador el LED se apaga.
* Se comprendió el funcionamiento de una resistencia pull-up de 10 kΩ.
* Se implementó el programa utilizando MPLAB X IDE y XC8.
* Se verificó el funcionamiento del circuito mediante la simulación en Proteus.
* La práctica permitió fortalecer los conocimientos sobre configuración de puertos digitales, lectura de entradas y control de salidas mediante un microcontrolador.


