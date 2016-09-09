### Division y Conquista (algoritmos recursivos)

Va dividiendo al problema hasta llegar hasta la solucion trivial.

Dado un problemea lo divido sucesivamente en subproblemas hasta que estos sean tan pequeños que se resuelven directamente (solucion trivial).

Luego voy combinando (union) las distintas soluciones a subproblemas hasta obtener l solucion final.

Los componentes son:

* Solcion trivial(st): cuando tenemos un problema tan pequeño que resolvemos directamente. SIEMPRE EN EL CASO BASE. Ej: ordenar un secuencia de un solo elemento.
* Division(div): consiste en dividir un problema en dos o mas subproblemas de igual naturaleza Ej: dada una secuecia divido en los mayores y los menores a un valor.
* Union(un): combino las soluciones a subproblemas.

10) Completar con sus palabras las componentes ST,DIV y UN de la busqueda binaria.

* ST: Elemento unico encontrado - El elemento buscado es igual al encontrado.
* DIV: dividir la secuencia a la mitad y tomo la secuencia donde esta el elemento.
* UN: no hay.

11) Pseudocodigo recursivo de la busqueda binaria.

```
Algoritmo
 Busqueda Binaria
Entrada
 Secuencia S de Numeros enteros ordenada
 Numero N a buscar
Salida
 Verdadero o falso

Pseudocodigo
  si (#S == 1)                                          Cst
    devolver (S[1] == N)                                Cst
  sino
    si (S[(#S / 2)] >= N)                               Cdiv
      devolver(BusquedaBinaria(S[1 .. (#S / 2)]), N)    Cdiv
    sino
      devolver(BusquedaBinaria(S[(#S/2) + 1 .. #S]), N) Cdiv
    fin si
  fin si
```

### Induccion

```
T(n) => Cst               Si n = 1
        T(n/2) + Cdiv     Si n > 1
```

Ejemplo

```
T(4) = T(2) + Cdiv = T(1) + Cdiv + Cdiv = Cst + Cdiv + Cdiv
```

12) Desarrollar la T para N = 256

```
T0(256) = T1(128) +     Cdiv 
        = T2(64)  + 2 * Cdiv 
        = T3(32)  + 3 * Cdiv
        = T4(16)  + 4 * Cdiv 
        = T5(8)   + 5 * Cdiv
        = T6(4)   + 6 * Cdiv
        = T7(2)   + 7 * Cdiv 
        = T8(1)   + 8 * Cdiv
        = Cst    + 8 * Cdiv
```

Conclusiones

```
K = Nivel maximo de recursividad. En este caso: 8
1 vez Cst
8 veces Cdiv
Igual K que cantidad de Cdiv
2^K = N
K = Log2(N)
```

### Metodo por induccion

13) Desarrollar 3 terminos mas de la induccion

```
T(N) = Cst            si N = 1
       T(N/2) + Cdiv  si N > 1

T0(N) = T1(N/2)  +     Cdiv
      = T2(N/4)  + 2 * Cdiv 
      = T3(N/8)  + 3 * Cdiv
      = T4(N/16) + 4 * Cdiv
      = ...
      = Tk(N/2^k) + K * Cdiv
      = Tk(1) + K * Cdiv

N/2^k = 1    => 2^K = N   => K = log2(N)

     = Cst + log2(n) * Cdiv

O(log(n)) => Logaritmico
```

### Division y conquista: Algoritmo "esta ordenado"

* ST: Una secuencia elemental esta siempre ordenada.
* DIV: Por la mitad igual que en la Busqueda Binaria.
* UN: Si ambos subproblemas estan ordenados, comparo el ultimo valor de la primer secuencia con el primero de la segunda secuencia.

14) Pseudocodigo recursivo "Esta ordenado"


```
Algoritmo
 Esta Ordenado (EO)
Entrada
 Secuencia S de numeros
Salida
 Verdadero o falso

Pseudocodigo
 si #S == 1                                                 Cst
  devolver verdadero                                        Cst
 fin si
 si (EO(S[1 .. (#S / 2)]) && (EO(S[(#S / 2) + 1 .. #S])))   Cdiv (divisiones) + X
  devolver (S[(#S / 2)] <= S[(#S / 2) + 1])                 Cun
 sino
  devolver falso                                            Cun
 fin si
```

15) Formula partida del tarda para el ejercicio 14.

```
T(N) = Cst                        si N = 1
       2 * T(N/2) + Cdiv + Cun    si N > 1
```

16) Desarrollar la T para N = 128 y contar cuantos DIV, ST y UN se hacen y determinar el K.

```
T0(128) = 2 * T1(64) + Cdiv + Cun
        = 2 * (2 * T2(32) + Cdiv + Cun) + Cdiv + Cun
        = 4 * T2(32) + 3Cdiv + 3Cun
        = 4 * (2 * T3(16) + Cdiv + Cun) + 3Cdiv + 3Cun
        = 8 * T3(16) + 11Cdiv + 11Cun
        = 8 * (2 * T4(8) + Cdiv + Cun) + 7Cdiv + 7Cun
        = 16 * T4(8) + 19Cdiv + 19Cun
        = 16 * (2 * T5(4) + Cdiv + Cun) + 15Cdiv + 15Cun
        = 32 * T5(4) + 35Cdiv + 35Cun
        = 32 * (2 * T6(2) + Cdiv + Cun) + 31Cdiv + 31Cun
        = 64 * T6(2) + 67Cdiv + 67Cun
        = 64 * (2 * T7(1) + Cdiv + Cun) + 63Cdiv + 63Cun
        = 128 * Cst + 127Cdiv + 127Cun
        
 K = 7
 O(N) = Lineal
```

17) Desarrolle 3 terminos del desarrollo inductivo

```
T(N) = Cst                        si N = 1
       2 * T(N/2) + Cdiv + Cun    si N > 1
       
T0(N) = 2 * T1(N/2) + Cdiv + Cun
      = 4 * T2(N/4) + 3Cdiv + 3Cun
      = 8 * T3(N/8) + 7Cdiv + 7Cun
      = 16 * T4(N/16) + 15Cdiv + 15Cun
      .
      .
      .
      = 2^K * TK(1) + (2^K - 1) * (Cdiv + Cun)
      = N * Cst + (N - 1) * (Cdiv + Cun)
      => O(n) = Lineal
```

Tarea:

1) Completar la induccion del Esta Ordenado y determinar la complejidad.

2) Codificar en java y contar empiricamente cuantas ST, DIV, UN y K se ejecuta para n = 4096
* Legajo Par:
 * Busqueda Binaria
* Legajo Impar:
 * Esta Ordenado
