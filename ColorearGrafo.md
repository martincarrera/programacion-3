## 1 - Ejercicio Backtracking (4 puntos)

Algoritmo:
    
  - ColorearGrafo

Entrada:

  - Grafo `G(V, A)`
  - Vertice Actual `V` (Inicialmente el origen) `// no lo uso`
  - Secuencia `S` de colores posibles
  - Diccionario `colores: vertice -> color` que asocia a cada vertice del grafo con un color (Inicialmente contiene todos los vertices del grafo y asociado el color indefinido)
  - Secuencia `Sc` de todos los vertices sin colorear (Inicialmente todos los vertices del grafo)
  - Algoritmo `verificarGrafo(G(V, A), colores)` que verifica si el grafo contiene vertices limitrofes con el mismo color
  - Algoritmo `contarColores(colores)` que devuelve una secuencia de todos los colores distintos contenidos en el diccionario colores. 

Salida
  - Tupla `(cantidadColores, colores)` que determine como colorear el grafo usando la menor cantidad de colores posibles de modo que no haya dos vertices limitrofes con el mismo color.

Pseudocodigo
```
  para cada vertice en Sc
    para cada color en S
      colores(vertice) <-- color
      si verificarGrafo(Grafo, colores)
        si #colores == #G.V
          devolver (cantColores(colores), colores)
        sino
          colorearGrafo(G, S, colores, Sc - vertice, verificarGrafo(Grafo, colores), contarColores)
        fin si
      fin si
    fin para
  fin para
```

Recorro los vertices uno a uno, pruebo colores hasta que encuentro un color que funciona.
Luego, voy invocando a la funcion nuevamente con los vertices faltantes.

Codigo:

``` js
const Vertices = [1, 2, 3, 4, 5];
const Aristas = [
  {
    origen: 1,
    destino: 2
  },
  {
    origen: 2,
    destino: 3
  },
  {
    origen: 2,
    destino: 5
  },
  {
    origen: 3,
    destino: 5
  },
  {
    origen: 4,
    destino: 5
  },
  {
    origen: 2,
    destino: 4
  }
];

const Grafo = { Vertices, Aristas };
const S = ["Rojo", "Amarillo", "Azul", "Verde", "Naranja", "Negro", "Marron"];
const colores = {};

const filter = (value, index, self) => {
  return self.indexOf(value) === index;
};

const contarColores = colores => {
  let values = [];
  Object.keys(colores).forEach(color => {
    values.push(colores[color]);
  });
  values = values.filter(filter);
  return values.length;
};

const verificarArista = (arista, colores) => {
  return colores[arista.origen] && colores[arista.destino]
    ? colores[arista.origen] != colores[arista.destino]
    : true;
};

const verificarGrafo = (Grafo, colores) => {
  let retVal = true;
  Grafo.Aristas.forEach(arista => {
    if (!verificarArista(arista, colores)) {
      retVal = false;
    }
  });
  return retVal;
};

const colorearGrafo = (Grafo, S, colores, Sc) => {
  Sc.forEach(v => {
    S.forEach(c => {
      colores[v] = c;
      if (verificarGrafo(Grafo, colores)) {
        if (Object.keys(colores).length === Grafo.Vertices.length) {
          console.log(colores);
        } else {
          const scCpy = JSON.parse(JSON.stringify(Sc));
          const index = scCpy.indexOf(v);
          scCpy.splice(index, 1);
          colorearGrafo(Grafo, S, colores, scCpy);
        }
      }
    });
  });
};

colorearGrafo(Grafo, S, colores, [1, 2, 3, 4, 5]);

```
