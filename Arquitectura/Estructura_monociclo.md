# Estructura Monociclo

Hoy en dia, la mayoria de los ISA emplean el modelo de von Neumann
- x86
- PDP-x: Programmed Data Processor(PDP-11)
- VAX
- IBM 360
- CDC 6600
- SIMD ISAs: CRAY-1, Connection Machine
- VLIW ISAs: Multiflow, Cydrome, IA-64(EPIC)
- PowerPC, POWER
- RISC ISAs: Alpha, SPARC, ARM, __MIPS__, __RISC-V__

¿Cuales son las diferencias fundamentales?
- E.g., cómo son especificadas las instrucciones y lo que cada una hace
- E.g., qué tan complejas son las instrucciones

## Arquitectura RISC-V

La Arquitectura RISC-V es reciente y es abierta. Tiene como objetivo convertirse en un ISA universal

ISA Estabel- El núcleo fundamental del ISA es llamado RV32I, el cúal puede ejecutar el stack de software completo. RV32I ésta congelado, es decir, nunca cambiará y por eso proove un objetivo estable para Desarrolladores de Compiladores, Sistemas Operativos y Programadores de Lenguaje Ensamblador.

ISA Modular- La modularidad viene de las extenciones opcionales estándar que el hardware puede incorporar de acuerdo a las necesidades de cada aplicación:
- RV32F (Punto flotante precisión simple)
-  