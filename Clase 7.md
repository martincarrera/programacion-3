## Backtracking para optimizacion.

### Pre: Programacion Dinamica

Volvamos al problema de la mochila... Ahora los elementos no se pueden partir.

Ejemplo:

```

S = [(Monedas, p: 3, gan: 3), (caliz, p: 6, gan: 7), (mujer, p:  5, gan: 4), (leon, p: 4, gan: 5)]
C = 10

Arbol de decision binario
(Ejemplo con 2 elementos)

```

Planteo del arbol de decision como formula con max

```

S = [(Corona, p: 3, gan: 3), (Totem, p: 3, g: 4)]
C = 5

Mochila(S, C) = Max( 3 + 1) Llevo mochila, 0 + 2) No llevo mochila) = Max(3 + Mochila([Totem, p:3, g:4], 2), 0 + Mochila([Totem, p:3, g:4], 5))

1) Mochila([Totem, 3, 4], 2) = Max(4 + Mochila([], -1), 0 + Mochila([], 2)) = Max(-inf, 0) = 0

2) Mochila([Totem, 3, 4], 5) = Max(4 + Mochila([], 2), 0 + Mochila([], 5)) = Max(4, 0) = 4

Mochila(S, C) = Max(3 + 0, 0 + 4) = 4

```

42) Resolver con: 

```

S = [(*, p: 3, gan: 2), (@, p: 2, g: 5)]
C = 5

Mochila(S, C) = Max(2 + Mochila([@, 2, 5], 2), 0 + Mochila([@, 2, 5], 5))

1) Mochila([@, 2, 5], 2) = Max(5 + Mochila([], 0), 0 + Mochila([], 2)) = Max(5, 0) = 5
2) Mochila([@, 2, 5], 5) = Max(5 + Mochila([], 3), 0 + Mochila([], 5)) = Max(5, 0) = 5

Mochila(S, C) = Max(2 + 5, 0 + 5) = 7

```

Tabla de dominio


| | C<0 | C=0 | C>0 |
|:---:|:---:|:---:|:---:|
|#S=0|-inf|0|0|
|#S>0|-inf|0|CALCULAR|

Formula

```
Mochila(S, C) = -inf                            si C < 0
                0                               si C = 0
                0                               si C > 0 y #S = 0
                Max(S[1].ganancia + Mochila(S[2 .. inf], C - S[1].peso), Mochila(S[2 .. inf], C)) si C > 0 y #S > 0
```

43) Traducir formula en pseudocodigo recursivo

```
Algoritmo
  Mochila
Entrada
  Secuencia S de elementos con peso y ganancia
  Numero C capacidad
Salida
  Numero M ganancia maxima
Pseudocodigo
  M <-- -inf
  si (C === 0) o (C > 0 y #S === 0)
    M <-- 0
  sino si (C > 0y #S > 0)
    M <-- Max(S[1].ganancia + Mochila(S[2 .. inf], C - S[1].peso), Mochila(S[2 .. inf], C))
  fin si
  devolver M
```

44) Formula del tarda considerando el N com la longitud de la secuencia

```
T(N) = C                      si n = 0
       2 * T(N - 1) + C       si n > 0
```

Tarea: Induccion de esa formula

```
T(N) = 2 * T(N - 1) + C
     = 2 * (2 * T(N - 2) + C) + C
     = 4 * T(N - 2) + 3C
     .
     .
     .
T(K) = 2^K * T(N - K) + (2^K - 1) * C
     
     N - K = 0 => N = K
     
     = 2^N * T(0) + (2^N - 1) * C
     = 2^N * C + (2^N - 1) * C
    
    O(N) = 2^N => Exponencial
```

45) Dado un almacenamiento de capacidad C y una secuencia de tamaños de archivos S, determinar el minimo espacio que me queda con la combinacion optima.

```
S = [3, 4, 5]
C = 8

```

||C < 0|C = 0|C > 0|
|:---:|:---:|:---:|:---:|
|#S = 0|+inf|0|C|
|#S > 0|+inf|0|CALCULAR|

```
  Almac(S, C) = + inf                     si C < 0
                0                         si C = 0
                C                         si C > 1 y #S = 0
                MIN(Almac(S[2 .. inf], C - S[1]), Almac(S[2 .. inf], C))  si C > 1 y #S > 0
```
