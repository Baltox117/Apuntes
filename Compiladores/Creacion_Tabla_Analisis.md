# Creación de la Tabla de Análisis LL1

Consideremos la gramática : 
* E -> TE'
* E'-> +TE' | -TE' | "Epsilon"
* T -> FT'
* T'-> *FT' | /FT' | "Epsilon"
* F -> (E) | num

Enumeramos las reglas
1. E -> TE'
2. E'-> +TE'
3. E'-> -TE'
4. E'-> "∈"
5. T -> FT'
6. T'-> *FT'
7. T'-> /FT'
8. T'-> "∈"
9. F -> (E)
10. F -> num

Numeramos las reglas, la tabla LL1 tendra como renglones a los simbolos _no terminales_, _terminales_ y a _$_.

Vn = {E, E', T, T', F}

Vt = {+, -, *, /, (, ), num}

|   | + | - | * | / | ( | ) |num| $ |
| E |   |   |
| E'|   |   |
| T |
| T'|
| F |
| + |
| - |
| * |
| / |
| ( |
| ) |
|num|
| $ |

Ahora analizamos cada regla
1. E -> TE'
    - Se calcula el first del lado derecho 
    
    First(TE') = {(, num}

    Tabla[E, {(, num}] = TE', 1
2. E' -> +TE'

    First(+TE') = { + }

    Tabla[E', {+}] = +TE', 2
3. 




## 

Una gramática es LL1 si se puede crear su tabla de anlaisis LL1 sin ambigüedades. Sea _G_ una grámatica, entonces la tabla T LL1 de _G_ se define como: 

T(α,β){
    pop Si α = β y α ∈ Vt
    
    "Gamma", i Si α ∈ Vn, α -> "Gamma" es la regla #i y β ∈ first("Gamma") - {∈}

    "Gamma", i Si α ∈ Vn, α -> "Gamma" es la regla #i, ∈ ∈ first("Gamma") y β ∈ follow(α)

    Donde α, β ∈ Vn U Vt U {$}
}

Representación de una gramática para calcular first y follow.

Considerando la gramática:


> Nota: libros de algoritmos