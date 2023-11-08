# Analizadores Sintácticos
Los Analizadores Sintácticos determinan si una cadena "sigma" pertenece a un lenguaje L.

Los lenguajes los definiremos por medio de Gramáticas. Utilizaremos gramáticas libres del contexto.

### Recordatorio
Una gramática G es una 4-tupla G

__G(Vt, Vn, S, θ)__

Donde:
* _Vt_ : Conjunto finito no vacio de elementos, llamados simbolos terminales.
* _Vn_ : Conjunto finito no vacio de elementos, llamados simbolos no terminales.
* _S ∈ Vn_ : Simbolo no terminal llamado simbolo inicial de la gramática.
* _θ_ : Conjunto finito no vacio de relaciones llamados reglas gramaticales.

Para gramáticas libres del contexto

_θ_ : Vn --> (Vn ∪ Vt)*

__Clasificacion de Chomsky__
1. Irrestrictas
2. Sensibles al contexto
3. Libres de contexto 
4. Regulares

__Ejemplo__ : Gramática de las expresiones regulares
* _Vt_ = {+,-,*,(,),num}
* _Vn_ = {E,T,F}
* _S_ = E
* _θ_ = {E -> E + T,
         E -> E - T,
         E -> T,
         T -> T * F,
         T -> T / F,
         T -> F,
         F -> (E),
         F -> num}
* _θ_ = {E -> E + T | E - T | T,
         T -> T * F | T / F | F,
         F -> (E) | num}
         