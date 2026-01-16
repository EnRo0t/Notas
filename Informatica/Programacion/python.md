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

### CASTEO
Un cast es una conversión explicita de un tipo de dato a
otro.

```py
x = str(3) # x será "3"
y = int(3) # y será 3
z = float(3) # z será 3.0 
```

### SABER EL TIPO DE DATO
Para comprobar que tipo de dato es una variable podemos
utilizar type():

```py
x = 5
y = "Aitor"
print(type(x))
print(type(y))
```


