# Llamadas a funciones

En lenguaje C
```C
sum(a, b);
int sum(int x, int y){
    return x + y;
}
```
En RISC-V
```verilog 
1000    add     a2,s0,x0    # x = a
1004    add 
```

* Instrucción simple para saltar y guardar una dirección: saltar y enlaza (_jump and link_) __jal__.
    * Antes:
    ```verilog
    1008    addi    ra,x0,1016  # ra = 1016

    ```
    * Despues:
    ```verilog
    
    ```
* Sintaxis para __jal__ 

* En general, se necesita salvar informacion extra además de __ra__
* Cuando se corre un programa en C existen 3 áreas de memoria

## Utilizando la Pila
* El registro __sp__ siempre apunta a la última localidad de la pila.
* Para utilizar la memoria de pila, se decrementa este apuntador por una cantidad del espacio que se necesita 

Compilando a mano:
```verilog
main:
    500     add     t0,t1,t2
    504     jal     x1,SumaCuadrada
    508     sub     t0,t1,t2
SumaCuadrada:
    1004    addi    sp,sp,-8    # hace espacio en la pila para 8 bytes
    1008    sw      ra,4(sp)    # guarda ra -la direccion de regreso-
    1012    sw      a4,0(sp)    #guarda a4 -contenido del registro-
    1016    add
```

Pseudocodigo
```C
for(i = 0; i < N; i++)
    for(j = 0; i < N; j++)
        if(A[i] > A[j])
        {
            temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
```
Ensamblador:
```verilog
addi    s0,x0,0     # i = 0
addi    s2,x0,6     # N = 6
addi    s1,x0,0     # j = 0
```

## Temas de exposicion
* 1.1
* 1.2 y 5.1
* 1.3 y 4.1
* 2.1 y 5.6
* 4.2 y 2.3 
* 2.2 y 4.3


> __Recordatorio__ : 