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
const

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

**Eliminar elemento mediante su posición**
```js
lista_frutas.splice(pos,0); //Borraría Manzana
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

Existen los asginadores de resta, multiplicación y división y otros muchos más
mucho menos frecuentes.

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
|OR (||)                    |Se debe cumplir o una u otra condición       |expr1 || expr2           |
|NOT (!)                    |Se debe cumplir lo opuesto                   |!expr1                   |

### OPERADORES DE CADENA
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

### CONVERSION DE TIPOS
**Convertir String a Number**
```js
let palabra = "Armario";
let numero = "123";

Number(palabra); //Esto se convienrte en NaN
Number(numero); //Esto se convierte en 123
```

### TRATAMIENTO STRINGS
**Eliminar espacios**
```js
let ejemplo = "ejemplo ";
console.log(ejemplo.trim()); //Devuelve la palabra sin espacio al final.
```


