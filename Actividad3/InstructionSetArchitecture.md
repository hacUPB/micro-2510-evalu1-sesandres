### 1. Diferencia entre desplazamiento lógico y aritmético
Desplazamiento lógico (LSR/LSL):  
Mueve los bits hacia la derecha o izquierda, rellenando con ceros en las posiciones vacías. No considera el signo del número.
Ejemplo: MOV R4, R1, LSR #2 desplaza 2 bits a la derecha en R1 y almacena en R4.

Desplazamiento aritmético (ASR):  
Al desplazar a la derecha, preserva el bit de signo (útil para números con signo en complemento a 2).
Ejemplo: MOV R5, R2, ASR #3 desplaza 3 bits a la derecha en R2, manteniendo el signo.

### 2. Aplicaciones útiles para ASR en lugar de LSR
En aplicaciones que manejan números con signo, como:  
-Procesamiento de señales (ej: audio).  
-Algoritmos matemáticos que requieren división por potencias de 2 preservando el signo.

### 3. Diferencia entre MOV R0, #42 y MOV R0, R1
-MOV R0, #42: Carga el valor inmediato 42 en el registro R0.  
-MOV R0, R1: Copia el valor almacenado en R1 al registro R0.

## 4. Función de MOVS vs MOV
-MOVS: Actualiza los flags de condición (como Zero, Negative) en el registro APSR.  
-MOV: Solo mueve el valor, sin afectar los flags.

### 5. Uso de MOVT con MOVW
Para cargar valores de 32 bits en un registro:

MOVW R8, #0x1234: Carga los 16 bits bajos (0x1234) en R8.

MOVT R8, #0x5678: Carga los 16 bits altos (0x5678) en R8, resultando en R8 = 0x56781234.

### 6. Limitaciones de valores inmediatos
En ARM, los valores inmediatos deben cumplir un formato específico:

Un byte rotado (8 bits + 4 bits de rotación).
Ejemplo: MOV R0, #0x1F0 es válido, pero MOV R0, #0x12345 no.

### 7. Máximo valor inmediato posible
El máximo valor inmediato es 0xFF (255), pero puede extenderse usando rotaciones (ej: 0xFF0).
Ejemplo: MOV R0, #0xFF00 es válido si se codifica con rotación.

### 8. Alternativa para mover números grandes
Usar dos instrucciones:

-MOVW para los 16 bits bajos.  
-MOVT para los 16 bits altos.  
Ejemplo:  
MOVW R0, #0x1234   ; R0 = 0x00001234  
MOVT R0, #0x5678   ; R0 = 0x56781234  