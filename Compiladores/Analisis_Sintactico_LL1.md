# Analisis Sintáttico LL1

Es un analizador descendente. 

Significado de LL1
- __L__ : La cadena de entrada se analiza de izquierda (L) a derecha.
- __L__ : Se genera una dericación por la izquierda(L)
- __1__ : Solamete se requiere 1 token para determinar la regla gramatical a aplicar

_Analizador Predictivo_

## Operaciones para crear un analizador LL1

Consideremos la siguiente gramatica: 
* A -> E
* E -> TE'
* E'-> +TE' | -TE' | "Epsilon"
* T -> FT'
* T'-> *FT' | /FT' | "Epsilon"
* F -> (E) | num

σ1 = num *(num + num)

σ2 = FT' E' ; E -> TE' -> FT' E'

### Operacion First

Dada una cadena σ el _First(σ)_ es el conjunto de los simbolos terminales , con los que inician las derivaciones de σ. ∈ ∈ First(σ) <-> σ = ∈


#### Nota 
Verificar si mi alfa es el ultimo y tiene epsilon
Considerar la condicion para cuando epsilon esta en el first ()

### Operacion Follow

Esta operacion recibe como argumento un simbolo no terminal. Si A es el simbolo inicial de G entonces $ ∈ Follow(A)

> _$_ es el fin de cadena

- G -> Reglas99
- /* Reglas -> Regla | Reglas Regla
- Regla -> LadoIzquierdo Flecha LadosDerechos
- LadoIzquierdo -> Simbolo
- /* LadosDerechos -> LadoDerecho | Lados OR LadoDerecho
- LadoDerecho -> SecSimbolos
- /* SecSimbolos -> Simbolo | SecSimbolos Simbolo

## Descenso Recursivo 

Gramatica de gramaticas(sin recurcion por la izquierda):

- G -> Reglas
- Reglas -> Regla Reglas' 
- Reglas' -> Regla Reglas' | ∈
- Regla -> LadoIzquierdo FLECHA LadosDerehos
- LadoIzquierdo -> SIMBOLO
- LadosDerechos -> LadoDerecho LadosDerechos'
- LadosDerechos' -> OR LadoDerecho LadosDerechos' | ∈
- LadoDerecho -> SecSimbolos
- SecSimbolos -> SIMBOLO SecSimbolos'
- SecSimbolos' -> SIMBOLO SecSimbolos' | ∈


```java
bool G(){
    return Reglas();
}

bool Reglas(){
    if(Regla())
        if(ReglasP())
            return true;
    return false;
}

bool ReglasP(){
    EdoAnalizLexic v = new EdoAnalizLexic();
    Lexic.getEdo(v);
    if (Regla())
        if (ReglasP())
            return true;
        else
            return false;
    Lexic.setEdo(v);
    return true;
}

bool Regla(){
    int Token;
    Token = Lexic.yylex();
    if (Token == SIMBOLO){
        Token = Lexic.yylex();
        if (Token == FLECHA)
            if (LadosDerechos())
                return true;
    }
    return false;
}

bool LadosDerechos(){
    if (LadoDerecho())
        if (LadosDerechosP())
            return true;
    return false;
}

bool LadosDerechosP(){
    int Token;
    Token = Lexic.yylex();
    if (Token == OR){
        if (LadoDerecho())
            if (LadosDerechosP())
                return true;
        return false;
    }
    Lexic.UndoToken();
    return true;
}

bool LadoDerecho(){
    if (SecSimbolos())
        return true;
    return false;
}

bool SecSimbolos(){
    int Token;
    Token = Lexic.yylex();
    if (Token == SIMBOLO)
        if (SecSimbolosP())
            return true;
    return false;
}

bool SecSimbolosP(){
    int Token;
    Token = Lexic.yylex();
    if (Token == SIMBOLO){
        if (SecSimbolosP)
            return true;
        return false;
    }
    Lexic.UndoToken();
    return true;
}
```
Vt = {_SIMBOLO_, _FLECHA_, _OR_}


<table>
    <tr>
        <td>Clase Lexica</td>
        <td>Expreción regular</td>
        <td>Token</td>
    </tr>
    <tr>
        <td>SIMBOLO</td>
        <td>([a-z][A-Z])&([a-z]|[A-Z]|[0-9]|_)^*</td>
        <td>10</td>
    </tr>
    <tr>
        <td>FLECHA</td>
        <td>- & ></td>
        <td>20</td>
    </tr>
    <tr>
        <td>OR</td>
        <td>|</td>
        <td>30</td>
    </tr>
    <tr>
        <td>Espacio</td>
        <td>( )^+</td>
        <td>ERROR</td>
    </tr>
</table>


#### Gramatica de Gramaticas con punto y coma (PC)

- G -> Reglas
- Reglas -> Regla PC Reglas' 
- Reglas' -> Regla PC Reglas' | ∈
- Regla -> SIMBOLO FLECHA LadosDerehos
- LadosDerechos -> LadoDerecho LadosDerechos'
- LadosDerechos' -> OR LadoDerecho LadosDerechos' | ∈
- LadoDerecho -> SecSimbolos
- SecSimbolos -> SIMBOLO SecSimbolos'
- SecSimbolos' -> SIMBOLO SecSimbolos' | ∈

### Tabla para acciones semanticas

```C#
bool G(){
    if(Reglas())
        return true;
    return false:
}

bool Reglas(){
    int Token;
    if(Regla()){
        Token = Lexic.yylex();
        if(Token == PC)
            if(ReglasP())
                return true;
    }
    return false;
}

bool ReglasP(){
    EdoAnalizador EdoAnaliz = new EdoAnalizador();
    int Token;
    Lexic.getEdoAnalizador(EdoAnaliz);
    if(Regla()){
        Token = Lexic.yylex();
        if(Token == PC)
            if(ReglasP)
                return true;
            return false;
    }
    Lexic.setEdo(EdoAnaliz);
    return true;
}

bool Regla(){
    int Token;
    String LadoIzq;
    Token = Lexic.yylex();
    if(Token == SIMBOLO){
        LadoIzq = Lexic.yytext();
        Token = Lexic.yylex();
        if(Token == FLECHA)
            if(LadosDerechos(ref LadoIzq))
                return true;
        return false;
    }
    return false;
}

bool LadosDerechos(ref String LadoIzq){
    Lista <Simbolos> L = new Lista <Simbolos>();
    if(LadoDerecho(LadoIzq, L)){
        ArrReglas[NumReglas].Simb = LadoIzq;
        ArrReglas[NumReglas].esTerminal = false;
        ArrReglas[NumReglas].ListaSimb = L;
        NumReglas ++;
        if(LadosDerechosP(LadoIzq))
            return true;
    }
    return false;
}

bool LadosDerechosP(ref String LadoIzq){
    int Token;
    Lista <Simbolos> L = new Lista <Simbolos>();
    Token = Lexic.yylex();
    if(Token == OR){
        if(LadoDerecho(L)){
            ArrReglas[NumReglas].Simb = LadoIzq;
            ArrReglas[NumReglas].esTerminal = false;
            ArrReglas[NumReglas].ListaSimb = L;
            NumReglas ++;
            if(LadosDerechosP(LadoIzq))
                return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}

bool LadoDerecho(Lista <Simbolos> L){
    if(SecSimbolos(L))
        return true;
    return false;
}

bool SecSimbolos(Lista <Simbolos> L){
    int Token;
    String Simb;
    Simbolo Nodo;
    Token = Lexic.yylex();
    if(Token == SIMBOLO){
        Nodo = new Simbolo(Lexic.yytext, true);
        L.count = 0;
        if(SecSimbolosP(L)){
            L.Add(Nodo,0);
            return true;
        }
        return false;
    }
    return false;
}

bool SecSimbolosP(Lista <Simbolos> L){
    int Token;
    String Simb;
    Simbolo Nodo;
    Token = Lexic.yylex();
    if(Token == SIMBOLO){
        Nodo = new Simbolo(Lexic.yytext, true);
        if(SecSimbolosP(L)){
            L.Add(Nodo, 0);
            return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}
```

> Nota: Definir en la clase del analizador sintactico
>   1. El arreglo de reglas
>   2. El contador de arreglos
>   3. Conjunto de No Terminales
>   4. Conjunto de Terminales