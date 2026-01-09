# JAVASCRIPT

## SINTAXIS BÁSICA

### VARIABLES
Javascript es un lenguaje de tipado dinámico, eso significa que no hay que
espeficiar el tipo de dato cuando se declara una variable.

let: Para variables locales.
 
var: Para variables globales, no recomendado.

EJ:
```js
let nombre = "Jaime";
let edad = 19;
let fondos = 6500.90;
let pobre = true;
```

### CONSTANTES
```js
const nombre_constante = "valor";
```

### ARRAYS
**Crear un array**
```js
let lista_frutas = ["Manzana", "Pera", "Melecoton"];
```
**Acceder a un objeto del array**
```js
console.log(lista_frutas[0]) //Esto devolveria Manzana;
```
**Recorrer un array con un for**
```js
for(i = 0; i < lista_frutas.length; i++) {
    console.log(lista_frutas[i]);
}
```
**Recorrer un array con un forEach (ideal)**

ForEach lo que va a hacer es ejecutar algo por cada elemento del array.
```js
lista_frutas.forEach(function(fruta) {
    console.log(fruta); //Esto devolvería: Manzana Pera...   
});
```
Aparte de añadir por parámetro una variable que representara cada elemento,
también se puede añadir a continuación el indice del elemento en el array y el
nombre del array.
```js
lista_frutas.forEach(functio(fruta, indice, array {
    console.log(fruta, indice, array); //Esto devolveria: Manzana 0 lista_frutas...
}
``` 
**Añadir un elemento al final de un array**
```js
lista_frutas.push("Melón");
```

**Eliminar el último elemento del array**
```js
lista_frutas.pop();
```

**Añadir elemento al principio del array**
```js
lista_frutas.unshift("Melón");
```
**Eliminar el primer elemento del array**
```js
lista_frutas.shift();
```

**Encontrar el índice de un elemento del array**
```js
lista_frutas.indexOf("Manzana");
```
**Comprobar si existe un elemento**
```js
lista_frutas.includes("Manzana"); //Devolvería true
```

**Eliminar elemento mediante su posición**
```js
lista_frutas.splice(pos,numero_elementos);
lista_frutas.splice(0,1); //Eliminaria manzana 
```

**Copiar un array**
```js
let copiaArray = lista_frutas.slice();
```

**Ver la cantidad de elementos de un array**
```js
console.log(lista_frutas.length);
```

### OPERADORES DE ASIGNACIÓN
|nombre                   |   operador|     significado|
|:-----------------------:|:---------:|:--------------:|
|Asignación               |x = y      |x = y           |
|Asignación suma          |x += y     |x = x + y       |
|Asignación multiplicación|x \*= y    |x = x * y       |
|Asignación división      |x /= y     |x = x / y       |

Existen  muchos más pero menos frecuentes.

### OPERADORES ARITMETICOS
|nombre            |simbolo     |
|:----------------:|:----------:|
|suma              |+           |
|resta             |-           |
|multiplicación    |*           |
|división          |/           |
|residuo           |%           |
|incremento        |++          |
|decremento        |--          |
|potencia          |**          |

### OPERADORES DE COMPARACIÓN
|nombre                     |descripción                                  |ejemplos true            |
|:-------------------------:|:-------------------------------------------:|:-----------------------:|
|igual (==)                 |Devuelve true si los operandos son iguales   |let n = 1; n == 1        |
|No igual (!=)              |Devuelve true si los operandos son diferentes|let n = 1; n != 2        |
|Igualdad estricta (===)    |True si es igual y del mismo tipo            |1 === 1                  |
|Desigualdad estricta(!==)  |True si son del mismo tipo pero no iguales   |1 !== 2                  |
|Mayor que (>)              |True si el valor es mayor                    |5 > 4                    |
|Menor que (<)              |True si el valor es menor                    |4 < 5                    |
|Mayor o igual (>=)         |True si es mayor o igual                     |5 >= 6; 5>= 5            |
|Menor o igual (<=)         |True si es menor o igual                     |4 <= 5; 4<=4             |

### OPERADORES LÓGICOS
|nombre                     |descripción                                  |ejemplos                 |
|:-------------------------:|:-------------------------------------------:|:-----------------------:|
|AND (&&)                   |Se deben cumplir ambas condiciones           |expr1 && expr2           |
|OR (\|\|)                  |Se debe cumplir o una u otra condición       |expr1 \|\| expr2         |
|NOT (!)                    |Se debe cumplir lo opuesto                   |!expr1                   |

### OPERADORES DE CADENA (concatenación)
Podemos unir valores con '+'.
Ej:
```js
let nombre = "Jaime";
console.log("Hola este es un mensaje para " + nombre + ".";
```

### OPERANDO TYPEOF
Devuelve el tipo de dato de una variable:
```js
var myFun = new Function("5 + 2");
var shape = "round";
var size = 1;
var foo = ["Apple", "Mango", "Orange"];
var today = new Date();
```

```js
typeof myFun; //Devuelve function
typeof shape; //Devuelve String
typeof size; //Devuelve numbre
typeof foo; //Devuelve object
typeof today; //Devuelve object
typeof nonexist; //Devuelve undefined
```
### OPERADOR INSTANCEOF
El operador instanceof devuelve true si las dos variables que compara son del mismo tipo:
```js
var theDay = new Date(1995, 12, 17);
if (theDay instanceof Date) {
  // instrucciones a ejecutar
}
```
### CONDICIONAL IF-ELSE
```js
if(condición) {
    //Ejecuta esto
} else {
    //Sino ejecuta esto otro
}
```

### CONDICIONAL IF-ELSE IF 
```js
if(condicion1) {
    //Ejecuta esto
} else if(condicion2) {
    //Ejecuta esto otro
} else {
    //Sino ejecuta esto otro
}
```
### SWITCH
```js
switch(expresion) {
    case1:
        //Ejecuta esto
    break;
    case2: 
        //Ejecuta esto otro
    break;
    case3:
        //Ejecuta esto
    break;
}
```

### CONDICIONAL OPERADOR TERNARIO
Es como un if else pero en una linea.

condicion ? val1 : val2
Si la condución es true el valor es val1 sino es val2.

```js
var status = age >= 18 ? "adult" : "minor";
```

### BUCLES
**Bucle FOR**

El bucle for itera sobre un indice, en el caso de ejemplo a cada iteración i + 1, hasta llegar a 100. 
```js
for(i = 0; i < 100; i++) {
    //Ejecuta esto
}
```

**Bucle While**

El bucle while se repite hasta que la condición deje de ser cierta. 
```js
while(condicion) {
    //Ejecuta esto
}
```

### ENTRADAS DE USUARIO
Puedes pedir al usuario que introduzca un valor con prompt:
```js
let nombre = prompt("Introduce tu nombre");
```

### VALIDACIONES DE ENTRADAS
**Validar que se trata de un número**

Para ello tenemos isNaN (is not a number)
```js
let numero = prompt("Introduce un número");
if(isNaN) {
    console.log("El valor introducido no es un número");
} else {
    console.log("Si se trata de un número");
}
```
**Validar que un string no esta vacio o es nulo**
```js
let nombre = prompt("Introduce tu nombre");
if(nombre === null || nombre.trim() === ""){
    console.log("El valor esta vacio o es nulo");
} else {
    console.log("El valor es correcto");
}
```
**Validación de input number completo con while**
```js
//Pedimos al usuario un número
let numero = prompt("Ingresi un número");

//Mediante un bucle verificamos que se trate de un número, no un string, valor vacio o nulo
while(numero === null || numero.trim() === "" || isNaN(numero) || numero < 1){
	//De ser un valor incorrecto, avisamos y volvemos a pedir
	alert("El valor introduït no es vàlid");
	numero = prompt("Torni a ingresar un valor");
}
//Una vez pasada la verificación, convertimos el input en number explicitamente
let numero_valid = Number(numero);
```
### CONVERSION DE TIPOS
**Convertir String a Number**

```js
let palabra = "Armario";
let numero = "123";

Number(palabra); //Esto se convienrte en NaN
Number(numero); //Esto se convierte en 123
```
**Convertir String a Array con Spread Operator (...)**

Aunque los Strings en js son iterables, eso no los convierte en arrays.

```js
let stringEjemplo = "Hola";

const arr = [...stringEjemplo];
```

### TRATAMIENTO STRINGS
**Eliminar espacios**

```js
let ejemplo = "ejemplo ";
console.log(ejemplo.trim()); //Devuelve la palabra sin espacio al final.
```
**Convertir a minúsculas**

```js
let string_ejemplo = "HOLA";
console.log(string_ejemplo.toLowerCase()); //Esto devolverá hola
```
**Convertir a mayúscula**

```js
let string_ejemplo = "hola";
console.log(string_ejemplo.toUpperCase(); //Esto devolverá HOLA
``` 

### FUNCIONES
Una función es un conjunto de operaciones.

**Ejemplo de función que comprueba si un número es par**
```js

let x = 3;
//Creamos la función. Por parámetro ponemos una palabra que clarifique el tipo de dato del input.
function esPar(numero) {
    if(numero % 2 === 0) {
        console.log(numero + " es par");
    } else {
        console.log(numero + " es impar");
    }
}

esPar(x); //Ejecutamos la función
```

### FUNCIONES MATÉMATICAS
**Comprobar si un número es par**

Dado un número introducido por el usuario y verificado:
```js
function esParell(num){
	if(numero_valid % 2 === 0) {
		alert(numero_valid + " es par");
	} else {
		alert(numero_valid + " es impar");
	}
}

esParell(numero_valid);
```

**Calcular factorial de un número**

El factorial de un número es el resultado del producto de todos los números
enteros positivos menores o iguales a él.

Dado un número introducido por el usuario y verificado:
```js
function factorial(num) {
        let resultado = 1;		
	for(let i = 1; i <= num; i++) {
		resultado *= i;		
	}
	return resultado;
}

alert(factorial(numero_valid));
```
La clave aquí es el operando *=.

**Comprobar si un número es primo o compuesto**

Dado un número introducido por el usuario y verificado:
```js
function esPrimo(num) {
  if (num < 2) return false;

  const limit = Math.sqrt(num);

  for (let i = 2; i <= limit; i++) {
    if (num % i === 0) {
      return false; // compuesto → salir
    }
  }

  return true; // ninguno dividió
}

```
La idea es convertir el algoritmo de división por tentativa en código.
 
Si divides un número entero compuesto por todos los números enteros > 2 hasta
la raíz de dicho número y ninguno de ellos tiene residuo 0, entonces estas ante
un primo. 

## OBJETOS
Son un tipo de dato capaz de almacenar colecciones de datos de varios tipos.

Podemos crear objetos utilizando las llaves { } para otorgarle propiedades en
formato clave:valor. Siendo la clave un string que identificara al objeto.
```js
let user = {
	nombre:"Aitor", //Clave
	edad:33 //Valor
};
```
También podemos generar objetos vacios:
    
```js
let user = new Object(); //Sintaxis de constructor de objetos
```
    
Podemos acceder a esos valores mediante un “.”
    
```js
alert(user.nombre); //Aitor
alert(user.edad); //33
```
    
También podemos añadir una propiedad de cualquier tipo de dato:
    
```js
user.isAdmin = true; //Le otorgamos un valor booleano
    
//Esto sería como hacer
let user = {
    nombre: "Aitor",
    edad: 33,
    isAdmin: true
};
```
    
Podemos eliminar una propiedad con el operador **delete**:
    
```js
delete user.isAdmin; //Eliminamos la propiedad isAdmin
```
    
Podemos añadir propiedades de más de una palabra, pero deben ir
entrecomilladas:
    
```js
let user = {
    name: "John",
    age: 30,
    "likes birds": true  // Las claves con más de una palabra deben ir entre comillas
};
```
    
La última propiedad puede terminar en “,” para facilitar la entrada de nuevas
propiedades (coma colgante):
    
```js
let user = {
    name: "John",
    age: 30,
}
```
    

### CORCHETES
Si queremos acceder a una propiedad de más de una palabra, no lo podremos hacer
con “.”, lo deberemos hacer mediante [ ]:
    
```js
let user = {};   
// asignando
user["likes birds"] = true;
    
// obteniendo
alert(user["likes birds"]); // true
    
// eliminando
delete user["likes birds"];
```
    
Los corchetes también brindan una forma de obtener el nombre de la propiedad
desde el resultado de una expresión (a diferencia de la cadena literal). Por
ejemplo, a través de una variable:
    
```js
let key = "likes birds";
    
// Tal cual: user["likes birds"] = true;
user[key] = true;
```
    
Podemos utilizar los corchetes cuando necesitemos que se calcule una propiedad
en tiempo de ejecución, por ejemplo, en una propiedad que le pedimos al
usuario:
    
```js
let user = {
    name: "John",
    age: 30
};
    
let key = prompt("¿Qué te gustaría saber acerca del usuario?", "name");
    
// acceso por medio de una variable
alert( user[key] ); // John (si se ingresara "name")
```
    
No podemos utilizar la notación “.” de esta manera:
    
```js
let user = {
    name: "John",
    age: 30
};
    
let key = "name";
alert( user.key ) // undefined
```
    

### PROPIEDADES CALCULADAS
Podemos utilizar corchetes a la hora de crear un objeto literal:
    
```js
let fruit = prompt("¿Qué fruta comprar?", "Manzana");
    
let bag = {
    [fruit]: 5, // El nombre de la propiedad se obtiene de la variable fruit
};
    
alert( bag.apple ); // 5 si fruit es="apple"
```

El significado de una propiedad calculada es simple: `[fruit]` significa que se
debe tomar la clave de la propiedad `fruit`.  Entonces, si un visitante
ingresa `"apple"`, `bag` se convertirá en `{apple: 5}`.

### PRUEBA DE PROPIEDAD EXISTENTE
En JavaScript puedes comprobar si una propiedad existe dentro de un objeto. De
no existir, esto no lanza un error, sino que “convierte” la propiedad
inexistente en undefined. Para comprobar si una propiedad existe tenemos el
operador “in”:

```js
let user = {
	nombre: Aitor,
	edad: 33,
}

alert("apellido" in user); //Mostraría un false
alert("nombre" in user); //Mostraría un true

Por tanto podriamos 
let hasName = "apellido" in user;

if (hasName) {
	alert("hello " + user.nombre + user.apellido);
} else {
	alert("hello " + user.nombre);
}
```
Si en lugar de una clave queremos hacer referencia a una variable, la pondremos
sin las “”.

### BUCLE FOR IN
Para recorrer todas las propiedades de un objeto existe el bucle for in:
    
```js
// Tenemos el objeto user:
let user = {
    nombre: "Aitor",
    edad: 33
};
    
// Queremos recorrer todas las claves (los nombres de las claves, no los valores)
for (key in user) {
    console.log(key); //Esto devolverá nombre edad
}
    
//Si queremos recorrer los valores de las claves:
for (let key in user) {
    console.log(user[key]); //Esto devolverá Aitor 33
}
    
//Combinado ambas cosas:
for (ley key in user) {
    console.log(key + " " + user[key]); //Devolverá nombre Aitor edad 33
}
```
    

### ORDEN DE LAS PROPIEDADES
Las propiedades aparecerán ordenadas por orden de creación, a no ser que por
clave les pongamos un número, entonces aparecerán ordenadas por orden numérico.

### REFERENCIAS A OBJETOS Y COPIA

Una de las diferencias fundamentales entre los tipos primitivos y los objetos
es que los primitivos almacenan directamente su valor, mientras que en los
objetos la variable almacena una referencia a la ubicación en memoria donde se
encuentra el objeto.

```js
// Imagina 2 primitivos tipo String
let mensaje = "Hola mundo";
let frase = mensaje;

// En ambos casos el mensaje será el mismo.
console.log(mensaje);
console.log(frase);
```

Esto parece una obviedad, pero en el caso de los objetos no funciona así. 

```js
// Tenemos un objeto:
let user = {
  name: "John"
};
```

En este caso, la variable user no contiene el objeto, sino una referencia a
este, una dirección de memoria. 

De este modo, podemos copiar la referencia:

```js
let user = {
  name: "John"
};

let admin = user;
```

Ahora hay dos variables apuntando al mismo espacio de memoria. admin y user.

Si hacemos cualquier cambio en una de ellas, este cambio se reflejará en la otra. 

### COMPARACIÓN POR REFERENCIA
Dos objetos son iguales si apuntan a la misma dirección de memoria, es decir,
son iguales si son el mismo objeto, el mismo, no uno idéntico.
    
```js
let a = {};
let b = a;
    
console.log(a == b); // Esto devuelve true
console.log(a === b); // Esto también
    
let a = {};
let b = {};
    
console.log(a == b); // Esto devuelve false
console.log(a === b); // Esto también
```
    

### CLONES
Si cuando hacemos:
    
```js
let a = {};
let b = {};
    
let b = a;
```
    

No estamos creando un objeto diferente con las mismas propiedades idénticas,
sino una nueva referencia al mismo objeto. ¿Cómo clonamos un objeto?

Respuesta: Iterando sobre sus propiedades con un for in:

```js
// Creamos el objeto original
let a = {
	nombre: "Aitor",
	edad: 33
};

// Inicializamos el objeto clon
let clon = {};

// Iteramos sobre las propiedades de a y las igualamos en clon
for(let key in a) {
	clon[key] = a[key];
}

clon.nombre = "Peter"; // Ahora el objeto clon tiene la propiedad nombre, podemos modificarla
console.log(a.nombre); // Esto devolvería Aitor porque no ha sido modificado. 
```

Esto se puede hacer de manera más sencilla con Object.assign(dest,…sources);

Donde dest es el objeto de destino y sources desde donde toma.

```js
let user = {
	nombre: "Aitor"
};

let objetoRandom = {
	edad: 33
};

let objetoRandom2 = {
	isAdmin = true
};

Object.assign(user, objetoRandom, objetoRandom2);

console.log(user.nombre + " " + user.edad + " " + user.isAdmin); // Esto devolverá Aitor 33 true
```

Si la propiedad ya existe se sobrescribe su valor. 

También podemos utilizar object assign para hacer una clonación simple:

```js
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user);

alert(clone.name); // John
alert(clone.age); // 30
```

### CLONACIÓN ANIDADA
Hasta ahora hemos visto como las propiedades de un objeto son primitivas, pero
también se pueden tener propiedades que hagan referencia a otros objetos:

```js
let user = {
	nombre: "John",
	tamaño: { // Propiedad objeto
		altura: 1.85,
		peso: 80
	}
};

console.log(user.tamaño.altura); // Devolvería 1.85
```

Ahora no es suficiente copiar `clone.sizes = user.sizes`, porque `user.sizes` es un objeto y será copiado por referencia. Entonces `clone` y `user` compartirán las mismas tallas (.sizes):

```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

alert( user.sizes === clone.sizes ); // true, el mismo objeto

// user y clone comparten sizes
user.sizes.width = 60;       // cambia la propiedad en un lugar
alert(clone.sizes.width); // 60, obtiene el resultado desde el otro

```

Para corregir esto, debemos hacer que `user` y `clone` sean objetos
completamente separados, debemos usar un bucle que examine cada valor
de `user[key]` y, si es un objeto, que replique su estructura también. Esto es
conocido como “clonación profunda” o “clonación estructurada”. Existe un
método [structuredClone](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone) que
implementa tal clonación profunda.

### STRUCTUREDCLONE
La llamada a `structuredClone(object)` clona el `object` con todas sus propiedadas anidadas.

```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = structuredClone(user);

alert( user.sizes === clone.sizes ); // false, objetos diferentes

// ahora user y clone están totalmente separados
user.sizes.width = 60;    // cambia una propiedad de un lugar
alert(clone.sizes.width); // 50, no están relacionados
```

El método `structuredClone` puede clonar la mayoría de los tipos de datos, como
objetos, arrays, valores primitivos.

También soporta referencias circulares, cuando una propiedad de objeto
referencia el objeto mismo (directamente o por una cadena de referencias).

Por ejemplo:

```js
let user = {};
// hagamos una referencia circular
// user.me referencia user a sí mismo
user.me = user;

let clone = structuredClone(user);
alert(clone.me === clone); // true
```

Como puedes ver, `clone.me` hace referencia a `clone`, no a `user`! Así que la
referencia circular fue clonada correctamente también.

Pero hay casos en que `structuredClone` falla.

Por ejemplo, cuando un objeto tienen una propiedad “function”:

```js
// error
structuredClone({
  f: function() {}
});
```

Las propiedades de función no están soportadas.

Para manejar estos casos complejos podemos necesitar una combinación de métodos
de clonación, escribir código personalizado o, para no reinventar la rueda,
tomar una implementación existente, por
ejemplo [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep) de la librería
JavaScript [lodash](https://lodash.com/).

### THIS
Igual que a un objeto le podemos añadir una propiedad como un tipo de dato
primitivo o como un objeto, también le podemos dar una función. 

```js
// Creamos un objeto con 2 propiedades
let user = {
	nombre:"Aitor",
	edad:33
};

// Le añadimos al objeto la funcion diHola como propiedad
user.diHola = function() {
	alert("Holaaaa");
};

user.diHola(); //Esto devolverá un popup con "Holaaaa"
```

Una función que es propiedad de un objeto es llamado “su método”.

## DOM 
El DOM (Document Object Model) es la estructura que crea el navegador para
representar un documento HTML como un conjunto de objetos. Gracias al DOM,
JavaScript puede acceder, modificar y reaccionar a los elementos de la página.

### SELECCIONAR ELEMENTOS DEL DOM
En algún momento va a interesarnos seleccionar un elemento de un HTML, bien sea
para extraer información o para modificarlo.  Hay diversas maneras de
seleccionar un elemento.

**Seleccionar elemento por su id**

html:
```html
<p id="parrafo">Holaaaa</p>
```
js:
```js
document.getElementById("parrafo");
``` 

**Seleccionar elementos por su clase**

html:
```html
<p class="parrafos">Holaaa</p>
```
js:
```js
document.getElementsByClassName("parrafos");
```

**Seleccionar elementos por nombre de etiqueta**

html:
```html
<p>hola</p>
```
js:
```js
document.getElementsByTagName("p");
```
**Seleccionar primer elemento que coincida con el selector CSS**

html:
```html
<p class=parrafos>Holaaa</p>
```
css:
```css
.parrafos {
    background-color: red;
}
```
js
```js
document.querySelector(".parrafos");
```

**Seleccionar todos los elementos que coiciden con el selector CSS**
html:
```html
<p class=parrafos>Holaaa</p>
```
css:
```css
.parrafos {
    background-color: red;
}
```
js
```js
document.querySelectorAll(".parrafos");
```

### MODIFICAR/OBTENER ELEMENTOS DEL DOM
Ahora que sabemos como seleccionar elementos, vamos a modificarlos. 

**Cambiar el texto de un elemento (borra el contenido anterior)**

```js
const elemento = document.getElementById('mi-elemento');
elemento.textContent = 'Nuevo contenido de texto';
```

**Cambiar contenido del html completo**
```js
const elemento = document.getElementById('mi-elemento');
elemento.innerHTML = '<strong>Texto en negrita</strong>';
```

**Cambiar el texto visible**
```js
const elemento = document.getElementById('mi-elemento');
elemento.innerText = 'Nuevo contenido de texto';
```
**Cambiar un valor en un formulario**

Se usa en: \<input\>, \<textarea\>, \<select\>

html:
```html
<input type="text" id="nombre">
```
```js
let input = document.querySelector("#nombre");

// Obtener el valor
console.log(input.value);

// Cambiar el valor
input.value = "Juan";
```

**Cambiar clase CSS**

html: 
```html
<p id="texto">Hola</p>
```
css:
```css
.rojo {
    color: red;
}
```
js:
```js
let p = document.querySelector("#texto");

// Añadir clase
p.classList.add("rojo");

// Quitar clase
p.classList.remove("rojo");

// Alternar clase
p.classList.toggle("rojo");
```
Aclaración sobre Toggle: Si la clase no existe, la añade. Si la clase existe,
la quita.

**Modificar estilos CSS**

html:
```html
<p id="parrafo">Hola</p>
```
js:
```js
let p = document.querySelector("#parrafo");

p.style.color = "blue";
p.style.backgroundColor = "yellow";
p.style.fontSize = "20px";
```
Apunte sobre buenas prácticas: Style se usa para cambios pequeños, para cambios
grandes mejor utilizar classList.

### EVENTOS
Los eventos son cosas que suceden en el sistema que estas programando. Js puede
capturar dichos eventos y ejercer acciones en consecuencia.
Un ejemplo claro de evento sería el que sucede cuando un usuario presiona un
botón en un HTML. Con Js podemos "capturar" dicho evento mediante un listener y
devolver una acción.

**Eventos frecuentes**

Hay demasiados eventos para nombrarlos todos aquí, pero estos son los más habituales:

|nombre           |tipo         |descripción                                   |
|:---------------:|:-----------:|:--------------------------------------------:|
|click            |ratón        |Cuando se hace clic                           |
|dblclick         |ratón        |Doble clic                                    |
|mousedown        |ratón        |Botón presionado                              |
|mouseup          |ratón        |Botón liberado                                |
|mousemove        |ratón        |Movimiento del mouse                          |
|mouseover        |ratón        |El mouse entra en un elemento                 |
|mouseout         |ratón        |El mouse sale del elemento                    |
|mouseenter       |ratón        |El mouse entra al elemento (no se propaga)    |
|mouseleave       |ratón        |El mouse sale del elemento (no se propaga)    |
|                 |             |                                              |
|keydown          |teclado      |Tecla presionada                              |
|keyup            |teclado      |Tecla liberada                                |
|keypress         |teclado      |(obsoleto, no usar)                           |
|                 |             |                                              |
|submit           |formulario   |Envío de formulario                           |
|change           |formulario   |Cambio de valor                               |
|input            |formulario   |Mientras el usuario escribe                   |
|focus            |formulario   |Cuando el elemento recibe foco                |
|blur             |formulario   |Cuando pierde el foco                         |
|reset            |formulario   |Reinicio del formulario                       |
|                 |             |                                              |
|load             |navegador    |Cuando la pagina termina de cargar            |
|DOMContentLoader |navegador    |Cuando el HTML esta listo                     |
|resize           |navegador    |Cambio de tamaño de la ventana                |
|scroll           |navegador    |Desplazamiento de la página                   |
|beforeunload     |navegador    |Antes de salir de la página                   |

**Capturar eventos**

Para capturar eventos podemos utilizar el listener addEventListener.
La sintaxis es:
```js
elemento.addEventListener("nombre_evento",funcion);
```
Ejemplo:
```js
//Vamos a suponer que en el html hay un botón con el id botón
const btn = document.getElementById("botón"); //Seleccionamos dicho botón

//Ahora capturamos el clic en el botón y ejecutamos la función cambiarFondo
btn.addEventListener("click",cambiarFondo);

//Creamos una función que cambiará el color del fondo
function cambiarFondo() {
    document.body.style.backgroundColor = "red";
}
```
También puedes escribir la función directamente en la misma linea:
```js
btn.addEventListener("click",function() {
    document.body.style.backgroundColor = "red";
});
```
O utilizar la función flecha:
```js
btn.addEventListener("click", () => {
    document.body.style.backgroundColor = "red";
});
```
**Capturar eventos con on**

addEventListener es la mejor manera de capturar eventos, pero no la única. Hay
objetos (como botones) que tienen la propiedad *event handler* que les permite
capturar eventos.
 
Ejemplo:
```js
//Vamos a suponer que en el html hay un botón con el id botón
const btn = document.getElementById("botón"); //Seleccionamos dicho botón

//Ahora capturamos el clic en el botón y ejecutamos la función cambiarFondo
btn.onclick = cambiarFondo;

//Creamos una función que cambiará el color del fondo
function cambiarFondo() {
    document.body.style.backgroundColor = "red";
}
```

**Objeto event**

El objeto event, evt o e, es un objeto que hace referencia al propio evento. Se
le puede pasar a una función para obtener características extra. 
Un ejemplo clásico es el de poder utilizar target, que selecciona el elemento
en sí que ha lanzado el evento. 

Ejemplo:
```js
//Vamos a suponer que en el html hay un botón con el id botón
const btn = document.getElementById("botón"); //Seleccionamos dicho botón

//Ahora capturamos el clic en el botón y ejecutamos la función cambiarFondo
btn.addEventListener("click",cambiarFondo);

//Creamos una función que cambiará el color del fondo del elemento
function cambiarFondo(e) {
    e.target.style.backgroundColor = "red";
}
```
Otra información extra que podemos obtener gracias a pasar el objeto event como
parámetro de la función manejadora son:

+ e.currentTarget: Elemento que escucha el evento.
+ e.type: Tipo de evento (click, keydown, etc).
+ e.timeStamp: Momento en que ocurrió el evento.
+ e.clientX: Coordenada X dentro de la ventana.
+ e.clientY: Coordenada Y dentro de la ventana.
+ e.pageX: Coordenada X dentro de la página.
+ e.pageY: Coordenada Y dentro de la página.
+ e.button: Botón presionado (0 izquierdo, 1 rueda, 2 derecho).
+ e.key: Tecla presionada ("a", "Enter", "Escape").
+ e.code: Tecla presionada ("KeyA", "Enter").
+ e.preventDefault();: Previene el comportamiento por defecto en un formulario.
  (Por ejemplo, evitar que se envie)
+ e.stopPropagation(): Detiene la propagación. 

### CREAR Y ELIMINAR ELEMENTOS

**Crear elementos del DOM**

+ createElement: Crea un elemento, pero no lo agrega todavía.
```js
const p = document.createElement("p");
```
Añade contenido al elemento
```js
p.textContent = "Hola mundo";
```

**Insertar elementos en el DOM**

+ appendChild: Agrega el elemento al final del de otro
```js
document.body.appendChild(p);
```
+ append(): Más moderno, permite texto y varios elementos.
```js
container.append(p, " texto extra");
```
+ prepend(): Inserta el elemento al principio
```js
container.prepend(p);
```
+ insertBefore(): Inserta antes de otro elemento hijo
```js
parent.insertBefore(nuevo, referencia);
```

**Eliminar elementos del DOM**

+ remove(): Elimina directamente un elemento
```js
p.remove();
```
+ removeChild(): Elimina un hijo desde el padre
```js
parent.removeChild(p);
```

**Remplazar elementos**

+ replaceChild(): parent.replaceChild(nuevoElemento, elementoViejo);

### FORMULARIOS

**Obtener valores de un formulario**

+ input.value: Permite acceder al valor que escribe el usuario
```js
const input = document.querySelector("#nombre");
console.log(input.value); //Mostraría por consola el valor
```
Esto funciona también con textarea y select

**Validaciones básicas**

Comprobar si está vacio
```js
if(input.value === "") {
    console.log("Campo vacío");
}
```

Longitud mínima
```js
if(input.value.length < 3) {
    console.log("Muy corto");
}
```

**Mostrar errores en el DOM**

Crear un mensaje de error
```js
const error = document.createElement("p");
error.textContent = "El campo es obligatorio";
error.style.color = "red";
```

Insertarlo en la página
```js
form.appendChild(error);
```

Evitar errores duplicados
```js
const errorExistente = document.querySelector(".error");
if (!errorExistente) {
  error.classList.add("error");
  form.appendChild(error);
}
```

### EJERCICIOS CODEWARS

**Invertir un String**

```js
function solution(str){
  let word = str.split(''); //Con split dividimos un string en chars y lo añadimos al array word
  let drow = []; //Inicializamos el array donde irá la palabra invertida
        for (j = word.length - 1; j >= 0; j--) { //Hacemos un for al revés
                drow.push(word[j]); //Vamos añadiendo al array drown letra por letra
        }

        let stringFinal = drow.join(""); //Convertimos el array en String de nuevo
        return stringFinal; //Retornamos el String
 }

console.log(solution("hello")); //Ejecutamos la función y la mostramos por consola
```

**Enamorados**

Si el una flor tiene un número de petalos par y la otra impar, es true, sino false.

```js
function lovefunc(flower1, flower2){
  // moment of truth
  if(flower1 % 2 == 0 && flower2 % 2 != 0) {
    return true
  } else if(flower2 % 2 == 0 && flower1 % 2 != 0){
    return true
  } else {
    return false
  }
}
```

**Encontar aguja en un array**

Encuentra "needle" en el array haystack

```js
function findNeedle(haystack) {
  // your code here
  if(haystack.includes("needle")) {
    let result = "found the needle at position " + haystack.indexOf("needle");
    return result 
  }
}

//opcion 2

function findNeedle(haystack) {
    return "found the needle at position " + haystack.indexOf("needle");
}
```

**Alquiler de coche**

Crea una function que si alquilas el coche por 3 dias o más te reducen en 20$ el precio total.
Si lo alquilas por 7 días o más, te reducen en 50$ el total.
El precio de coche/dia es 40$.

```js
function rentalCarCost(d) {
  // Your solution here
  let priceDay = 40;
  let totalPrice; 
  if(d >= 7) {
    totalPrice = ((priceDay * d) - 50);
    return totalPrice
  } else if(d >=3 && d < 7) {
    totalPrice = ((priceDay * d) - 20);
    return totalPrice
  } else {
    totalPrice = priceDay * d;
    return totalPrice
  }
}
```

**Función calculadora**

Debes hacer una función que pasandole el tipo de operación y dos valores, devuelva el resultado. 

```js
function basicOp(operation, value1, value2){
  //Code
  switch(operation) {
    
    case "+":
          return value1 + value2
    break;
    case "-":
          return value1 - value2
    break;
    case "*":
          return value1 * value2
    break
    case "/":
          return value1 / value2
    break
    default:
          return 0;
  }
}

// Método alternativo
function basicOp(operation, value1, value2)
{
  return eval(value1 + operation + value2);
}
```

**Si tu nombre empieza por R...**

Función a la que le pasas un nombre por parámetro y si empieza por R, ese
nombre esta tocando el banjo.

```js
function areYouPlayingBanjo(name) {
  // Implement me
 
let letters = name.split('');
  if(letters[0] == "R" || letters[0] == "r") {
    return name + " plays banjo"
  } else {
    return name + " does not play banjo"
  }
  
  return name;
}

/* NOTA PARA MI. En js los strings son iterables
 * no necesitas dividir el string con split() el string en si
 * ya es un array de chars...
 * por lo tanto esto se puede hacer con name[0] == "r"  
 */
```

## AJAX
AJAX son las siglas de Asynchronous JavaScript and XML.  Es una técnica de
desarrollo web que permite a las páginas comunicarse de forma asíncrona con el
servidor sin necesidad de recargar la página, normalmente usando JavaScript y
formatos como JSON.

Para implementar esta técnica en el cliente se utilizan principalmente dos
Client-Side APIs del navegador: XMLHttpRequest y fetch.

XMLHttpRequest es una API más antigua y más verbosa, aunque todavía compatible.
Fetch es una API más moderna, basada en promesas y más sencilla de usar.

### FETCH

**¿Qué es?**

+ Es una Client-Side API del navegador que nos sirve para implementar AJAX
+ Esta basada en promesas
+ No bloquea la ejecución

**Como funciona**

Imaginemos que queremos que al apretar un botón se nos cargue un archivo local
en formato texto.

```html
<body>
    <button id="boton"></button>
    <div id="container"></div>
</body>
```

```js
let btn = document.getElementById("boton");
let contenedor = document.getElementById("container");

btn.addEventListener("click", mostrarTexto);

function mostrarTexto() {
    fetch("texto.txt")
    .then(data => data.text())
    .then(data2 => {
        contenedor.innerHTML = data2;        
    })
    .catch(error => {
        console.log("ERROR: " + error);
    })
    .finally( () => {
        console.log("Programa finalizado");
    });
}
```

Si queremos llamar a un recurso del servidor es exactamente lo mismo pero señalando al endpoint
```js
fetch("/api/users");
```

Si queremos hacerlo con un servidor externo igual
```js
fetch("https://webejemplo.com/users");
```

Al final siempre es:
´´´js
pidoUnRecurso("recurso")
.entonces(datosRecurso => recurso.convierteTexto()
.entonces(datosRecurso2 => {
    //haz esto con el recurso
}
.capturaError(error => {
    //Ejecuta esto
}
.finalmente( () => {
    //Ejecuta esto siempre
}

´´´js

**Métodos HTTP**

Bien, fetch por defecto hace un GET, si queremos hacer otro método HTTP debemos
especificarlo.

Por ejemplo por POST:

´´´js
fetch("/api/users", {
  method: "POST",
  body: JSON.stringify({ nombre: "Ana" }),
  headers: { "Content-Type": "application/json" }
});
´´´

RECORDATORIO MÉTODOS HTTP:
+ GET -> Leer datos
+ POST -> Enviar datos
+ PUT/PATCH -> Actualizar datos
+ DELETE -> Borrar datos

**Cabeceras (headers)**

´´´js
fetch("/api", {
  headers: { "Authorization": "Bearer token123" }
});
´´´

**Body**

´´´js
body: JSON.stringify({ name: "Juan" })
´´´

**Conversiones**

Fetch no devuelve los datos en si, devuelve un objeto response. 
Hemos de converiir dicho objeto en el formato que queremos.

+ response.text() -> Texto plano
+ response.json() -> json
+ response.blob() -> archivos binarios (imágenes, PDFs)
+ response.arrayBuffer() -> Datos binarios sin procesar

Cada uno devuelve otra promesa, por eso usamos .then()


