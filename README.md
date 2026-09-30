# Código de Hamming (7,4) — Detección y Corrección de Errores

## Autores

* **Miguel Ángel Plazas Llanes**

**Ingeniería de Telecomunicaciones**  
**Universidad Militar Nueva Granada**  
**Docente:** José de Jesús Rúgeles Uribe

---

## Detección y Corrección de Errores mediante Código de Hamming (7,4)

Este repositorio contiene el desarrollo y análisis del **Código de Hamming (7,4)** para la detección y corrección automática de errores en transmisiones digitales[cite: 1].  
En este trabajo se implementa el esquema de Control de Errores Hacia Adelante (FEC) utilizando la técnica de paridad par sobre palabras de datos de 4 bits ($D_3D_2D_1D_0$), generando tramas codificadas de 7 bits con 3 bits de redundancia ($P_2$, $P_1$ y $P_0$)[cite: 1].

Se evaluó la integridad de las palabras asignadas **Palabra A ($0101_2$)** y **Palabra B ($1100_2$)**, comprobando la generación del síndrome de paridad $C_2C_1C_0 = 000_2$ para transmisiones sin ruido y la detección/corrección precisa ante la inyección simulada de errores de un solo bit en las posiciones 5 y 6 respectivamente[cite: 1].

---

## Objetivos

### Objetivo general
Implementar y evaluar el código de detección y corrección de errores de Hamming (7,4) mediante el cálculo de bits de paridad par sobre palabras de datos de 4 bits, verificando la detección y corrección de errores de un solo bit mediante el síndrome de paridad[cite: 1].

### Objetivos específicos
* Calcular los bits de paridad par ($P_0$, $P_1$ y $P_2$) para formar las palabras codificadas de 7 bits correspondientes a las palabras de datos asignadas: $A = 0101$ y $B = 1100$[cite: 1].
* Verificar la integridad de las palabras codificadas en recepción mediante el cálculo del síndrome de paridad $C_2C_1C_0$, comprobando que sea igual a $000_2$ cuando no se presentan errores en el canal[cite: 1].
* Simular la inyección de errores de un solo bit en posiciones específicas de las palabras codificadas (posición 5 en $A$ y posición 6 en $B$) y evaluar la capacidad del síndrome para localizar y corregir el bit alterado[cite: 1].

---

## Parámetros de la práctica

| Parámetro | Valor |
| :--- | :--- |
| **Algoritmo de Codificación** | Código de Hamming (7,4)[cite: 1] |
| **Criterio de Paridad** | Paridad Par[cite: 1] |
| **Bits de Datos ($k$)** | 4 bits ($D_3, D_2, D_1, D_0$)[cite: 1] |
| **Bits de Redundancia ($m$)** | 3 bits ($P_2, P_1, P_0$)[cite: 1] |
| **Longitud de la Trama ($n$)** | 7 bits ($n = k + m$)[cite: 1] |
| **Distancia Mínima de Hamming ($d_{\min}$)** | 3[cite: 1] |
| **Capacidad de Corrección** | 1 bit por trama (SEC)[cite: 1] |
| **Palabra de Datos A** | `0101`[cite: 1] |
| **Palabra de Datos B** | `1100`[cite: 1] |

---

## Metodología

### 1. Estructura de Posiciones de la Trama (7 bits)
Los bits de paridad se ubican en las posiciones correspondientes a potencias de $2$ ($1, 2, 4$), mientras que los bits de datos ocupan las posiciones restantes ($3, 5, 6, 7$)[cite: 1]:

| Posición Trama | 7 | 6 | 5 | 4 | 3 | 2 | 1 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Peso Binario** | $111_2$ | $110_2$ | $101_2$ | $100_2$ | $011_2$ | $010_2$ | $001_2$ |
| **Asignación de Bit** | $D_3$ | $D_2$ | $D_1$ | $P_2$ | $D_0$ | $P_1$ | $P_0$ |

### 2. Ecuaciones de Generación de Paridad Par
Cada bit de paridad se calcula aplicando la operación XOR ($\oplus$) sobre su respectivo grupo de comprobación[cite: 1]:
* **$P_0$ (supervisa posiciones 1, 3, 5, 7):** $P_0 = D_0 \oplus D_1 \oplus D_3$[cite: 1]
* **$P_1$ (supervisa posiciones 2, 3, 6, 7):** $P_1 = D_0 \oplus D_2 \oplus D_3$[cite: 1]
* **$P_2$ (supervisa posiciones 4, 5, 6, 7):** $P_2 = D_1 \oplus D_2 \oplus D_3$[cite: 1]

### 3. Evaluación del Síndrome de Paridad en Recepción
En recepción se calculan los bits de comprobación $C_0, C_1, C_2$ mediante las ecuaciones de paridad[cite: 1]:
* $C_0 = P_0 \oplus D_0 \oplus D_1 \oplus D_3$[cite: 1]
* $C_1 = P_1 \oplus D_0 \oplus D_2 \oplus D_3$[cite: 1]
* $C_2 = P_2 \oplus D_1 \oplus D_2 \oplus D_3$[cite: 1]

El síndrome binario $S = C_2C_1C_0$ representa la posición decimal del bit alterado ($S_{10}$)[cite: 1].

---

## Resultados y Análisis

### Resumen de Codificación, Detección y Corrección

| Parámetro Evaluado | Caso 1: Word A | Caso 2: Word B |
| :--- | :--- | :--- |
| **Datos Originales (4 bits)** | `0101`[cite: 1] | `1100`[cite: 1] |
| **Bits de Paridad Calculados** | $P_2=1, P_1=0, P_0=1$[cite: 1] | $P_2=0, P_1=0, P_0=1$[cite: 1] |
| **Trama Transmitida (7 bits)** | `0101101`[cite: 1] | `1100001`[cite: 1] |
| **Comprobación Limpia ($C_2C_1C_0$)** | `000` (Sin error)[cite: 1] | `000` (Sin error)[cite: 1] |
| **Posición del Error Inyectado** | Posición 5 ($D_1$)[cite: 1] | Posición 6 ($D_2$)[cite: 1] |
| **Palabra Recibida Alterada** | `0111101`[cite: 1] | `1000001`[cite: 1] |
| **Síndrome Calculado ($C_2C_1C_0$)** | $101_2 \rightarrow \mathbf{5_{10}}$[cite: 1] | $110_2 \rightarrow \mathbf{6_{10}}$[cite: 1] |
| **Acción Correctiva** | Inversión Bit 5 ($1 \rightarrow 0$)[cite: 1] | Inversión Bit 6 ($0 \rightarrow 1$)[cite: 1] |
| **Trama Corregida Recuperada** | `0101101`[cite: 1] | `1100001`[cite: 1] |
| **Datos Finales Recuperados** | `0101`[cite: 1] | `1100`[cite: 1] |

---

## Desarrollo

- [x] Informe
- [x] Procedimiento cuaderno
