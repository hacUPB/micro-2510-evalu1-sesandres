## Explica cómo se realiza el proceso de decodificación por parte de la CPU. Si encontraste otras funcionalidades, repórtalas en tu repositorio.

La decodificación de una instrucción en la CPU sigue estos pasos:

#### 1. Recepción de la Instrucción: La instrucción obtenida en el paso fetch se carga en el registro de instrucciones (IR).

#### 2. Descomposición: La instrucción se divide en diferentes partes:

##### 2.1. Opcode: El código de operación que indica qué acción realizar (sumar, mover, etc.).
##### 2.2.Operandos: Los datos o direcciones de memoria involucradas en la operación.
#### 3. Decodificación: La unidad de control interpreta el opcode y coordina qué operación se debe realizar. También selecciona los registros o direcciones de memoria que se utilizarán.

#### 4. Asignación de Recursos: Se configuran los registros y los buses de datos según lo que la instrucción requiere para ejecutar la operación.