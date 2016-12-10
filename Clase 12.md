### Backtracking

* Soluciones
  * Todas las soluciones
    * Secuencia de soluciones (Secuencia de secuencias)
  * Una solucion si existe...
    * (Hay solucion, solucion)
    * Booleano si existe o no
    * Solucion
  * La mejor solucion
    * (Valor solucion, mejor solucion (secuencia))
    * Valor

```
Algoritmo
 Caballos
Entrada
 Tupla Pos(X, Y) con la posicion actual del caballo
 Matriz Tablero de MxM de booleanos que dice si una celda esta visitada o no
 Numero M ancho del tablero
 Algoritmo sePuedeMover(Pos(X, Y), Tablero)
 algoritmo todoVisitado(Tablero)
Salida
 Verdadero o falso si puedo recorrer todo el tablero
Pseudocodigo
 Res <-- falso
 si no sePuedeMover(Pos, Tablero)
  Res -- todoVisitado(Tablero)
 sino
  para cada PosPosible en movimientosPosibles(Pos, Tablero)
   si no Res
    Tablero[posPosible.X, posPosible.Y] <-- verdadero
    res <-- Caballos(PosPosible, Tablero, M, sePuedeMover, todoVisitado)
    Tablero[posPosible.X, posPosible.Y] <-- falso
   fin si
  fin para
 fin si
 devolver res
```


```
Algoritmo
 Laberinto
Entrada
 Tupla Pos(esSalida, esTransitable, vencinos) donde vecinos es una secuencia de tuplas igual a la dada
 Conjunto C con posiciones ya visitadas inicialmente vacio
 Secuencia Sc con posiciones recorridas hasta la salida
Salida
 Tupla (CantPasos, Solucion)
Pseudocodigo
 Res <-- (CantPasos: inf, solucion: ?)
 si pos.esSalida
  Res <-- (CantPasos: #Sc, Solucion: Sc)
 sino
  para cada vecino en pos.vecinos
   si vecino.esTransitable y no vecino en C
    aux <-- Laberinto (vecino, c+{vecino}, Sc + vecino)
    si (aux.cantPasos < res.cantPasos)
     res <-- aux
    fin si
   fin si
  fin para
 fin si
 devolver res
```
