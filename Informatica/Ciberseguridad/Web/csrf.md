# CSRF (CROSS-SITE REQUEST FORGERY)

## REFERENCIAS WEB
+ https://portswigger.net/web-security/csrf#what-is-csrf

## ¿QUÉ ES EL CSRF?
Es un ataque web en el que se induce a un usuario a realizar una acción sin su
consentimiento y de manera subrepticia.
Un atacante podría hacer que un usuario cambiara su dirección de correo
eléctronico o la contraseña de su cuenta en el sitio web, por ejemplo. 

## ¿CÓMO FUNCIONA?
Para que un CSRF pueda acontecer, se deben dar 3 condiciones:
+ Una acción relevante: Debe haber una acción que el atacante quiera realizar
  como otro usuario. Un cambio de contraseña, un cambio en los permisos del
usuario...
+ Manejo de sesiones basada en cookies: No debe existir otra manera de
  autenticar a un usuario en una sesión que no sea mediante cookies de sesión. 
+ Sin parámetros de solicitud impredecibles: Las solicitudes que realizan la
  acción no contienen ningún parámetro cuyos valores el atacante no pueda
determinar o adivinar. Por ejemplo, al hacer que un usuario cambie su
contraseña, la función no es vulnerable si un atacante necesita saber el valor
de la contraseña existente. 

Supongamos que la aplicación web tiene una función para cambiar la dirección de
correo electrónico de un usuario.  Cuando el usuario envia la solicitud esta
tiene un aspecto como el siguiente:
```bash
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```
Aquí se cumplen las 3 condiciones mencionadas anteriormente. 
+ Existe una acción relevante: Cambiar la dirección de correo electrónico. 
+ La aplicación utiliza una cookie de sesión para identificar quien ha emitido
  la solicitud. No existe otro método.
+ El atacante puede deducir los valores de los parámetros que debe introducir
  para cambiar la dirección de correo. 

Si se dan dichas condiciones, un atacante podría construir una web maliciosa con un falso formulario: 
```html
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
        </form>
        <script>
            document.forms[0].submit();
        </script>
    </body>
</html>
```
De tal modo que cuando el usuario ingrese en dicha página web, de manera
automática se cambiará la dirección de su correo electrónico por el del
atacante.

Básicamente lo que hace el html es enviar una solicitud por POST al enlace
donde se hace el cambio de correo electrónico de la web vulnerable con unos
valores ya predeterminados (el email del atacante).
 
