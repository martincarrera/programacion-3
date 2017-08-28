# Greedy (No Recursivos)

La utilizaremos para resolver problemas de optimizacion (maximizar o minimizar algo), dividiendo el problema en etapas y aplicando en cada una de ellas un criterio de seleccion (euristica).

### Ejemplo: Problema del cambio (del super chino)

Dado un monto M y una secuencia D denominaciones de billetes, encontrar la minima cantidad de billetes con los que se obtiene M. (dar la menor cantidad de billetes posibles)

26. Pseudocodigo no recursivo del cambio.

```
Algoritmo
  Greedy
Entrada
  Numero M monto de vuelto  devolver
  Secuencia S de numeros enteros ordenada de mayor a menor
Salida
  Numero cantidad minima de billetes
Pseudocodigo
  N <- 0
  para cada el en S[1 ... infinito]
    N <- N + M / S[el]
    M <- M - S[el] * M / S[el]
    si M == 0
      el <- infinito
   fin si
  fin para
  devolver N
fin
```

Alternativa de un compañero
```
 i <- 1
 billetes <- 0
 mientras M > 0 y i <= #S
   billetes <- billetes + (M / S)
   m <- m % S[i]
   i <- i + 1
 fin mientras
 devolver billetes
```


### Otro Ejemplo -> Problema de la mochila (version divisible)

Dada una mochila de capacidad M y secuencia S de tuplas (peso, ganancia). Los elemetos se pueden dividir obteniendo una ganacia proporcional.

27. Pseudocodigo que reciba un algoritmo de ordenamiento y calcule la ganancia maxima.

```
Algoritmo
  Mochila
Entrada
  Numero M peso maximo que soporta la mochila
  Secuencia S de tuplas de la forma (peso, ganancia)
Salida
  Numero ganancia maxima
Pseudocodigo
  ganancia -> 0
  ordenaTupla(S)
  para cada el en S[1 ... infinito]
    si M <= peso
      ganancia <- ganacia + el.peso * el.ganancia
      M <- M - el.peso
    sino
      ganancia <- ganancia + M * el.ganancia / el.peso
      M <- 0
    fin si
    si M == 0
      el <- infinito
    fin si 
  fin para
  devolver ganancia
fin
```

Resuelto por el profesor:

```
Entrada
  Capacidad C
  Secuencia S de tuplas (peso, ganacia)
  Algoritmo ordenaPorGananciaDivididoPesoDesc
Salida
  res
pseudocodigo
  S <- ordenaPorGananciaDivididoPesoDesc(S)
  para cada el de S
    Si C > 0
      Si el.peso < C
        res <- res + el.ganancia
        C <- C - el.peso
      sino
        res <- res + (c * el.ganancia) / el.peso
        C <- 0
      fin si
    fin si
  fin para
devolver res
```				


### Algoritmos de Grafos
Sea G(V, A) un grafo representado por una tupla donde V es una secuencia de vertices y A una secuencia de aristas donde cada arista es a su vez una tupla (origen, destino, peso).

28. Pseudocodigo que calcule la sumatoria del peso de las aristas de un grafo.

```
Algoritmo
  Pesototalgrafo
Entrada
  Grafo G(V,A)
Salida
  Peso total de aristas de G(V,A)
Pseudocodigo
  total <- 0
  para cada A de G.A
    total <- total + A.peso
  fin para
devolver total
```

29. Determinar el vertice con mayor peso de sus aristas.

```
Algoritmo
  verticemayorpeso
Entrada
  Grafo G(V,A)
Salida
  Maximo peso de la arista de G(V,A)
Pseudocodigo
  max <- -infinito
  para cada V de G.V
    suma <- 0
    para cada A de G.A
      si (A.origen) o (A.destino=0)
        suma <- suma + A.peso
      fin si
    fin para
    si suma > max
      max <- suma
    fin si
  fin para
devolver max	
```

## Dijkstra

Va a calcular el camino minimo de un nodo origen al resto. En este caso A.


30. Dijkstra del grafo de la carpeta

31. Realizar un grafo de ejemplo con 8 vertices y aplicar dijkstra detalando pasos. (Tarea)
				
