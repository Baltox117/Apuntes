# Convertidor de infijo a postfijo
Gramatica:
* A -> E
* E -> TE'
* E'-> +TE' | -TE' | "Epsilon"
* T -> FT'
* T'-> *FT' | /FT' | "Epsilon"
* F -> (E) | num

__Entrada__ = 2.8 + 4 -5 * 9 
__Salida__ = ((2.8) ((4 5 -) 9 *) +)

## Solucion

'''
print()
'''


## Obtener Un AFN a partir de una exprecion regular
Requerimos la gramatica para el lenguaje de las expresiones regulares (G1):
* A -> E
* E -> E _OR_ T | T
* T -> T _&_ C | C
* C -> C+ | C* | C? | F
* F -> [sim - simb] | simb | (E)

El arbol de derivacion para __[a - z] & ([a - z] | [0 - 9])*__ es:



## Quitamos la recursion a G1
G2: 
* A -> E
* E -> TE'
* E'-> _OR_ TE' | "Epsilon"
* T -> CT'
* T'-> _&_ CT' | "Epsilon"
* C -> FC'
* C'-> +C' | *C' | ?C' | "Epsilon"
* F -> (E) | simb | [simb - simb]

Apliquemos descenso recursivo para obtener el AFN asociado a una exprecion regular
```js
console.log("Hola mundo")
```