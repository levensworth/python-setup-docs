# Recursión:
Recursión es un concepto de programación que tiene sus bases en matemática, se utiliza en ramas como
matemática discreta, teoría de grafos, probabilidad y algebra entre otras.

En la secundaría, habrán escuchado a un profesor de lengua pedirles la definición de una palabra y
reprocharlos porque utilizaron la propia palabra para definirla. En informática esto es algo bueno
y es lo que celebramos como *recursividad*!

Es un conepto importante dado que, cuando el problema presenta un carácter recursivo, la soluciones
son frecuentemente más sencillas de entender y de implementar. 

Este método potente de diseño y resolución de problemas, tiene una relación natural con la [inducción
matemática](https://es.wikipedia.org/wiki/Inducci%C3%B3n_matem%C3%A1tica) y por ello facilita la resolución de problemas y diseño de algoritmos.


## En criollo ... donde puedo encontrar ejemplos:
En simples palabras, los programadores utilizamos recursión para plantear soluciones programaticas
de forma más fácil de leer. Ustedes conocen varios casos de recursión solo que no lo denominan de esa
forma:
- El problema de la ciudadanía :smile_face
- La suma de números
- La serie de Fibonacci

La suma tal, como la uitilizan, puede definirse de manera recursiva:


$$A + B + C$$ 

en realidad se traduce en:

$$(A + B) + C$$

es decir que primero resolvemos la suma entre 2 números y luego decimos que 
el resultado lo sumamos al tecero. Lo que en verdad hacemos es simplemente 
decirnos la siguiente definición de suma:

$$Suma_n$$

donde **n** representa la cantidad de terminos que estamos queriendo sumar.

*Caso base*: **n** = 2

$$Suma(a, b) =  a + b$$


*Caso recursivo*: **n** > 2

$$Suma_n(a, b, c, ...) = Suma(Suma(Suma(a, b), c)..)$$

Recursividad no es más que funciones que dentro del cuerpo se llamana a si mismas!

!!! info
    La llamada de una función a si misma dentro de la propia definición se denomina
    *llamado recursivo*


## Problemas modelos:

Veamos algunos problemas básicos que nos ayudarán a ver la estructura que comparten los problemas recursivos.

### Fibonacci:
La secuencia de Fibonacci se define utilizando la propia definición.
De forma que:

- Fibonacci(1) = 1
- Fibonacci(2) = 1
- Fibonacci(n) = Fibonacci(n-1) + Fibonacci(n-2)

Este tipo de problema, en el que la definición del mismo se puede expersar de forma recursiva es fácilmente 
traducible a código dado que entendemos donde está el *llamado* recursivo

```python
def fibo(n: int) -> int:
    '''
    Args:
    n: (int) representa el indice de la secuencia que se espera obtener.

    Return:
    (int) el valor de dicho indice.
    '''
    
    # primero escribimos los casos base
    if n == 1:
        return 1
    
    if n == 2:
        return 1

    return fibo(n-1) + fibo(n-2)
```

!!! warning
    Como ya saben, la forma recursiva de Fibonacci aunque elegante en su expresión es muy ineficiente.


### Suma de lista:

Escriba una función que dada una lista de enteros retorne el valor de la suma de cada uno de ellos.
La función no puede usar: `sum` ni  `for` y debe de tener no más de 5 lineas (docstring y lineas vacias no cuentan).

``` Python
    from typing import List

    def sum_list(a_list: List[int]) ->  int:
        '''
        Args:
        - a_list:(List[int]) representa la lista de enteros
        
        Returns:
        (int) el valor de la suma de los elementos de la lista.
        '''
        # Defino los casos base
        if len(a_list) == 0:
            return 0
        if len(a_list) <= 2:
            return a_list[0] + a_list[1] if len(a_list) == 2 else a_list[0]
        
        # llamado recursivo
        return a_list[0] + sum_list(a_list[1:])
```



## Como encarar los problemas:
Generalmente los problemas de recursión tiene 3 estructuras básicas. Lo más importante es encontrar 
la parte recursiva del problema, por ejemplo:
- Si el problema trata sobre listas, recordar que una lista tiene un definición recursiva
  del tipo: "una lista es un elemento seguido de una sublista"
- Si el problema nos presenta un `string`, también podemos entenderlo como un caracter seguido de un substring.
- Si el enunciado trata sobre números, escribir el pseudo algoritmo que nos piden para encontrar la parte recursiva (ejemplo: 
Fibonacci).
Dentro de las estructuras básicas encontramos:

1. Recursión sobre la definición del problema. Estos son los casos como fibonacci, donde la recursión está
   explicita en la definición del problema en si.

2. Recursión sobre la estructura de los parámetros. Estos son los casos donde nos pasan un tipo de argumento que tiene una 
definición recursiva y sobre la que tenemos que moldear la solución como el caso de sumar los elementos de una lista.

3. Recursión para backtracking. Estos problemas son normalmente los que requieren que encontremos todas las posibilidades de una 
secuencia o satisfacer los constrains de un problema. [Mas info en la sección avanzada]


Luego de encontrar la estructura, en conveniente definir el/los casos base del problema. Generalemnte 
este paso determina el tipo de solución que tendremos. Recordar que en una solución recursiva, siempre 
tenemos un camino de "ida" hacia el caso base y un camino de "vuelta" desde el caso base. Muchas veces 
depende el problema debemos hacer cosas en el camino de "ida" y otras en el camino de "vuelta" pero esto 
viene determinado por como pensemos el caso base. 

!!! info
    Lo que hagamos `antes` del llamado recursivo ocurre en nuestro camino "hacia" el caso base y 
    lo que hagamos `luego` del llamado recursivo ocurre en el camino "de retorno" desde el caso base. 

