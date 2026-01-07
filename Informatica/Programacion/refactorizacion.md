# REFACTORIZACIÓN

## ¿QUÉ ES?
La refactorización consiste en mejorar la estructura y legibilidad del código
sin cambiar su comportamiento.

### TÉCNICAS

**Extracción de constantes**
Se utiliza cuando:
+ Un valor literal se repite
+ Cuando un número o string no explica su significado
+ Para evitar magic numbers / magic strings

Imagina este código sin refactorizar
```java
if (user.getAge() > 18) {
    System.out.println("Acceso permitido");
}
```
Extraemos la constante de tal modo que queda más claro de donde viene el número 18
```java
static final int EDAD_MINIMA = 18;

if (user.getAge() > EDAD_MINIMA) {
    System.out.println("Acceso permitido");
}
```

**Extracción de método**
Se utiliza cuando:
+ Un método hace demasiadas cosas
+ Código duplicado

Tenemos el siguiente método
```java
void procesarPedido(Pedido pedido) {
    double total = pedido.calcularTotal();
    double impuesto = total * 0.21;
    double totalFinal = total + impuesto;

    System.out.println("Total con impuestos: " + totalFinal);
}
```
Convertimos un mismo método en dos métodos separados. Mucho más claro y fácil de mantener.
```java
void procesarPedido(Pedido pedido) {
    double totalFinal = calcularTotalConImpuestos(pedido);
    System.out.println("Total con impuestos: " + totalFinal);
}

double calcularTotalConImpuestos(Pedido pedido) {
    double total = pedido.calcularTotal();
    double impuesto = total * 0.21;
    return total + impuesto;
}
```

**Extracción de variables**
Se utiliza cuando:
+ Expresiones largas y complejas
+ Mejorar legibilidad

Tenemos este código con un condicional con una expresión compleja
```java
if ((user.getAge() > 18) && user.isActive() && !user.isBlocked()) {
    permitirAcceso();
}
``` 

Conververtimos las expresiones complejas en un par de variables.
```java
boolean esMayorDeEdad = user.getAge() > 18;
boolean puedeAcceder = user.isActive() && !user.isBlocked();

if (esMayorDeEdad && puedeAcceder) {
    permitirAcceso();
}
```

**Renombrado de variables**
Se utiliza cuando:
+ El nombre no explica bien la intención
+ Hay abreviaturas, ambigüedad o contexto innecesario

Tenemos la siguiente variable. No tiene un contexto apropiado
```java
int d; //días desde creación
```
Le cambiamos el nombre para que este más claro
```java
int daysSinceCreation;
```

**Inline**
Es lo opuesto a la extracción.
Se utiliza cuando:
+ La variable no añade claridad
+ Solo se usa una vez

Tenemos una variable y un retorno
```java
double impuesto = total * 0.21;
return impuesto;
```
Eliminamos la variable y lo reducimos todo a un inline
```java
return total * 0.21;
```

**Guard clauses (cláusulas de guarda)**
Se utiliza cuando:
+ Hay muchos ifs anidados
+ Validaciones al inicio del método

Código sin refactorizar
```java
void procesar(User user) {
    if (user != null) {
        if (user.isActive()) {
            ejecutar();
        }
    }
}
```
Refactorizado
```java
void procesar(User user) {
    if (user == null) return;
    if (!user.isActive()) return;

    ejecutar();
}
```
Mejora mucho la legibilidad.


