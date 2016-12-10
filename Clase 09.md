### Ejercicio tipo parcial

```
Algoritmo
  Ej
Entrada
  Secuencia S
Salida
  3
Pseudo
  res <-- 0
  si #S = 0
    res <-- 3 /* 1 */                 Cst
  sino
      para cada e en S
        res <-- res + e /* 2 */       N
      fin para
      res <-- Ej(S[2 .. inf])         T(N-1)
  fin si
  devolver res
```

1) Induccion

```
Tarda(N) =  Cst                    si #S = 0
            N + T(N - 1) + Cdiv    si #S > 0
            
T0(N) = N + T1(N - 1) + Cdiv
     = N + (N - 1 + T2(N - 2) + Cdiv) + Cdiv
     = N + N - 1 + T2(N - 2) + 2*Cdiv
     .
     .
     .
     = (N * (N + 1) / 2 ) + Tk(N - K) + K * Cdiv
     => K = N
     = (N * (N + 1) / 2 ) + Cst + N * Cdiv
     
T(N) = (N * (N + 1) / 2 ) + Cst + N * Cdiv
     => N^2 / 2 + N * (Cdiv + 1/2) + Cst
     => O(N^2)
```

2) Cuantas veces se ejecuta *1* para n = 1024

```
T(N) = (N * (N + 1) / 2 ) + Cst + N * Cdiv
     *1* = Cst
     => La parte 1 se ejecuta 1 sola vez para cualquier n.
```

3) Cuantas veces se ejecuta *2* para n = 32

```
T(N) = (N * (N + 1) / 2 ) + Cst + N * Cdiv

     *2* = (N * (N + 1) / 2 )
     
     => La parte 2 se ejecuta 32 * (32 + 1) / 2 veces, o sea 528 veces.
```

4) Cuantas veces se ejecuta *3* para n = 4096

```
T(N) = (N * (N + 1) / 2 ) + Cst + N * Cdiv
     
     *3* = (N * Cdiv)
     => La parte 3 se ejecuta 4096 veces

```

7 de la guia) Ana trabaja en una empresa de comunicaciones. Le han encargado la compra del regalo de cumpleaños de Dario, un compañero de trabajo. Para ello, Ana va a un negocio donde hay diferentes obsequios que le pueden gustar a Dario. Cada obsequio tiene un precio determinado. Ana conoce el monto minimo a gastar para la compra del regalo, y su objetivo es encontrar una combinacion de objetos a comprar que cubra exactamente el monto a gastar o __lo supere en forma minima__; considerando que no puede repetir objetos.

a) Árbol de decision binario con tres items inventados.
b) Tabla de dominio.
c) Formula.
d) Matriz inventada con 3 filas
e) Backtracking
f) Optimización programacion dinamica.

Ana: $35

R1: $10

R2: $20

R3: $30

A)

```
                              R1
                        Si          No
                  R2                         R2
             Si       No                  Si     No
           R3            R3            R3           R3
        Si   No      Si      No     Si  No      Si       No
      60      30  *40*         10  50      20  30          0 

```

B) 

C = Plata que queda despues de la transaccion

S = Elementos que hay en la tienda

| | C<0 | C=0 | C>0 |
|:---:|:---:|:---:|:---:|
|#S=0|Mod(C)|0|+inf|
|#S>0|Mod(C)|0|CALCULAR|


C) 

```
Ana(S, C) = | C |                 si c < 0
          = 0                     si c = 0
          = +inf                  si c > 0 y #S = 0
          = Min(Ana(S[2 .. inf], C-S[1], Ana(S[2 .. inf], C))  si c > 0 y #S > 0
```

D) 

| | C=0 | C=1 | C=2 | C=3 |
|:---:|:---:|:---:|:---:|:---:|
|[]|0|+inf|+inf|+inf|
|[1]|0|Ana([1], 1) = Min(Ana(S[], 0), Ana(S[], 1)) = Min(0, +inf) = 0|Ana([1], 2) = Min(Ana([], 1), Ana([], 2)) = Min(+inf, +inf) = +inf|Ana([1], 3) = Min(Ana([], 2), Ana([], 3)) = Min(+inf, +inf) = +inf|
|[4, 1]|0|Ana([4, 1], 0) = Min(Ana(S[1], -3), Ana(S[1], 1)) = Min(3, 0) = 0|Ana([4, 2], 1) = Min(Ana(S[1], -2), Ana(S[1], 2)) = Min(2, +inf) = 0|Ana([4, 1], 3) = Min(Ana(S[1], -1), Ana(S[1], 3)) = Min(1, +inf) = 1|

E) 

```
Algoritmo
  Ana
Entrada
  Secuencia S de regalos posibles
  Entero C de plata ahorrada
Salida
  Monto minimo que pone Ana
Pseudocodigo
  res <-- 0
  si c < 0
    res <-- |c|
  sino si (c > 0 && #S == 0)
    res <-- +inf
  sino si (c > 0 && #S > 0)
    res <-- Min(Ana(S[2..inf], C-S[1]), Ana(S[2..inf], C))
  fin si
  devolver res
```

F) 

```
Algoritmo
  Ana
Entrada
  Secuencia S de regalos posibles
  Entero C de plata ahorrada
Salida
  Monto minimo que pone Ana
Pseudocodigo
  M <-- [#S + 1, C + 1]zb
  para cap <-- 1 .. c
    M[0, cap] <-- +inf
  fin para
  para el <-- 0 .. #S
    M[el, 0] <-- 0
  fin para
  
  para el <-- 1 .. #S
    para cap <-- 1 .. c
      si (cap - S[el] < 0)
        dif <-- |cap -S [el]|
        M[el, cap] <-- Min(Dif, M[el -1, cap])
      sino
        M[el, cap] <-- Min(M[el-1, cap], M[el - 1, cap - S[el]])
      fin si
    fin para
  fin para
  devolver M[#S, C]
```
