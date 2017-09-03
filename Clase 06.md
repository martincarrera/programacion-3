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
  // Se podria haber hecho llamando a InicializarDiccionario asi:
  // part <-- InicializarDiccionario(G(V, A))
  i <-- 1
  part: vert --> particion
  para cada vertice de G.V                     V
    part(vert) <-- i                           C1
    i++                                        C2
  fin para

  st <-- (V: G.V, A: [])
  aristas <-- OrdenarAristas(G.A)             // No se la complejidad de este algoritmo, no lo tengo en cuenta
  
  para cada arista en aristas                  A
    si (part(arista.origen) != part(arista.destino))     C3
      UnirParticiones(part, arista)            V
      st.A <-- st.A + arista                   C4
    fin si
  fin para
  
  devolver st

T(V, A) = V * (C1 + C2) + A * (C3 + V + C4)
        = V * C12 + A * V * C34
        
O(V, A) => O(A*V)
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
  
  mientras #origen !== #G.V                           V
    min <-- (origen: indef, destino: indef, peso: inf)C1
    para cada arista en G.A                           A
      si (A.origen pertenece origen && A.destino !pertenece origen && A.valor < min.peso)      C2
        min <-- A                                     C3
      fin si
    fin para
    origen <-- origen + min.destino                   C4
    st.A <-- st.A + min                               C5
  fin mientras
  
  devolver st
  
T(V, A) = V * (C1 + A * (C2 + C3) + C4 + C5)
        = V * (C1 + A * C23 + C45)
        = V * (C145 + A * C23)
        = V * C145 + V * A * C23

O(V, A) = (V * A)
```
