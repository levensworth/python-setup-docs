
# Partes de un objeto.

Entendamos como representar un objeto en Python

Intentemos representar un estudiante. Progresivamente vamos a ir llegando a un modelo que nos sea útil.

!!! Obs
    OOP es un estilo de programación que pone gran parte del enfoque en generar un modelo de la realidad 
    que sea útil para nuestro problema.

## Que es esto de clases:


![blue print](../imgs/blue_print.jpeg)


Una clase es simplemente un "blue print" de lo que esperamos que tenga.
Como en arquitectura, piensen en la definción de clase como el plano de la casa lo cual no es lo mismo que la casa.

Ahora, un objeto es una "instancia de la clase" o lo mismo que una casa que siga los planos que planteamos. Es la 
materialización del blue print que armamos.

## 1. Objeto dummy:

```python
# definición de la clase (blue print)
#Aquí definimos una clase, en su forma más sencilla. No contiene absolutamente ningún valor nuevo.


class Student:
    pass

# acá estamos generando una "instnacia de la clase". Lo que sería la casa de nuestra analogía.
chispita = Student()

# ahora chispita es una variable que hace referencia a una instancia de la clase Student.

not_chispita = Student()

# veamos que dos instancias de la misma clase no son iguales. Esto es porque son diferentes objetos
# a pesar de que ambos pertenecen a la clase Student.
chispita == not_chispita
```


## 2. Métodos:

Ahora como todo alumno es cordial, deberiamos permitir que el objeto alumno tenga una forma de saludar
imprimiendo por pantalla el mensaje "hola!"

Para esto tenemos que agregar un "metodo" a la case que ejecute el comportamiento que nosotros queremos.
Un Método es el nombre OOP que le damos a las funciones que se declaran como parte de una clase. 
```python

class GreetingStudent:

    def greet(self) -> None:
        print('hola!')
```

En este ejemplo verán la clase GreetingStudent contiene un método greet el cual ejecuta el comportamiento 
deseado. Lo primero que vemos, es que un método es literalmente una función y esto es correcto. Lo segundo
que veremos es que la función recibe un parámetro llamado "self", esto es lo que diferencia a una función tal
y como la concen de un método (a aprte de estar definida dentro de una clase). 
El primer parámetro de los métodos de una clase casi siempre es especial. En el caso de "self", como el nombre 
indica es una referencia a si mismo. Lo que tienen que saber es que este argumento solo deben declararlo en la 
definición de la función pero al llamarla este parámetro es auto completado por Python.


```python
class GreetingStudent:

    def greet(self) -> None:
        print('hola!')
student = GreetingStudent()
student.greet() # Asi es como invocamos a la función greet, fijense que tuve que crear una instancia de GreetingStudent para poder ejecutarla.
```

## 3. Atributos

Al igual que en un plano podemos incluir "paredes","puertas", "aperturas" en las clases
podemos tener lo que llamamos "atributos". 
Un atributo, es simplemente un valor que pertenece a esa clase. Piensenlo como una variable
interna de la clase, podemos generar cuantas querramos, la forma de crearlas es utilizando el argumento 
de self.

```python

class StudentWithArguments:
    def __init__(self,):
        # de esta forma estamos asignando el valor 'santiago' a la variable name
        # ahora en cualquier otro metodo de la clase donde utilicemos el atributo name (self.name)
        # obtendremos este valor
        self.name = 'santiago'

    def greet(self) -> None:
        print(f'Hola me llamo {self.name}')


santi = StudentWithArguments()
santi.greet()
```

