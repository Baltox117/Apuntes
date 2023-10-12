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
```java
bool A(String s)
{
    if(E(s))
        return true;
    return false;
}
bool E(String s)
{
    if(T(s))
        if(Ep(s))
            return true;
    return false;
}
bool Ep(String s)
{
    int Token;
    String s1;
    Token = Lexic.yylex();
    if(Token == MAS || Token == MENOS)
    {
        if(T(s1))
        {
            s = s + " " + s1 + " " (Token == MAS ? "+" : "-");
            if(Ep(s))
                return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}
bool T(String s)
{
    if(F(s))
        if(Tp(s))
            return true;
    return false;
}
bool Tp(String s)
{
    int Token;
    String s1;
    Token = Lexic.yylex();
    if(Token == PROD || Token == DIV)
    {
        if(F(s1))
        {
            s = s + " " + s1 + " " (Token == PROD ? "*" : "/");
            if(Tp(s))
                return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}
bool F(String s)
{
    int Token;
    Token = Lexic.yylex();
    switch(Token);
    {
        case PAR_I:
            if(E(s))
            {
                Token = Lexic.yylex();
                if(Token == PAR_D)
                    return true;
            }
            return false;
        case NUM:
            s = Lexic.yylex();
            return true;
    }
    return false;
}
```
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
```java
bool A(AFN f)
{
    if(E(f))
        return true;
    return false;
}
bool E(AFN f)
{
    if(T(f))
        if(Ep(f))
            return true;
    return false;
}
bool Ep(AFN f)
{
    int Token;
    AFN f1;
    Token = Lexic.yylex();
    if(Token == OR)
    {
        if(T(f1))
        {
            f.Union(f1);
            if(Ep(f))
                return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}
bool T(AFN f)
{
    if(C(f))
        if(Tp(f))
            return true;
    return false;
}
bool Tp(AFN f)
{
    int Token;
    AFN f1;
    Token = Lexic.yylex();
    if(Token == CONC)
    {
        if(C(f1))
        {
            f.Conc(f1);
            if(Tp(f))
                return true;
        }
        return false;
    }
    Lexic.UndoToken();
    return true;
}
bool C(AFN f)
{
    if(F(f))
        if(Cp(f))
            return true;
    return false;
}
bool Cp(AFN f)
{
    int Token;
    AFN f1;
    Token = Lexic.yylex();
    switch(Token)
    {
        case POSIT:
            f.CerrPos();
            return (Cp(f));
        case KLEEN:
            f.CerrKleen();
            return (Cp(f));
        case OPC:
            f.Opcional():
            return (Cp(f));
    }
    Lexic.UndoToken();
    return true;
}
bool F(AFN f)
{
    int Token;
    char simb1, simb2;
    Token = Lexic.yylex();
    switch(Token)
    {
        case PAR_I:
            if(E(f))
            {
                Token = Lexic.yylex();
                if(Token == PAR_D)
                    return true;
            }
            return false;
        case SIMB:
            f = new AFN(Lexic.yytext[0]);
            return true;
        case CORCH_I:
            Token = Lexic.yylex();
            if(Token == SIMB)
            {
                simb1 = Lexic.yytext[0];
                Token = Lexic.yylex();
                if(Token == GUION)
                {
                    Token = Lexic.yylex();
                    if(Token == SIMB)
                    {
                        simb2 = Lexic.yytext[0];
                        Token = Lexic.yylex();
                        if(Token == CORCH_D)
                        {
                            f = new AFN(simb1, simb2);
                            return true
                        }
                    }
                }
            }
            return false;
    }
    return false;
}
```