### Backtracking

Llegar a una solucion probando todas las posibles 

Dado un problema P la tecnica busca una o todas las **soluciones**

```
S = [S1, S2, ..., Sn]
```

Para ello determina todas las secuencias posibles que podrian llegar a ser solucion llamada **solucion candidata**.

A los valores que puede tomar cada componente de la solucion lo conocemos como **dominio** o **dominio del problema**.

La cantidad de componentes de la solucion candidata se llama **etapa**.

62) Dominio [1, 2, 3]. 2 etapas. Armar un arbol que genere todas las soluciones candidatas.

```
                                 [ ]
          [1]                    [2]                    [3]
 [1, 1] [1, 2] [1, 3]   [2, 1] [2, 2] [2, 3]    [3, 1] [3, 2] [3, 3]
```

### Ejemplo

  * Todas las soluciones
  * Cantidad fija de etapas
  
 ```
 Algoritmo
  BK
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad E etapas
  ...
 Salida
  Secuencia de secuencias con todas las soluciones encontradas
 Pseudocodigo
  res <-- []
  si #sc = e
    si esSolucion(Sc)
      res <-- [Sc]
    fin si
  sino
    para cada el en dominio
      res <-- res + BK(Sc+[el], e, ...)
    fin para
  fin si
 ```
 
 63) Buscar un numero de N cifras cuyas cifras sumen X
 
 
 ```
 Algoritmo
  CifrasSumanX
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad N de cifras
  Numero X de sumatoria deseada
  Numero sum con sumatoria parcial inicialmente 0
 Salida
  Secuencia de secuencias con todas las soluciones encontradas
 Pseudocodigo
  res <-- []
  si #Sc == N
    si SUM == X
      res <-- [Sc]
    fin si
  sino
    para cada el en [0 .. 9]
      res <-- res + CifrasSumanX(Sc+[el], N, X, SUM + el)
    fin para
  fin si
  devolver res
 ```
 
 ### Poda
 
Consiste en agregar un if antes de la llamada recursiva para evitar seguir profundizando en el arbol de recursividad si la solucion ya no es factible

64) Agregar una PODA al ejemplo anterior


 ```
 Algoritmo
  CifrasSumanX
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad N de cifras
  Numero X de sumatoria deseada
  Numero sum con sumatoria parcial inicialmente 0
 Salida
  Secuencia de secuencias con todas las soluciones encontradas
 Pseudocodigo
  res <-- []
  si #Sc == N
    si SUM == X
      res <-- [Sc]
    fin si
  sino
    para cada el en [0 .. 9]
      si (SUM + el < X)
        res <-- res + CifrasSumanX(Sc+[el], N, X, SUM + el)
      fin si
    fin para
  fin si
  devolver res
 ```
 
 Ejemplo:
  * Una solucion
  * Cantidad fija de etapas
 
 ```
 Algoritmo
  BK
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad E etapas
  ...
 Salida
  Tupla (HaySolucion, Solucion)
 Pseudocodigo
  res <-- (HaySolucion: falso, Solucion: ?)
  si #sc = E
    si esSolucion(Sc)
      res <-- (HaySolucion: verdadero, Solucion: Sc)
    fin si
  sino
    para cada el en dominio
      si no res.HaySolucion
        res <-- BK(Sc+[el], E, ...)
      fin si
    fin para
  fin si
 
 Algoritmo 
  EsSolucion
 Entrada
  Secuencia S de cifras
  Entero X a Sumar
 Salida
  Bool es solucion
 Pseudocodigo
  Suma <-- 0
  para cada e en S
    Suma <- Suma + e
  fin para
  devolver suma == X
 ```
 
 65) Problema de las N reinas. Ubicar N reinas en un tablero de N * N
 
 Disponen del algoritmo "SeAmenazan" que dice si la solucion es valida. Pseudocodigo.
 
 
 ```
 Algoritmo
  Reinas
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad E etapas
  Algoritmo SeAmenazan
 Salida
  Tupla (HaySolucion, Solucion)
 Pseudocodigo
  res <-- (HaySolucion: falso, Solucion: ?)
  si #sc = E
    si !SeAmenazan(Sc)
      res <-- (HaySolucion: verdadero, Solucion: Sc)
    fin si
  sino
    para cada el en 1 .. N
      si no res.HaySolucion
        res <-- NReinas(Sc+[el], E, SeAmenazan)
      fin si
    fin para
  fin si
 ```
 
 
 Ejemplo:
  * La mejor solucion
  * Cantidad fija de etapas
 
 ```
 Algoritmo
  BK
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Cantidad E etapas
  ...
 Salida
  Tupla (ValorSol, Solucion)
 Pseudocodigo
  res <-- (ValorSol: -inf, Solucion: ?)
  si #sc = E
    si esSolucion(Sc)
      res <-- (ValorSol: Evaluar(Sc), Solucion: Sc)
    fin si
  sino
    para cada el en dominio
      aux <-- BK(Sc + [el], E, ...)
      si aux.valorSolucion > res.valorSolucion
        res <-- aux
      fin si
    fin para
  fin si
  devolver res
  ```
  
 66) Dada una secuencia C de caracteres, se quiere armar la mejor clave de N caracteres, para ello dispongo del algoritmo Seguridad que asigna a un codigo, un valor. Si use un caracter no lo puedo volver a utilizar.
 
 
 ```
 Algoritmo
  MejorClave
 Entrada
  Secuencia Sc que representa la solucion candidatada inicialmente vacia
  Secuencia C de caracteres
  Cantidad N de caracteres maximos a utilizar
  Algoritmo Seguridad
 Salida
  Tupla (ValorSol, Solucion)
 Pseudocodigo
  res <-- (ValorSol: -inf, Solucion: ?)
  si #Sc = N
    res <-- (ValorSol: Seguridad(Sc), Solucion: Sc)
  sino
    para cada el en C
      aux <-- MejorClave(Sc + [el], E, EsSolucion)
      si aux.valorSolucion > res.valorSolucion
        res <-- aux
      fin si
    fin para
  fin si
  devolver res
  ```
