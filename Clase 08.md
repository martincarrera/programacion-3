## Backtracking para optimizacion.

### Problema del cambio
```
S = Secuencia de denominaciones de billetes
```

Ej:

```
S[500, 100, 50, 20, ... ]
C = Monto a cambiar
```
48) Tabla de dominio

| | C<0 | C=0 | C>0 |
|:---:|:---:|:---:|:---:|
|#S=0|+inf|0|+inf|
|#S>0|+inf|0|CALCULAR|

49) Formula



50) Pseudocodigo

51) Fibonacci

52) Completar arbol

53) Complejidad Mochila

```
T(N) = C                      si n = 0
       2 * T(N - 1) + C       si n > 0


T(N) = 2 * T(N - 1) + C
     = 2 * (2 * T(N - 2) + C) + C
     = 4 * T(N - 2) + 3C
     .
     .
     .
T(K) = 2^K * T(N - K) + (2^K - 1) * C

     => N - K = 0 => N = K

     = 2^N * T(0) + (2^N - 1) * C
     = 2^N * C + (2^N - 1) * C

    O(N) = 2^N => Exponencial

```

54) Desarrollar un Fibonacci no recursivo que llene una secuencia los primeros 2 valores con 1, y el resto de los elementos con un para. Devolver la ultima posicion.

```
Algoritmo
  Fibonacci Secuencial
Entrada
  Numero N
Salida
  Numero F
Pseudocodigo
  S <-- []
  S[1] <-- 1
  S[2] <-- 1
  para cada num entre 3 y N
    S[num] = S[num-1] + S[num-2]
  fin para
  devolver S[N]

```

### Mochila

```
Mochila(S, C) = 0               C = 0
              = - inf           C < 0
              = 0               C > 0 y #S = 0
              = MAX(Mochila(S[2.. inf], C), S[1].g + Mochila(S[2 .. inf], C - S[1].p))   C > 0 y #S > 0
```

| | 0 | 1 | 2 | 3 | 4 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| [] | 0 | 0 | 0 | 0 | 0 |
| [(Mujer, p: 1, g: 10)] | 0 | M([M], 1) = Max(M([], 1), 10 + M[], 0) = Max(0, 10) = 10 (Llevo mujer) | M([M], 1) = Max(M([], 1), 10 + M[], 0) = Max(0, 10) = 10 (Llevo mujer) | | |
| [(Biografia, p: 1, g: 20), (Mujer, p: 1, g: 10)] | 0 | | | | |
| [(Negro WS, p: 2, g: 30), (Biografia, p: 1, g: 20), (Mujer, p: 1, g: 10)] | 0 | | | | |
