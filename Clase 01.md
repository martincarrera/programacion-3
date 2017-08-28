## Forma

* Parcial (con recuperatorio)
* TP (java)
* Tareas clase a clase (obligatorias)
* Final
 
## Contenido

* Tecnicas de Programacion
  * División y conquista
  * Greedy
  * Backtracking
  * Programacion dinámica
* Teoria de Complejidad Computacional
* Algoritmos Conocidos

## Lineamientos de Pseudo Código

```
Algoritmo
 <nombre>
Entrada
 <tipo de datos> <nombre> <explicación>
 Secuencia S de Numeros enteros ordenada
 Cantidad C de Participantes
Salida
 <tipo de dato> <explicacion>
 Secuencia ordenada
```

## Ejemplo

```
Variables
 A <-- 3
 Nom <-- "Esteban"
 Rangos 1 .. 5
Iteracion
 Para I <-- 1 .. 10
  algo
 Fin Para
```

1) Pseudocodigo que calcule la sumatoria de los valores de X a Y dado.
 
```
Algoritmo
 Sumatoria de los valores entre X e Y
Entrada
 Numero X Entero
 Numero Y Entero mayor que X
Salida
 Numero Entero con el resultado de X + ( X + 1 ) + .. +  ( Y - 1 ) + Y

Pseudocodigo
 Resultado <-- 0
 Para I <-- X .. Y
  Resultado = Resultado + I
 Fin Para
 Devolver Resultado
```

### Valores especiales

* Infinito
* Infinito Negativo
* Indefinido

### TDAs

#### Secuencia

```
S <-- [] // con corchetes
S2 <-- [3, 2, 4, 1]
V <-- S2[1] // Obtengo el 3
L <-- #S2 // Obtengo el largo de S2
Si A > B
 ...
Fin SI
```

2) Dada una Secuencia S devolver el elemento mayor (usar valores especiales)
```
Algoritmo
 Devolvedor de elemento mayor de una secuencia
Entrada
 Secuencia S de Numeros
Salida
 Numero mayor de la secuencia

PseudoCodigo
 mayor <-- -infinito
 para cada el en S
  si el > mayor
   mayor = el
  fin si
 fin para
 devolver mayor
```

#### SubSecuencias

```
S <-- [2, 8, 7, 5, 3]
Sizq <-- S[1 .. (#S / 2)] /* [2, 8] */
Sder <-- S[(#S/2) + 1 .. #S]
Sder <-- S[(#S/2) + 1 .. infinito] // Hasta el final (sin irme de rango)
Sder <-- S[(#S/2) + 1 .. 10] // Hasta el final (sin irme de rango)
V <-- S[38] /* Da indefinido */
```

#### Operadores

* /  Division entera
* // Division con decimales
* %  Resto

3) Dada una secuencia S, si el primer elemento es par, devolver el promedio de la primer mitad; sino el promedio de la segunda mitad.

```
Algoritmo
 Algoritmo que devuelve el promedio de la primer mitad si el primer elemento es par, de la segunda si es impar
Entrada
 Secuencia S de Numeros
Salida
 Numero con decimales que es el promedio de la primer mitad si S[1] es par, o de la segunda mitad en otro caso

Pseudocodigo
 total <-- 0
 si (S[1] % 2 == 0)
  para cada el de S[1 .. (#S / 2)]
   total <-- total + el
  fin para
  devolver (total / (#S / 2))
 fin si
 para cada el de S[(#S / 2) .. #S]
  total <-- total + el
 fin para
 devolver (total / ((#S / 2) + 1))
```

#### Concatenar Secuencias

```
S1 <-- [1, 2, 3]
S2 <-- [4, 5, 6, 7]
UN <-- S1 + S2
DOS <-- S1 + [3, 8]
AG <-- S1 + [1]
```

#### Conjuntos
```
C <-- {}
C2 <-- {2, 3}
si 4 pertenece a C
si 3 no pertenece a C
```

4) Dada una secuencia S y un conjunto C, devolver otra secuencia con los elementos de S que no esten en C
```
Algoritmo
 Algoritmo que devuelve una subsecuencia de S de los elementos que no estan en C
Entrada
 Secuencia S de Numeros
 Conjunto C de Numeros
Salida
 Secuencia con elementos de S que no estan en C

Pseudocodigo
 res <-- []
 para cada el en S
  si el no pertenece a C
   res <-- res + el
  fin si
 fin para
 devolver res
```

#### Tuplas

Agrupan varias variables conceputalmente relacionadas en una sola

```
Triangulo <-- (Base: 10, Altura: 20)
B <-- Triangulo.Base
devolver (x:10, y:20)

Entrada
 Tupla (X, Y, Z) que representa un punto en el espacio
Salida
 Tupla (Mayor, Menor) que ...
```

5) Dada una secuencia S devolver una tupla con la sumatoria y el promedio
```
Algoritmo
 Algoritmo que devuelve la sumatoria y el promedio de los elementos de S
Entrada
 Secuencia S de Numeros
Salida
 Tupla (sumatoria, promedio) de los elementos de S

Pseudocodigo
 total <-- 0
 para cada el en S
  total <-- total + el
 fin para
 devolver (sumatoria: total, promedio: (total / #S))
```

## Teoria de la Complejidad Computacional

Busca clasificar a los algoritmos dependiendo como varia la cantidad de instrucciones que ejecuta en funcion del tamaño del set de datos de entrada (n)

* Constantes O(c)
 * Ejecuta siempre la misma cantidad de instrucciones independientemente del n.
* Logaritmicos O(log n)
 * 
* Lineales O(n)
 * La cantidad de instrucciones depende linealmente de n (2n, 6n + 4, 8n + 100)
* Lineal - Logaritmicos O (n * log(n))
* Cuadratica O(n<sup>2</sup>)
* Cubicas O(n<sup>3</sup>)
* Polinomicas
* Exponenciales O(2<sup>n</sup>)

### Ejemplo

```
Pseudocodigo
 total <-- 0                                            C1
 para cada el en S                                      n
  total <-- total + el                                  C2
 fin para
 devolver (sumatoria: total, promedio: (total / #S))    C3
 
Tarda(n) = C1 + n(C2) + C3 = C13 + n(C2)
=> Lineal => O(n)
```

6) Dada una secuencia S devolver una segunda secuencia con aquellos elementos de S que tengan un doble (2x) en la secuencia

```
Algoritmo
 Algoritmo que devuelve la subsecuencia de elementos de S que tienen un doble en S
Entrada
 Secuencia S de Numeros
Salida
 Subsecuencia de S con aquellos numeros cuyos dobles pertenecen a S

Pseudocodigo
 res <-- []              C1
 para cada e en S        n
  para cada el en S      n
   si ((e * 2) == el)    C2
    res <-- res + e      C3
   fin si
  fin para
 fin para
 devolver res            C4
```

7) Calcular la complejidad del ejercicio 6.

```
 tarda(n) = C1 + (n * n * (C2 + C3)) + C4 = C1 + C23 n*n + C4
 => Cuadratica => O(n^2)
```

### Relaciones (Diccionarios)

```
// Declaracion 
Santillana: palabras --> significado
 
// Creacion de claves
Santillana("abad") <-- "persona que vive en una abadia"
Santillana("abadia") <-- "lugar donde vive el abad"

// Preguntar si una clave existe
si "abadu" no pertenece a Santillana
 ...
fin si

// Recorro las claves
para cada clave en Santillana
 def <-- Santillana(clave)
fin para
```

8) Dada una Secuencia P de Palabras, utilizar un diccionario para contar la cantidad de ocurrencias de cada palabra y luego devolver la mas frecuente

```
Algoritmo
 Buscar palabra mas frecuente en secuencia de palabras
Entrada
 Secuencia P de Palabras
Salida
 Palabra mas frecuente en S

Pseudocodigo
 dic: Palabra --> Ocurrencias
 para cada pal en P                                      n
  si pal pertenece en dic                                Ca
   dic(pal) <-- dic(pal) + 1                             Cb
  sino                                                   
   dic(pal) <-- 1                                        Cc
  fin si
 fin para
 mayor <-- (palabra:indefinido, cantidad: -infinito)
 para cada pal en dic                                   n
  si mayor.cantidad < pal.cantidad                      Cd
   mayor <-- (palabra: pal, cantidad: dic(pal))         Ce
  fin si
 fin para
 devolver mayor.palabra                                 Cf
 
 tarda(n) = n *  MAX(Ca + Cb, Ca + Cc) + n * (Cd + Ce) = n * Cabc + n * Cde 
 => Lineal => O(n)

```

### Calculo de Complejidad

```
...
 si A > B            CW
  C <-- 3            CX
 sino
  para cada el de S  n
   C <-- C + el      CY
  fin para
 fin si
...

tarda(n) = ... + cw + MAX(CW, n * CY) + ... = ... + cw + (n * cy)+ ...
```

9) Calcular complejidad act 8.

Opcional: Ir armando TDA secuencia en Java
