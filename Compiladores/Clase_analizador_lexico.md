# Clase Analizador Lexico
### Componentes
* AFD        (arreglo bidimensional)
* Sigma      (cadena a analizar)
* PosActual  (entero)
* IniLexema  (entero)
* FinLexema  (entero)
* PasoxEdoA  (booleano)
* Lexema     (string)
* Pila_P     (pila de enteros)

__Sigma__ = a + 2.78 *

* _a_ = IniLexema
* _*_ = FinLexema

__Pila_P__ : Tendra los indices que corresponden a la posicion actual en sigma al inicial al analisis de la cadena.

### Ejemplo

			 0 1 2 3 4 5 6 7 8 9 10  11  12
	Sigma = |4|7|+|1|6|.|2|*|(|4| - | 5 | ) |

	P = |	|	Los valores guardados en P sirven para realizar un "ctrl + z" en el proceso del analisis lexico
		-----	
		|	|	
		-----	
		|	|	
		-----	
		| 7 |	
		-----	Lo que hacemos es poner en posicion actual el valor del tipo de la pila 
		| 3 |
		-----
		| 2 |
		-----
		| 0 |

		int yylex() // Metodo que regresa el token que correspondd al lexema identificado