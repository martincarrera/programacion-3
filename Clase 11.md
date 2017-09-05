4) Dados n numeros positivos distintos, se desea encontrar todas las combinaciones de esos numeros tal que la suma sea M.

El dominio para este problema es binario. Hay 2 llamadas recursivas sin el cicla para.

```
Algoritmo
  SUM
Entrada
  Secuencia Sc num elegidos
  Numero suma sumatoria numeros elegidos inicialmente 0
  Valor M sumatoria deseada
  Secuencia N numeros posibles
Salida
  Secuencia de secuencias cuya sumatoria de M
Pseudocodigo
  res <- []

  Si Suma = M
      res <- res + Sc
  SINO SI Suma < M
      para cada el en N
          res <- res + SUM(Sc + [el], Suma + el, M, N)
      fin para
  FIN SI

  devolver res
```

```go
// Codigo funcional en un lenguaje como la gente...
func Sum(candidata []int, suma int, sumaDeseada int, dominio []int) [][]int {
	res := [][]int{}

	if suma == sumaDeseada {
		res = append(res, candidata)
	} else if suma < sumaDeseada {
		for _, el := range dominio {
			aux := Sum(append(candidata, el), suma+el, sumaDeseada, dominio)
			res = append(res, aux...)
		}
	}

	return res
}
```
