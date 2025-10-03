## P1

Para este tipo de preguntas, en genetal, se puede asumir que los arboles son del tipo que a uno le convenga (`Nodoi`, `Nodoe` o con solo `Nodo`).

En este caso lo haremos usando solo Nodo.

Lo primero en estas preguntas es evaluar cuales son nuestros casos base (sirve pensar en caso base como cualquier cosa que detenga la recursion). El primer caso base es que ambos nodos sean vacíos, entonces, se retorna `True`, ya que dos nodos vacíos son iguales. Luego, es que solo uno sea vacío, donde se retorna `False`, por último, tenemos el caso donde los valores de ambos nodos son distintos, donde también se retorna `False`.

Luego, evaluaremos el caso general. El caso general consiste en un árbol del que, a priori, no sabemos nada. ¿Cómo evaluamos si es que son iguales? Tenemos que confirmar que el valor de cada nodo es igual y que los hijos son iguales. En código es lo siguiente  


```python
def congruentes(p, q): # Esto te lo dieron por enunciado, no hay que cambiarlo
    # Evaluar casos base
    if p == None and q == None: # Caso ambos vacíos
        return True
    elif p == None or q == None: # Caso uno vacío
        return False
    elif p.info != q.info: # Caso son distintos los valores
        return False
    else:
        if congruentes(p.izq, q.izq) and congruentes(p.der, q.der): # Si es que los hijos son iguales
            return True
        else: 
            return False
```

## P2

Para esto es llegar y chantar teorema maestro.

```math
T(n)=pT(\frac{n}{q})+Cn^r
```

1. 
    - 
        $T(n)=2T(\frac{n}{3}) + n$: 


        $p=2$, $q=3$ y $r=1$ por lo que estamos en el caso $q^r>p$ por lo tanto la solución es:

        $T(n) = \Theta(n^{r})=\Theta(n^{1})=\Theta(n)$

    - $T(n)=3T(\frac{n}{3}) + n$: 

        $p=3$, $q=3$ y $r=1$ por lo que estamos en el caso $q^r=p$ y la solución es:

        $T(n)=\Theta(n^r\log n) = \Theta(n^1 \log n) = \Theta(n\log n)$
    - $T(n)=4T(\frac{n}{3}) + n$: 

        $p=4$, $q=3$ y $r=1$ por lo que estamos en el caso $q^r<p$ y la solución es:

        $T(n) = \Theta(n^{\log_qp}) = \Theta(n^{\log_34})
        $

2.
    $a_n=a_{n-1} + 12a_{n-2}, a_0 = 0, a_1=7$

    Se asume que la función es exponencial, entonces $a_n = \lambda^n$.

    ```math
    \lambda^n = \lambda^{n-1}+ 12\lambda^{n-2} \\

    \Rightarrow \lambda^n - \lambda ^{n-1} - 12 \lambda ^{n - 2} = 0 \\

    \Rightarrow \lambda^2 - \lambda ^{1} - 12= 0 \\
    \Rightarrow \phi = \frac{1 + \sqrt{49}}{2} = 4 \land \hat{\phi} = \frac{1 - \sqrt{49}}{2} = -3\\
    \Rightarrow a_n = A\phi^n + B\hat{\phi}^n \\
    ```
    Como $a_0 = 0$, entonces, $A = -B$ y $a_n = A(\phi^n-\hat{\phi}^n)$. Luego, con $a_1 = 7$ tenemos que $7 = A(\phi - \hat{\phi}) = A * 7 \Rightarrow A = 1$.

    $\Rightarrow a_n = 4^n - (-3)^n$


## P3
Estas son las preguntas más difíciles.
    
1. Lo primero es ver la estructura del problema, se tiene que la lista es estrictamente creciente y luego estrictamente decreciente. Nos dan la pista de que hay que inspirarnos en la búsqueda binaria, entonces haremos una solución similar. En la búsqueda binaria sabemos que todo el arreglo está ordenado y se utiliza eso para hacer el *dividir para reinar*, en este caso hay que aprovechar la propiedad que tiene el arreglo. 

    Respuesta a la pregunta: El algoritmo irá recorriendo recursivamente el arreglo, comenzando por los dos elementos del medio (si el número de elementos es impar, entonces el del medio y el de su derecha), en caso de que el de la derecha sea mayor, se ejecuta el algoritmo con la mitad derecha del arreglo y si no, con la mitad izquierda. Si unicamente se tienen tienen 2 elementos, entonces se retorna el mayor y si se tiene un único elemento, se retorna este.

    ```python
    def maximo(arreglo):
        # Casos base
        if len(arreglo) == 1:
            return arreglo[0]
        if len(arreglo) == 2:
            if arreglo[0] > arreglo[1]:
                return arreglo[0]
            else: 
                return arreglo[1]

        medio = (len(arreglo) - 1) // 2
        if arreglo[medio] > arreglo[medio + 1]:
            return maximo(arreglo[:medio + 1])
        else:
            return maximo(arreglo[medio + 1:])
    ```
    En estos ejercicios normalmente da lo mismo confundirse con los indices por uno o por dos, o los detalles de python; lo importante es la idea.

2. Para plantear la ecuación, tenemos que pensar que hacemos en cada paso de la función. Lo primero es ver cuantos llamados recursivos se hacen y podemos ver que es un llamado recursivo, ya que la función se ejecuta o bien para el lado izquierdo, o bien para el derecho. Además, el llamado recursivo es con la mitad de los elementos iniciales (ya que partimos el arreglo por la mitad y usamos un lado). Luego, tenemos que ver cuantas operaciones hacemos por llamado recursivo, que son 3, ya que hacemos 3 comparaciones (`if`) en cada llamada. De modo que la ecuación queda así: $T(n) = 1 * T(\frac{n}{2}) + 3$. Esto es literal la explicación que dí antes expresado como fórmula.

    **Resolución**: 
    
    TIP: Para estos problemas hay que ver la formula, si es que el valor dentro del término recursivo tiene una división, entonces se usa teorema maestro, si tiene una resta se usa el otro método.

    Hay que chantar la fórmula y usar teorema maestro. con $p=1$, $q=2$ y $r=0$. Entonces, estamos en el caso $q^r = p$ y la solución es $T(n)=\Theta(n^r\log n) = \Theta(n^0\log n) = \Theta(\log n)$.

## P4