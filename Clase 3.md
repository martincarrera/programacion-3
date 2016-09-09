19) Pseudocodigo no recursivo donde dadas dos secuencias S1 y S2 ordenadas, devolver una secuencia ordenada con los elementos de ambas.

```
Algoritmo
 Merge
Entrada
 Secuencia S1 de Numeros enteros ordenada
 Secuencia S2 de Numeros enteros ordenada
Salida
 Secuencia S3 de Numeros enteros ordenada

Pseudocodigo
  i1 <-- 1
  i2 <-- 1
  S3 <-- []
  mientras (i1 <= #S1) y (i2 <= #S2)
    si(S1[i1] <= S2[i2])
      S3 <-- S3 + [ S1[i1] ]
      i1 <-- i1 + 1
    sino
      S3 <-- S3 + [ S2[i2] ]
      i2 <-- i2 + 1
    fin si
  fin mientras
  S3 <-- S3 + S1[i1 .. infinito]
  S3 <-- S3 + S2[i2 .. infinito]
  devolver S3
```

### Merge-Sort

* St: Una secuencia de un elemento esta ordenada.
* Div: A la mitad, igual que en la busqueda binaria.
* Un: Merge.

20) Pseudocodigo del Merge-Sort

```
Algoritmo
 MergeSort
Entrada
 Secuencia S1 de Numeros enteros
 Algoritmo Merge
Salida
 Secuencia S de Numeros enteros ordenada
Pseudocodigo
  si (#S1 == 1)
   devolver (S1)
  sino
   S1 <-- MergeSort(S[1 .. (#S / 2)])
   S2 <-- MergeSort(S[(#S/2) .. #S])
   devolver Merge(S1, S2)
  fin si
```

21) Formula partida del Tarda del Merge-Sort

```
T(n) => Cst                   Si n = 1
        2T(N/2) + Cdiv + N    Si n > 1
```

22) Desarrollar 3 terminos de la induccion

```
T0(N) = 2 * T1(N/2) + Cdiv + N
      = 2 * (2 * T2(N/4) + Cdiv + N/2) + Cdiv + N
      = 4 * T2(N/4) + 3Cdiv + 2N
      = 4 * (2 * T3(N/8) + Cdiv + N/4) + 3Cdiv + 2N
      = 8 * T3(N/8) + 7Cdiv + 3N
      .
      .
      .
      = 2^K * TK (N/2^K) + (2^K - 1) Cdiv + KN
      
      N = 2^K => log2(N) = K
      
      = N * TK(1) + (N - 1) Cdiv + N * log2(N)
      = N * Cst + (N - 1) Cdiv + N * log2(N)
      => O(N * log2(N))
```

23) Completar la induccion y demostrar la complejidad

### Quick-Sort

* St: Una secuencia vacia esta ordenada
* Div: Dado el primer elemento de una secuencia llamado pivot, armamos dos secuencias con los mayores y los menores.
* Union: Concateno menores + [pivot] + mayores

```
Algoritmo
 QuickSort
Entrada
 Secuencia S de Numeros enteros
Salida
 Secuencia S2 de Numeros enteros ordenada
Pseudocodigo
  menores <-- []
  mayores <-- []
  si (#S == 0)
   devolver S
  fin si
  pivot <-- S[1]
  para cada el en S[2 .. infinito]
   si (el < pivot)
    menores <-- menores + el
   sino
    mayores <-- mayores + el
   fin si
  fin para
  mayores <-- QuickSort(mayores)
  menores <-- QuickSort(menores)
  devolver menores + [pivot] + mayores
```

25) Formula del Tarda del QS considerando que quedan todos de un lado y ninguno del otro

```
T(n) => Cst                      Si n = 0
        T(N - 1) + Ndiv + Cun    Si n > 0
        
T0(N) = T1(N - 1) + N + Cun
      = T2(N - 2) + (N - 1) + Cun + N + Cun
      = T2(N - 2) + N + (N - 1) + 2 * Cun
      = T3(N - 3) + N + (N - 1) + (N - 2) + 3 * Cun
      .
      .
      .
      = TK(N - K) + (N) + (N - 1) + ... + (3) + (2) + (1) + K * Cun
      
      T(N - K) = T(0) => N - K = 0 => N = K
      
      T0(N) = T(0) + 1 + 2 + 3 + ... + N + N*Cun
      T0(N) = Cst + (N^2) / 2 + N / 2 + N * Cun
      
      => O(n^2) = Cuadratica
```
