# PYTHON

## ¿QUÉ ES PYTHON?
+ Es un lenguaje de programación interpretado.
+ De alto nivel
+ Tiene POO
+ Posee una sintaxis muy sencilla y ligera

## ENTORNO VIRTUAL
Para crear un entorno virtual en el que
instalar librerias sin alterar la máquina
host:
```bash
python3 -m venv venv

source venv/bin/activate

# Instalar librerias
pip instal nombre_libreria
```
Para salir del entorno virtual:
```bash
deactivate
```
Al desactivar el entorno virtual este permanece de forma local en el
directorio venv.

Si quisieras activarlo de nuevo:

```bash
source venv/bin/activate
```

### IDENTACIÓN
En la mayoría de lenguajes de programación la identación es
una cuestión estética. En Python se utiliza la identación
para identificar bloques de código y es obligatoria. 

Esto funciona
```py
if 5 > 2:
    print("Cinco es mayor que 2")
```

Esto no
```py
if 5 > 2:
print("Cinco es mayor que 2")
```
No importa cuantos espacios utilices, siempre y cuando sea minímo 1.

### VARIABLES
+ En python no es necesario especificar el tipo de dato
  cuando se asigna una variable. Es de tipado dinámico. 
+ Es keysensitive, de tal manera que la variable A y la a
  no son la misma
+ Una variable se crea siempre que se asigne un valor

```py
x = 5
y = "Hello World"
``` 

Para escribir el nombre de las variables podemos utilizar 3 formatos:

**CAMEL CASE**

Consiste en escribir la primera palabra en minúsculas y la
segunda y siguientes en mayúsculas. Sin espacios.

```py
miVariableNombre = "Aitor"
```

**PASCAL CASE**
Cada palabra comienza en mayúscula, incluido la primera.

```py
MiVariableNombre = "Aitor"
```

**SNAKE CASE**
Cada palabra se separa por "_"

```py
mi_variable_nombre = "Aitor"
```
**Asignar multiples variables en la misma línea**

En Python puedes hacer esto:
```py
x, y, z = "Naranja", "Banana", "Cherry"
```

**Asignar un mismo valor a varias variables**

También puedes hacer esto: 
```py
x = y = z = "Naranja"
```

**Asignar valores de una lista o tupla a una serie de variables**

Si tienes una tupla o lista 
```py
# Tienes una lista de frutas
lista_frutas = ["Manzana", "Naranja", "Sandia"]
# Metes cada valor en una variable
x, y, z = lista_frutas
```

### COMENTARIOS
Para escribir un comentario debes utilizar #

```py
#Esto es un comentario
print("Hello World")
```

### MOSTRAR ALGO POR PANTALLA
Para mostrar texto por pantalla utilizamos print()

```py
print("Hola mundo")
```

Si quieres evitar el salto de línea después de un print():
Utiliza end=" "
```py
print("Hello Wordl", end=" ")
print("Lo que sea")
```

**Imprimir número**

Imprimir numeros es exactamente lo mismo, pero sin " ":
```py
print(3)
```

**Concatenar número con String**

Para concatenar numeros con string se utiliza ",":
```py
print("Hola me llamo Bartolo y tengo ", 33, " años")
```

**Imprimir multiples variables a la vez**

```py
x = "Hola "
y = "Mundo "
z = "Que tal? "

print(x, y, z)
```
También puedes utilizar "+" siempre y cuando sean variables del mismo tipo.
Aunque si lo utilizas con números actuara como un operador matemático

```py
x = 2
y = 3
print(x + y)  # Output: 5
```

**Variables globales y de función**

Cuando creas una variable fuera de una función, esta es global.
```py
# Asigno variable global (fuera de la función)
x = "Aitor"

# Creo una función 
def miFuncion():
    # Llamo a dicha variable
    print(x)

# Ejecuto mi función
miFuncion()
```
Esto no es lo mismo que esto otro: 
```py
# Creo una función y asigno una variable dentro
def miFuncion():
    x = "Aitor"
    print(x)

# Ejecuto mi función
miFuncion()
```
En el segundo caso la variable es de función, y no puede ser llamada por otra
función fuera de esta.

Para crear una variable dentro de una función y que esta sea global, utilizamos
la palabra clave global.
```py
# Creo una función y asigno una variable dentro
def miFuncion():
    global x
    x = "Aitor"
    print(x)

# Ejecuto mi función
miFuncion()
```
### TIPOS DE DATO

|Tipo           |nombre                     |nomeclatura                |
|:-------------:|:-------------------------:|:-------------------------:|
|Texto          |String                     |str                        |
|Numeros        |Enteros                    |int                        |
|Numeros        |Coma flotante              |float                      |
|Numeros        |complejos                  |complex                    |
|De secuncia    |lista                      |list                       |
|De secuencia   |tupla                      |tuple                      |
|De secuencia   |rango                      |range                      |
|Mapeado        |diccionario                |dict                       |
|Asignación     |set                        |set                        |
|Asiganción     |frozenset                  |frozenset                  |
|Booleanos      |booleano                   |bool                       |
|Binarios       |byte                       |byte                       |
|Binarios       |bytearray                  |bytearray                  |
|Binarios       |memoryview                 |memoryview                 |
|Sin tipo       |No tipo                    |NoneType                   |

**Saber el tipo de dato**
Para comprobar que tipo de dato es una variable podemos
utilizar type():

```py
x = 5
y = "Aitor"
print(type(x))
print(type(y))
```

**Asignar un tipo de dato a una variable**

En Python no es necesario definir explícitamente el tipo de dato al asignar un
valor a una variable, ya que es un lenguaje de tipado dinámico.  El tipo de
dato se determina de forma implícita según el valor asignado, y está asociado
al objeto al que la variable hace referencia.

Ejemplos:

|Tipo de dato                 |Asignación                          |
|:---------------------------:|:----------------------------------:|
|str                          |x = "Hola mundo"                    |
|int                          |x = 20                              |
|float                        |x = 20.5                            |
|complex                      |x = 1j                              |
|list                         |x = ["Manzana","Pera","Naranja"]    |
|tuple                        |x = ("Manazana","Pera,"Naranja")    |
|range                        |x = range(6)                        |
|dict                         |x = {"nombre": "John", "edad" : 33} |           
|set                          |x = {"Manazana", "Banana", "Fresa"} |
|frozenset                    |x = ({"Manzana", "Banana", "Fresa"})|
|bool                         |x = true                            |
|bytes                        |x = b"Hello"                        |
|bytearray                    |x = bytearray(5)                    |
|memoryview                   |x = memoryview(bytes(5))            |
|None                         |x = None                            |

A pesar de que no es estrictamente necesario, sí podemos explicitar el tipo de
dato de una variable.

|Tipo de dato                 |Asignación                                |
|:---------------------------:|:----------------------------------------:|
|str                          |x = str("Hola mundo")                     |
|int                          |x = int(20)                               |
|float                        |x = float(20.5)                           |
|complex                      |x = complex(1j)                           |
|list                         |x = list(("Manzana","Pera","Naranja"))    |
|tuple                        |x = tuple(("Manazana","Pera,"Naranja"))   |
|range                        |x = range(6)                              |
|dict                         |x = ("nombre": "John", "edad" : 33)       |           
|set                          |x = (("Manazana", "Banana", "Fresa"))     |
|frozenset                    |x = (("Manzana", "Banana", "Fresa"))      |
|bool                         |x = bool(5)                               |
|bytes                        |x = bytes(5)                              |
|bytearray                    |x = bytearray(5)                          |
|memoryview                   |x = memoryview(bytes(5))                  |
|None                         |x = None                                  |


### CASTEO
Un cast es una conversión explicita de un tipo de dato a
otro.

```py
x = str(3) # x será "3"
y = int(3) # y será 3
z = float(3) # z será 3.0 
```

## STRINGS

**Meter comillas dentro de otras comillas**

Puedes utilizar comillas simples para meter comillas dentro de otras comillas. 
```py
print("Hola a todos 'sobretodo a la buena gente'")
```

**Strings multilinea**

```py
 a = """Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."""
print(a) 
```

**Los Strings son ARRAYS**

Este es un concepto importante a tener en cuenta. Un String actua como un array
de carácteres. 

```py
a = "Hello Word"
print(a[1]) # Me devolveria "e"
```
Hay que tener en cuenta que el indice empieza siempre en 0

**Recorrer un String como si fuera un ARRAY (lo es)**

```py
for x in "Aitor"
    print(x)
```

**Conocer longitud de un String**

```py
a = "Hello World"
print(len(a))
```

**Comprobar si un String contiene una palabra**

```py
txt = "Las mejores cosas del mundo son gratis"
print("gratis" in txt)
```

Esto también lo podríamos utilizar dentro de un if
```py
txt = "Las mejores cosas del mundo son gratis"
if "gratis" in txt:
    print("'Gratis' esta en el texto")
```

**Comprobar que un String NO contiene una palabra**

```py
txt = "Las mejores cosas del mundo son gratis"
print("gratis" not in txt)
```

### DIVIDIR STRINGS

Puedes dividir un string, desde un punto a otro simplemente indicando un indice:
```py
b = "Hola Mundo"
print(b[2:5]) # Corta desde "o" hasta "M" sin incluirlos. Es decir: la (El espacio cuenta)
```

**Dividir desde el principio**

```py
b = "Hola Mundo"
print(b[:5]) # Desde el principio hasta el 4 carácter
```

**Dividir hasta el final** 

```py
b = "Hola Mundo"
print(b[2:]) # Desde el tercer carácter hasta el final. Es decir: la Mundo
```

**Indexación negativa**

```py
b = "Hola Mundo"
print(b[-5:-2]) # Contando desde el final
```

### MODIFICAR STRINGS
    
**Convertir a mayúsculas**

```py
a = "Hello World"
print(a.upper())
```

**Convertir a minúsculas**

```py
a = "Hello World"
print(a.lower())
```

**Eliminar espacio en blanco**

```py
a = "Hello World "
print(a.strip()) # Elimina el espacio en blanco del final
```

**Remplazar un String**

```py
a = "Hello World "
print(a.replace("H", "J")) # Remplaza H por J
```

**Dividir un String y que retorne una lista**

```py
a = "Hello, World "
print(a.split(",")) # Utilizará la coma para separar los elementos de la lista
# Devolverá: ["Hello", " World!"] 
```

### CONCATENACIÓN DE STRINGS

```py
a = "Hello"
b = "World"

c = a + b

print(c) # HelloWorld
```

### FORMATEO DE STRINGS

**Fstring**

Con "f" podemos formatear un string y añadir las variables con {}:
Este es el método más utilizado en la actualidad.

```py
edad = 33
txt = f"Mi nombre es Aitor y tengo {edad} años"
```

En el placeholder {} pueden ir variables, operaciones, funciones...

**Carácteres de escape**

Podemos escapar ciertos carácteres con "\"


|código             |Resultado                                  |
|:-----------------:|:-----------------------------------------:|
|\'                 |Comilla simple                             |
|\ \                |Barra inversa                              |
|\n                 |Salto de línea                             |
|\r                 |Carriage return                            |
|\t                 |Tabulación                                 |
|\b                 |backspace                                  |
|\f                 |Form feed                                  |
|\ooo               |Valor Octal                                |
|\xhh               |Valor Hexadecimal                          |

### MÉTODOS STRING

|Métodos                     |Descripción                                  |
|:--------------------------:|:-------------------------------------------:|
|capitalize()                |Convierte el primer carácter en mayúscula    ||casefold()                  |Convierte el string en minúscula             |
|center()                    |Retorna un String centrado                   |
|count()                     |Retorna el número de veces que un valor especifico se repite en un string|
|encode()                    |Retorna una version encodeada del String     |
|endswitch()                 |Retorna true si el String termina en un valor especifico|
|expandtabs()                |Setea el tamaño de la tabulación en un String|
|find()                      |Busca un valor especifico en el String y retorna su posición|
|format()                    |Formatea valores especificos en un String    |
|format_\map()               |Formate valores especificos de un String     |
|index()                     |Lo mismo que find                            |
|isalnum()                   |Retorna true si todos los carácteres son alfanúmericos|
|isaplha()                   |Retorna true si todos son alfabeticos       | |isascii()                   |Retorna true si todos son ascii             | |isdecimal()                 |Retorna true si todos son decimales         |
|isdigit()                   |Retorna true si todos son digitos           |
|isidentifier()              |Retorna true si todos son identifier        |
|islower()                   |Retorna true si todos son minúscula         |
|isnumeric()                 |Retorna true si todos son numeric           |
|isprintable()               |Retorna true si todos son printeables       |
|isspace()                   |Retorna true si todos son espacios en blanco|
|istitle()                   |Retorna true si el string sigue las relgas de un titulo|
|isupper()                   |Retorna true si todos son mayúscula         |
|join()                      |Une elementos de un iterable al final de un String|
|ljust()                     |Retorna un string justificado a la izquierda |
|lower()                     |Convierte un String en minúscula             |
|lstrip()                    |Elimina carácteres vacios a la izquierda    |
|maketrans()                 |Retorna una traslación de una tabla         |
|partition()                 |Retorna una tupla donde el string es partido en tres partes|
|replace()                   |Remplaza una parte de un string             |
|split()                     |Divide el String según un separador         |
|splitlines()                |Divide el string en el salto de linea y devuelve una lista|
|startswith()                |Retorna true si el string empieza por un valorespecifico|
|strip()                     |Retorna un string "trimeado"                |
|swapcase()                  |Cambia de mayus a minus y viceversa         |
|title()                     |Cambia el primer carácter de cada palabra a mayúscula|
|translate()                 |Retorna un string trasnlated                |
|upper()                     |Convierte un String a mayúscula             |
|zfill()                     |Llena un string desde el inicio con un número especifico de ceros|

