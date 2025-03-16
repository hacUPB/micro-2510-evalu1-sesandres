## Control de Frecuencia de Parpadeo con Listas y SysTick

A continuacion se muestra el codigo el cual enciende los 2 leds disponibles en el microprocesador a diferentes frecuencias.

```
.syntax unified
.global _start
.text
.thumb_func
/* Definiciones de direcciones y offsets */
.equ RCC_BASE, 0x40023800        /* Dirección base del RCC */
.equ RCC_AHB1ENR_OFFSET, 0x30    /* Offset del registro RCC_AHB1ENR */
.equ GPIOA_BASE, 0x40020000      /* Dirección base de GPIOA */
.equ GPIOA_MODER_OFFSET, 0x0     /* Offset del registro MODER */
.equ GPIOx_OTYPER_OFFSET, 0x4    /* Offset del registro OTYPER */
.equ GPIOx_OSPEEDR_OFFSET, 0x08  /* Offset del registro OSPEEDR */
.equ GPIOx_PUPDR_OFFSET, 0x0C    /* Offset del registro PUPDR */
.equ GPIOx_ODR_OFFSET, 0x14      /* Offset del registro ODR */
_start:
   /* 1. Habilitar el reloj para GPIOA */
   LDR R0, =RCC_BASE
   LDR R1, [R0, #RCC_AHB1ENR_OFFSET]
   ORR R1, R1, #0x01             /* Habilita GPIOA */
   STR R1, [R0, #RCC_AHB1ENR_OFFSET]
   /* 2. Configurar PA6 (D2) y PA7 (D3) como salidas */
   LDR R0, =GPIOA_BASE
   LDR R1, [R0, #GPIOA_MODER_OFFSET]
   BIC R1, R1, #(0b11 << 12 | 0b11 << 14) /* Limpia bits PA6 y PA7 */
   ORR R1, R1, #(0b01 << 12 | 0b01 << 14) /* Modo salida (01) */
   STR R1, [R0, #GPIOA_MODER_OFFSET]
   /* 3. Configurar como push-pull */
   LDR R1, [R0, #GPIOx_OTYPER_OFFSET]
   BIC R1, R1, #(0b1 << 6 | 0b1 << 7)      /* Push-pull para PA6 y PA7 */
   STR R1, [R0, #GPIOx_OTYPER_OFFSET]
   /* 4. Velocidad alta */
   LDR R1, [R0, #GPIOx_OSPEEDR_OFFSET]
   ORR R1, R1, #(0b11 << 12 | 0b11 << 14) /* Alta velocidad */
   STR R1, [R0, #GPIOx_OSPEEDR_OFFSET]
   /* 5. Sin pull-up/pull-down */
   LDR R1, [R0, #GPIOx_PUPDR_OFFSET]
   BIC R1, R1, #(0b11 << 12 | 0b11 << 14)
   STR R1, [R0, #GPIOx_PUPDR_OFFSET]
   /* Contadores para los LEDs */
   MOV R2, #0                   /* Contador D2 */
   MOV R3, #0                   /* Contador D3 */
loop:
   BL espera_100ms               /* Base de tiempo: 100ms */
   /* Manejo de D2 (PA6) - Toggle cada 500ms (5 intervalos) */
   ADD R2, #1
   CMP R2, #5
   BLT skip_d2
   LDR R0, =GPIOA_BASE
   LDR R1, [R0, #GPIOx_ODR_OFFSET]
   EOR R1, R1, #(1 << 6)        /* Invierte PA6 */
   STR R1, [R0, #GPIOx_ODR_OFFSET]
   MOV R2, #0
skip_d2:
   /* Manejo de D3 (PA7) - Toggle cada 300ms (3 intervalos) */
   ADD R3, #1
   CMP R3, #3
   BLT skip_d3
   LDR R0, =GPIOA_BASE
   LDR R1, [R0, #GPIOx_ODR_OFFSET]
   EOR R1, R1, #(1 << 7)        /* Invierte PA7 */
   STR R1, [R0, #GPIOx_ODR_OFFSET]
   MOV R3, #0
skip_d3:
   B loop
/* Subrutina de retardo de 100ms */
espera_100ms:
   LDR R6, =1600000             /* Ajuste para 100ms */
   MOV R7, #0
1:
   ADD R7, #1
   CMP R7, R6
   BLT 1b
   BX LR

 ```