## 2 - Ejercicio Backtracking (3 puntos)

Algoritmo:
    
  - PermutacionLetras

Entrada:

  - Secuencia `S` de letras
  - Cantidad `N` de letras deseadas con N <= S
  - Secuencia `Sc` de letras elegidas inicialmente vacia

Salida
  - Secuencia de secuencias con todas las permutaciones de `N` letras de `S` (Ej: Si `S` = `[A, B, C]`, entonces `Salida` = `[ [A, B] , [B, A], [A, C] , [C, A], [B, C] , [C, B] ]`)
  
PseudoCodigo:
  ```
  sol <-- []
  para cada l en S
    si l no pertenece a Sc // no puedo preguntar si una letra pertenece a una secuencia, deberia iterarla y verificar si pertenece o no
      Sc <-- Sc + l // asumo pasaje por valor entre metodos y no por referencia. Esto en el codigo de abajo no funciona.
      si N == 1
        sol <-- sol + [l]
      sino
        subPerms <-- permutarLetras(S, N - 1, Sc)
        para cada perm en subPerms
          sol <-- sol + [l + perm]
        fin para
      fin si
    fin si
  fin para
  devolver sol
  ```
  
Codigo (javascript)
  
  ``` js
  const permuteLetters = (s, n, sc) => {
  const sol = [];
  s.forEach(l => {
    if (sc.indexOf(l) === -1) {
      if (n === 1) {
        sol.push([l]);
        sc.push(l);
      } else {
        const scCpy = JSON.parse(JSON.stringify(sc));
        scCpy.push(l);
        subPerms = permuteLetters(s, n - 1, scCpy);
        if (subPerms) {
          subPerms.forEach(perm => {
            sol.push([l + perm]);
          });
        }
      }
    }
  });
  return sol;
};

console.log(permuteLetters(["a", "b", "c", "d"], 3, []));
  
  
 ```
