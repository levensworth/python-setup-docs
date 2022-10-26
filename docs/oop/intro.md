# Programación Orientada a Objetos:

En esta sección veremos los conceptos básicos de Programación orientada a objetos (OOP en inglés).
El objetivo es entender que es el paradigma, que intenta solucionar y cuales son sus fundamentos.

## Un poco de historia:
En la prehisotria, cuando los primeros homosapiens comenzaron a darse cuenta que escribir código
es útil, las empresas comenzaron a tener servidores (los denominados *main frames*) y contratar 
muchas personas para manejar dichos servidores y reemplazar tareas administrativas como operaciones 
contables o tareas repetitivas.

![main frame example](../imgs/main-frame-example.jpeg)

Ya para la decada de 1980 gran parte de la sociendad se encontraba en proceso de digitalización,
para este momento los programas había empezado a escalar en complejidad y la cantidad de personas
manejando dichos sistemas. Esta complejización llevó a que se dificulte cada vez más pensar en programas
que funcionen utilizando el paradigma procedural (el que ya conocen).

Esta nueva complejidad, sistemas que empezaban a tener años en servicio y muchas lineas de código,
impulsó a que se busque una nueva forma de encarar el desarrollo de aplicaciones para el sector. Esta
búsqueda culminó en la adopción del paradigma de objeto para mediados de los 90s.

Esto se debió a que los sistemas que se diseñaban con esta mentalidad y estilo eran más mantenibles en
el tiempo y permitían sumar nuevas personas al desarrollo sin tanta fricción al proceso.

## Definiciones:
Veamos un poco de terminología básica.

### Objeto:
Es la unidad básica del paradigma. Se define como una estructura porpia que debe cumplir con
lo siguiente:
- Debe poseer un estado interno
- Debe poseer un comportamiento. Responder ante mensajes del exterior.
- Debe tener una identidad. Una forma de unicidad que identifique a cada objetos único.

En Python esto se logra utilizando el tipo `class`. 

### Método:
Es el comportamiento que le otorgamos a cada objeto.

```python
class MyClass:
    def greet(self):
        print('hello!')

```
En este caso la función `greet` es un método definido para objetos de tipo `MyClass`.

### Atributo:
Son los estados (valores) que un objeto puede poseer.

```python

class MyClass:

    def __init__(self):
        self.name = 'santi'
    
instance = MyClass()

print(instance.name) # muestra 'santi'
```
En este caso, vemos que un objeto de tipo `MyClass` tiene un atributo `name` el cual puede ser accedido
utilizando el operador `.`.


!!! note
    Si te estas preguntando que es `self` o `__init__`, paciencia ... lo veremos más adelante.

## Fundamentos del paradigma:
El fundamento principal del paradigma es que **todo es un objeto** el cual puede tener un estado 
interno y exponer métodos para aceptar interacciones con otros objetos. Sacando lo pomposo de la
frase, ustedes ya conocen algunos objetos como son `list` o `dict`. 

Ustedes no saben como funcionan por dentro, aún así presentan una variedad de métodos para 
comunicarnos con ellos y obtener cosas de los mismos. También sabemos que tiene un estado 
internos que no nos exponen ya que de alguna forma están guardando los elementos que les pedimos.

A partir de esta frase, nacen 4 pialares con los cuales intentamos diseñar las soluciones 
orientadas a objetos. Estos son confusos (parecen escritos por Yoda, pero tienen sentido 
una vez que se acostumbran).

### Encapsulamiento
*Los objetos deben presentar una interfaz con la cual otros puedan comunicarse sin necesidad de entender su implementación.*

La implementación de código no debe ser accesible por quien no corresponde. Es decir, 
si un método de una clase solo sirve para si misma y no debe ser utilizada por otros objetos.
Cuando llamamos a un método, no nos interesa su implementación sino lo que esperamos del mismo.

```python

class Contador:
    def __init__(self):
        self.__counter = 0

    def add_item(self):
        self.__counter += 1
    
    def del_item(self):
        if self.__counter > 0:
            self.__counter -= 1
    
    def get_counter(self) -> int:
        return self.__counter

nuevo_contador = Contador()
nuevo_contador.add_item()
nuevo_contador.del_item()
print('el contador esta en ', nuevo_contador.get_counter())
```
!!! obs
    En este contexto, el usuario de `nuevo_contador` no se preocupa por la implementación de `del_item`. En cambio,
    confía en lo que este método debe hacer y lo invoca para que cumpla su labor.

### Abstracción
*El estado de un objeto solo debe ser visible a quien corresponda e inaccesible a quien no.*

Cada objeto tiene la potestad de ocultar o exponer estados para que otros accedan o no. Es por
este motivo que el comportamiento que necesite de un cierto conjunto de valores, usualmente
va en el mismo objeto. De esa forma todos comparten visibilidad sobre los mismo valores.

En el ejemplo previo, vimos que definimos y utilizamos un estado interno llamado `__counter`, el mismo no
se expone al usuario de nuestra clase. En cambio, definimos métodos para que interactuen con este valor, de
froma que tenemos el control sobre como varía el valor.


!!! obs
    El uso de `__` como comienzo del nombre de atributos dentro de la clase define que no deben
    ser accedidos por entidades fuerda del objeto. Son valores que solo le conciernen al propio objeto.
    Esto es el concepto de `scope` para atributos.


### Polimorfismo
Se refiere a la independencia entre el tipo de un objeto y el método que deseamos ejecutar.
Si tenemos multiples objetos que soportan el mismo método y ejecutan el mismo comportamiento,
aquel que invoque a dicho comportamiento no debe preocuparse de que `tipo` es exactamente el objeto
al cual está llamando.

```python
class Brid:
    def fly(self):
        pass

    def count_wings(self):
        return 2
        

class Parrot(Brid):

    def (self):
        print("flying slowly")


class Hummingbird(Brid):

    def fly(self):
        print("flying really fast")

# common interface
def flying_test(bird: Brid):
    bird.fly()

#instantiate objects
blu = Parrot()
peggy = Hummingbird()

# passing the object
flying_test(blu)
flying_test(peggy)

```

En este ejemplo, vemos que `flyin_test` no necesita saber exactamente que `tipo` es el objeto 
sobre el que está efectuando el llamado al método `fly()` sino que confía en que el objeto 
implementa el método de la forma adecuada para su caso.

!!! obs
    Este también es un caso de herencia, en el cual ambos objetos `blu` y `peggy` tienen el método
    `count_wings` a su disposición dado que ambos son instancias de clases que heredan de `Bird`.

### Inheritance & Composition
Refiere a la habilidad de los objetos de obtener características de otros objetos. Generalmente,
utilizamos esta habilidad para definir comportamientos comunes entre varios objetos.
En el caso de `composition` esto se logra teniendo un objeto como atributo de otro objeto, mientras 
que en `inheritance` logramos esto a través de la herencia de comportamiento y atributos.


```python

class Engine:
    def acelerate(self):
        ...
    
    def slow_down(self):
        ...


class Car:
    
    def __init__(self):
        self.engine = Engine()


```

En este caso utilizamos la **composición** para lograr que la clase `Car` tenga
disponible un `Engine` y su funcionalidad sin tener que realmente escribirla 
como parte de la clase `Car`.

