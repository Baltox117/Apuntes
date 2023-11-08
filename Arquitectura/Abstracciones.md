# Abstracciones

## Realidad importante #1
Los números enteros (_int_) no son enteros, los números de punto flotante (_float_) no son reales, por ejemplo:
- ¿Es x^2 >= 0
    - Con _float_ -> __Si__
    - Con _int_   -> __??__
        - 04000*04000 -> 0016,000,000 = 0X000F42400 = 0000-0000-1111-0100-0010-0100-0000-0000
        - 90000*90000 -> 8,100,000,000 = 0X1E2CC3100 = 0001-1110-0010-1100-1100-0011-0001-0000-0000
- Es (x + y) + z = x + (y + z)
    - Con _signed int_ & _unsigned int_ -> __Si__
    - Con _float_ -> __??__
        - (1e20 + -1e20) + 3.14 -> 3.14
        - 1e20 + (-1e20 + 3.14) -> ??

## Aritmética computacional

- No debe generar valores aleatorios:
    - Las operaciones aritmeticas tienen propiedades matemáticas importantes
- No se pueden asumir propiedades "usuales":
    - Debido a la exactitud de as representaciones (Registros)
    - Las operaciones con enteros satisfacen las propiedades de un "anillo"
        - Conmutatividad, asociatividad y distributividad
    - Las operaciones de punto flotante satisfacen las propiedades de "orden"
        - Monotocidad (conservan el orden), valores de signo
            - _f_ es monótona para toda x < y si f(x) < f(y)
- Observaciones:
    - Se necesita entender qué abstracciones aplicar dependiendo del contexto
    - Es un tema importante para programadores de compiladores y programadores de aplicaciones serias

## Realidad importante #2 

¿Se tiene que saber ensamblador?

En general, las oportunidades de nunca escribir un programa en ensamblador son grandes:
- Los compiladores son mucho mejores y más pacientes de lo que son las personas

Sin embargo, entender el lenguaje ensambladore es clave para ejecutar modelos a nivel máquina:
- Para entender el comportamiento de programas en precencia de errores
    - Se analizan el Modelo de lenguaje de alto
- Para ajustar el desempeño del programa
    - Entender las fuentes de ineficiencia del programa
- Implementando software de sistemas
    - Los compiladores tienen código máquina como objetivo
    - LOs sistemas operativos deben administrar el estado del proceso