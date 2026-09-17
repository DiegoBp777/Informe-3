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
- [16. Pruebas y resultados](#16-pruebas-y-resultados)
- [17. Dificultades encontradas](#17-dificultades-encontradas)
- [18. Análisis crítico](#18-análisis-crítico)
- [19. Conclusiones](#19-conclusiones)

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
