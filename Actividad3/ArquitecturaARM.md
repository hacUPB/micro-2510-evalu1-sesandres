### 1. ¿Qué significa que ARM sea una arquitectura RISC?
ARM es una arquitectura RISC (Reduced Instruction Set Computing), lo que significa que su conjunto de instrucciones es reducido y optimizado.   
Las características clave incluyen:

-Instrucciones simples y de longitud fija (generalmente 32 bits en ARM clásico).  
-Ejecución en un solo ciclo de reloj para la mayoría de las operaciones.  
-Enfoque en la eficiencia energética, ideal para dispositivos móviles y embebidos.  
-Uso intensivo de registros (16 registros de propósito general en ARM clásico).


### 2. ¿Por qué la arquitectura ARM es popular en dispositivos móviles?
Bajo consumo de energía: Optimizada para eficiencia energética, crucial para baterías. 

-Flexibilidad: Licencias de diseño permiten personalizaciones (ej: Snapdragon, Apple M1).  
-Rendimiento equilibrado: Combina potencia y eficiencia gracias a diseños como big.LITTLE.  
-Ecosistema amplio: Soporte de software (Android, iOS) y hardware (GPUs, modems).

### 3. ¿En qué consiste la “Arquitectura Harvard modificada” en ARM?
Aunque ARM usa principalmente arquitectura von Neumann (bus único para datos e instrucciones), en ciertos microcontroladores (Cortex-M) se emplea una Harvard modificada:

-Buses separados para instrucciones y datos, permitiendo acceso simultáneo.  
-Memoria unificada a nivel lógico: Las direcciones de memoria son únicas, pero físicamente hay separación.

### 4. ¿Cuáles son las principales familias de procesadores ARM?
-Cortex-A: Para aplicaciones de alto rendimiento (smartphones, servidores).  
-Cortex-R: Enfocado en sistemas en tiempo real (automóviles, industriales).  
-Cortex-M: Microcontroladores de bajo consumo (IoT, wearables).  
-Cortex-X: Versiones "customizadas" para máxima potencia (ej: Samsung Exynos).

### 5. ¿Qué ventajas ofrece el set de instrucciones Thumb-2?
-Mejor densidad de código: Combina instrucciones de 16 bits (Thumb) y 32 bits (ARM), reduciendo el tamaño del programa.  
-Rendimiento mejorado: Permite operaciones complejas sin sacrificar eficiencia.

### 6. ¿Por qué es relevante la comunidad ARM?
-Estandarización: Define arquitecturas compatibles en múltiples fabricantes (NVIDIA, Qualcomm, Apple).  
-Innovación colaborativa: Empresas contribuyen con extensiones (ej: NEON para SIMD).  
-Soporte global: Herramientas de desarrollo (Keil, GCC) y sistemas operativos (Linux, FreeRTOS).

### 7. ¿Qué características distinguen al ARM Cortex-M4?
-Unidad de punto flotante (FPU) opcional: Para cálculos en coma flotante de precisión simple.  
-Instrucciones DSP: Optimizadas para procesamiento digital de señales (ej: filtros, FFT).  
-Bajo consumo: Ideal para IoT y dispositivos portátiles.  
-Núcleo de 32 bits con arquitectura Harvard modificada.

## 8. ¿Qué tipos de registros básicos se encuentran en la arquitectura ARM Cortex-M?
-Registros de propósito general (R0-R12): Almacenan datos temporales.  
-Stack Pointer (SP): R13, gestiona la pila.  
-Link Register (LR): R14, guarda la dirección de retorno en llamadas a funciones.  
-Program Counter (PC): R15, indica la próxima instrucción.  
-Registros especiales: APSR (estado), CONTROL (modo de operación).

### 9. ¿Para qué se utilizan los modos Thread y Interrupt en ARM Cortex-M?
-Modo Thread: Ejecución normal del programa (sin privilegios).

-Modo Interrupt: Se activa durante interrupciones o excepciones (con privilegios de acceso completo).
Esto mejora la seguridad: el código de usuario no puede acceder a recursos críticos directamente.

### 10. ¿En qué consiste el mapa de memoria de 4 GB en Cortex-M?

Sistema (0xE0000000 - 0xFFFFFFFF): Funciones del núcleo (NVIC, SysTick).
Permite acceso unificado y seguro a todos los recursos del sistema.