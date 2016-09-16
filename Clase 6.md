## Algoritmo de Kruskal

C --2-- E :white_check_mark:

D --2-- E :white_check_mark:

B --3-- D :white_check_mark:

A --4-- B :white_check_mark:

B --5-- C :x:

A --6-- E :x:

B --7-- E :x:

A --8-- D :x:


| Vertice | Particion |
|---|---|
|A|1|
|B|~~2~~ 1|
|C|~~3~~ ~~2~~ 1|
|D|~~4~~ ~~3~~ ~~2~~ 1|
|E|~~5~~ ~~3~~ ~~2~~ 1|

37) Programar el algoritmo unir particiones que recibe un diccionario que a un vertice le asigna una particion y una arista, y devuelve el diccionario modificado.

```
Algoritmo
  Unir Particiones
Entrada
  part: vert --> particion
  Arista A
Salida
  part
Pseudocodigo
  si part(A.origen) <= part(A.destino)
    para cada V en part
      si part(V) == part(A.destino)
        part(V) <-- part(A.origen)
      fin si
    fin para
  sino
    para cada V en part
      si part(V) == part(A.destino)
        part(V) <-- part(A.origen)
      fin si
    fin para
  fin si

```

38) Fragmento de pseudocodigo que declara el diccionario y a partir de un grafo lo inicializa.

```
Algoritmo
  Inicializar Grafo
Entrada
  part: vert --> particion
  Grafo G(V, A)
Salida
  part: vert --> particion

Pseudocodigo
  i <-- 1
  part: vert --> particion
  
  para cada vertice de G.V
    part(vert) <-- i
    i++
  fin para
```

39) Algoritmo del Kruskal que recibe como parametros: 
  * OrdernarAristas
  * UnirParticiones

```
Algoritmo
  Kruskal
Entrada
  OrdenarAristas
  UnirParticiones
  InicializarDiccionario
  Grafo G(V, A)
Salida
  Grafo st(V, A) con los caminos minimos

Pseudocodigo
  part <-- InicializarDiccionario(G(V, A))
  st <-- (V: G.V, A: [])
  aristas <-- OrdenarAristas(G.A)
  
  para cada arista en aristas
    si (part(A.origen) != part(A.destino))
      UnirParticiones(part, arista)
      st.A <-- st.A + arista
    fin si
  fin para
  
  devolver st

Complejidad de Kruskal: O(A) => Siempre recorro todas las aristas del grafo.
```

### Primm

1. Tengo un Grafo, partiendo de un vertice aleatoriamente elegido, recorro todas las aristas del grafo y busco la de menor peso cuyo origen sea el mismo del vertice.
2. Agrego la arista al sparring tree.
3. Agrego el vertice destino al conjunto de origen.
4. Recorro nuevamente las aristas buscando la de menor peso cuyo vertice de origen este en el conjunto de origen, y el vertice destino no este en el conjunto origen.
5. Repito los pasos 2, 3 y 4 hasta que el conjunto de origen esta compuesto por todos los vertices del grafo.

40) Pseudocodigo del PRIMM

```
Algoritmo
  Primm
Entrada
  OrdenarAristas
  Grafo G(V, A)
  Vertice de origen V
Salida
  Grafo st(V, A) con los caminos minimos
  
Pseudocodigo
  st <-- (V: G.V, A: [])
  origen <-- {V}
  
  mientras #origen !== #G.V
    min <-- inf
    para cada arista en G.A
      si (A.origen pertenece origen && A.destino !pertenece origen && A.valor < min.valor)
        min <-- A
      fin si
    fin para
    origen <-- origen + min.destino
    st.A <-- st.A + min
  fin mientras
  
  devolver st
```
