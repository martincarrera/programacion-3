# Final regular Progra 3 (16/12/2016) - Viernes noche

## 1 - Ejercicio Backtracking (4 puntos)

Algoritmo:
    
  - ColorearGrafo

Entrada:

  - Grafo `G(V, A)`
  - Vertice Actual `V` (Inicialmente el origen) `// yo no lo use`
  - Secuencia `S` de colores posibles
  - Diccionario `colores: vertice -> color` que asocia a cada vertice del grafo con un color (Inicialmente contiene todos los vertices del grafo y asociado el color indefinido)
  - Secuencia `Sc` de todos los vertices sin colorear (Inicialmente todos los vertices del grafo)
  - Algoritmo `verificarGrafo(G(V, A))` que verifica si el grafo contiene vertices limitrofes con el mismo color `// Yo aclare que la comparacion de indefinido con indefinido da FALSO, y cualquier color es distinto de indefinido.`
  - Algoritmo `contarColores(colores)` que devuelve una secuencia de todos los colores distintos contenidos en el diccionario colores. `// Aclare que si hay por lo menos un color indefinido, devuelve una secuencia vacia, para contemplar el caso en que no pudo pintarse todo el grafo`

Salida
  - Tupla `(cantidadColores, colores)` que determine como colorear el grafo usando la menor cantidad de colores posibles de modo que no haya dos vertices limitrofes con el mismo color.

Pseudocodigo
```
        res <-- (-infinito, colores) // incialmente el diccionario de colores tiene todos seteados en indefinido
        para cada vertice en Sc
            para cada color en S
                colores(vertice) <-- color
                si (verificarGrafo(G(V, A)))
                    color <-- S[+infinito] // finalizo el para de colores
                    Sc <-- Sc[2 .. +infinito] // Quito el vertice de Sc porque ya lo pinte
                sino
                    colores(vertice) <-- indefinido
                fin si
            fin para
        fin para
        c <-- contarColores(colores)
        si #C == 0
            devolver res
        sino
            devolver (#C, colores)
        fin si
```

## 2 - Ejercicio Backtracking (3 puntos)

Algoritmo:
    
  - PermutacionLetras

Entrada:

  - Secuencia `S` de letras
  - Cantidad `N` de letras deseadas con N <= S
  - Secuencia `Sc` de letras elegidas inicialmente vacia `// Yo no la use, creo que hice algo mal aca`

Salida
  - Secuencia de secuencias con todas las permutaciones de `N` letras de `S` (Ej: Si `S` = `[A, B, C]`, entonces `Salida` = `[ [A, B] , [B, A], [A, C] , [C, A], [B, C] , [C, B] ]`)

Pseudocodigo
```
    si N = 1
        para cada L en S
            Salida <-- Salida + L // (1)
        fin para
    sino
        para cada L en S
            aux <-- permutacionesLetras(S, N-1, []) // (2)
            para cada A en aux
                Salida <-- Salida + [L + A] // (3)
            fin para
        fin para
    fin si
    devolver Salida
```
Notas: 

1. A la secuencia `Salida` se le agregan todas las secuencia de 1 letra (Ej: Si `S` = `[A, B, C]`, entonces `Salida` = `[ [A], [B], [C] ]`)
2. Calculo todas las permutaciones posibles con las mismas letras y `N` = `N - 1`
3. A la secuencia de soluciones `Salida` le agrego todas las secuencias formadas por la concatenacion de la letra `L` actual y la subsecuencia de `N - 1` letras `A` calculada en 2.

## 3 - Induccion (3 puntos)

Complete y demuestre por induccion `*1` y `*2` para:

1. Obtener una complejidad Lineal 
2. Obtener una complejidad Exponencial

```
T(N) =  C                si *1
        2.T(*2) + C      si N > 1
```

Resolucion:

1. Lineal

```
*1: N = 1
*2: 1

T(N) = 2.T(1) + C = 2 (C) + C = 3C
O(C) = Lineal
```


2. Exponencial

```
*1: N = 0
*2: N - 1

T(N) = 2.T(*2) + C = 
     = 2.T(N - 1) + C = 2.(2.T(N - 2) + C) + C = 
     = 4.T(N - 2) + 3C = 4.(2.T(N - 3) + C) + 3C = 
     = 8.T(N - 3) + 7C 
     .
     .
     .
     = (2^K).T(N - K) + ((2^K) - 1).C
     
     => N - K = 0 => N = K =>
     
T(N) = (2^N).T(0) + ((2^N) - 1).C = 
     = (2^N).C + ((2^N) - 1).C =>
     
O(2^N) = Exponencial
```
