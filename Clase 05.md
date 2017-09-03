31) Dado un grafo G y un vertice origen V, fragmento de pseudocodigo que inicialice un diccionario de pesos acumulados, uno de anteriores y declare un conjunto de visitados.

```
Algoritmo
 Inicializar Dijaskjtrkajstra
Entrada
 Grafo G
 Vertice origen V
Salida
  
Pseudocodigo
  dicPesoAcum: Vertice --> pesoAcum
  dicAnte: Vertice --> verticeAnt
  conjuntoVisitados <-- {}
  
  para cada v en G
    dicPesosAcum(v) <-- inf
    dicAnte(v) <-- indef
  fin para
  dicPesosAcum(V) <-- 0
```

32) Dado un grafo G y un vertice origen V, fragmento de pseudocodigo que determine en el diccionario el vertice con menor peso acumulado

```
Algoritmo
 Buscar menor
Entrada
 Grafo G
 Vertice origen V
Salida
  
Pseudocodigo
 Menor <-- inf
 V <-- indef
 
 para cada vert en dicPesoAcum
  si dicPesoAcum(vert) < menor
   menor <-- dicPesoAcum(vert)
   V <-- vert
  fin si
 fin para
```

33) Dado un grafo G y un vertice origen V, fragmento de pseudocodigo que actualice el peso acumulado de los adyacentes usando la funcion min

```
Algoritmo
 Actualizar nodos adyacentes 
Entrada
 Grafo G
 Vertice origen V
Salida
  
Pseudocodigo
 pesoNuevo <-- 0
 para cada A de GA
  si A.origen == vert
   pesoNuevo <-- pesoAcum(A.origen) + A.peso
   si pesoNuevo < pesoAcum(A.destino)
    pesoAcum(A.destino) <-- pesoNuevo
   fin si
  fin si
 fin para
```

34) Pseudocodigo Dijkstra

```
Algoritmo
 Dijkstra
Entrada
 Grafo G
 Vertice origen O
Salida
 Tupla (dicPesoAcum, dicAnt)

Pseudocodigo

 dicPesoAcum: Vertice --> pesoAcum
 dicAnte: Vertice --> verticeAnt
 conjVisitados <-- {}
 
 para cada v en G.V                          V
  dicPesosAcum(v) <-- inf                    C1
  dicAnte(v) <-- indef                       C2
 fin para
 dicPesosAcum(O) <-- 0                       C3

 mientras #conjVisitados < #G.V              V
  VMenor <-- (vertice: indef, peso: infinito)C4
  para cada clave en dicPesoAcum             V
   si dicPesoAcum(clave) < VMenor.peso y clave no pertenece conjVisitados C5
    VMenor.peso <-- dicPesoAcum(clave)       C6
    VMenor.vertice <-- clave                 C6
   fin si
  fin para
  para cada a en G.A                         A
   si a.origen = VMenor.vertice y dicPesoAcum(a.destino) > (dicPesoAcum(a.origen) + a.peso) C7
    dicAnt(a.destino) <-- a.origen           C8
    dicPesoAcum(a.destino) <-- dicPesoAcum(a.origen) + a.peso   C8
   fin si
  fin para
  conjVisitados <-- conjVisitados + {VMenor.vertice}  C9
 fin mientras
 devolver (dicPesoAcum, dicAnt)
```

Tarea: Calcular complejidad de dijkstra

```
T(V, A) = V * (C1 + C2) + C3 + V * (C4 + V * (C5 + C6) + A * (C7 + C8) + C9)
        = V * C12 + C3 + V * (C4 + V * C56 + A * C78 + C9)
        = V * C12 + C3 + V * C4 + V * V * C56 + V * A * C78 + V * C9
        = V * V * C56 + V * A * C78 + V * (C12 + C4 + C9) + C3
        = V * V * C56 + V * A * C78 + V * C1249 + C3

=> O(V^2 + V*A)
```

Complejidad de algoritmos de grafos:

Se expresa en funcion de A y V

```
O(v)
O(a)
O(a.v)
O(a^2)
```

35) Calcular la complejidad del algoritmo:

```
Algoritmo
 verticemayorpeso
Entrada
 Grafo G(V,A)
Salida
 Maximo peso de la arista de G(V,A)
Pseudocodigo
 max <-- infinito               C1
 para cada V de G.V             V1
  suma <- 0                     C2
  para cada A de G.A            A
  si (A.origen) o (A.destino=0) C3
   suma <- suma + A.peso        C4
  fin si
 fin para
 si suma > max                  C5
  max <- suma                   C6             
 fin si
fin para
devolver max

T() = C1 + V * (C2 + A * (C3 + C4) + C5 + C6)) + C7
    = C1 + V * (C2 + A * C34 + C56) + C7
    = C1 + V * (A34 + C256) + C7
    = C1 + V * (A34) + V * C256 + C7
 => O(V * A)
```
