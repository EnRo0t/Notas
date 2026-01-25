# AUTENTICACIÓN VS AUTORIZACIÓN

## RECURSOS WEB
+ https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
+ https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html

## AUTENTICACIÓN

+ **AUTENTICACIÓN (AuthN)**: Es el proceso de verificación en
  el que un individuo, entidad o web es quien dice ser mediante
la validación de uno o más autenticadores (contraseñas,
fingerprints, o tokens de seguridad) que respaldan su
identidad. 
+ **IDENTIDAD DIGITAL**: Es la única representación de un
  sujeto en una transacción en línea. La identidad digital es
siempre única en el contexto de un servicio digital, pero no
necesariamente es trazable a un ser humano IRL. 
+ **PRUEBA DE IDENTIDAD**: Establece que el sujeto es realmente
  quien dice ser. Este concepto esta realcionado con el
concepto de KYC (know your costumer) que apunta a ligar una
identidad digital con una persona IRL. 
+ **ADMINISTRACIÓN DE SESIONES**: Es el proceso mediante el
  cual un servidor mantiene un estado sobre una entidad que
esta interactuando con él.  Esto es necesario para que el
servidor recuerde como reaccionar subsecuentemente a las
peticiones futuras. La sesión es mantenida en el servidor por
un identificador de sesión que puede ser trasmitido desde el
cliente al servidor y viceversa cuando estos interactuan. Las
sesiones deben ser unicas para cada usuario y
computacionalmente dificiles de predecir.

### DIRECTRICES GENERALES DE AUTENTICACIÓN

+ **USER IDs**: La función principal de un identificador de
  usuario es identificar de manera única a dicho usuario en el
sistema. Los identificadores de usuario deberían estar
generados de manera aleatoria para prevenir la creación
predecible o secuencial, de lo contrario podría ser un riesgo
para la seguridad.
+ **USERNAMES**: Los nombres de usuario son identificadores fáciles de recordar y escogidos por los propios usuarios para identificarse en el momento del acceso a un sistema o servicio. Los terminos user id y username pueden ser intercambiables si el username escogido por el usuario sirve como identificador único en el sistema. 
A los usuarios se les debe permitir utilizar su dirección de correo como username. Adicionalmente, ellos deben tener la opción de escoger otro username aparte de la dirección de correo electronico.
+ **SOLUCIÓN DE AUTENTICACIÓN Y CUENTAS SENSIBLES**:
    + No permitir el inicio de sesión con cuentas sensibles (es
      decir, cuentas que se utilicen internamente para acceder
a un backend, middleware o base de datos) desde ninguna
interfaz de frontend.
    + No utilizar la misma solución de autenticación (por
      ejemplo, IDP o Active Directory) que se usa internamente
para accesos no seguros (por ejemplo, acceso público o en la
DMZ).
+ **IMPLEMENTACIÓN DE CONTRASEÑAS FUERTES**: Un tema clave es
  el de utilizar contraseñas fuertes. Lo que significa "fuerte"
depende de varios factores:
    + Longitud de la contraseña
        + La longitud miníma debe ser establecida por la
          aplicación.
            + Si MFA (multiple factor autentication) esta
              activado, contraseñas más coras de 8 carácteres
serán consideradas debiles.
            + Si MFA no esta activado, las contraseñas deberán
              ser de más de 15 carácteres. 

        + La longitud máxima debería ser de 64 carácteres. 
    + No debería de haber límite sobre los carácteres que se
      pueden utilizar, es decir, se deberían de poder utilizar
todo tipo de carácteres, especiales, espacios en blanco, etc.
    + Hay que asegurar el cambio de credenciales cuando ocurra
      algun tipo de intrusión o cuando cambie el sistema de
autenticación. Hay que evitar el cambio de credenciales de
manera periodica, esto es un error común y malinterpretado, lo
que hay que conseguir es que los usuarios utilicen contraseñas
fuertes. Cambiar de manera peridica puede hacer que los
usuarios se acostumbren a utilizar credenciales debiles y
faciles de recordar.
+ Incluir un medidor de fortaleza de contraseñas para que el
  usuario, pueda ver, de manera visual, la fuerza de su
contraseña.
    + La libreria zxcvbn-ts puede ser utilizada para dicho
      proposito.
+ Bloquear contraseñas tipicas o contraseñas que se encuentren
  en diccionarios de fuerza bruta conocidos (rockyou,
seclist...)
+ **IMPEMENTAR UN RECUPERADOR DE CONTRASEÑAS SEGURO**
+ **GUARDAR CONTRASEÑAS CON UN ALGORITMO SEGURO**
+ **COMPARAR HASHES DE CONTRASEÑA CON FUNCIONES SEGURAS**:
  Cuando sea posible, la contraseña aportada por el usuario
debería de ser comparada con el hash almacenado utilizando una
funcuón de comparación que proporcione el lenguaje o framework
con el que se trabaja, como por ejemplo password_verify() de
PHP. Cuando no sea posible, la función de comparación
personalizada debería: 
    + Tener un máximo de longitud de input, para evitar ataques
      DDoS.
    + Explicitar los tipos de ambas variables, para protegerse
      contra ataques de type confusión como los magic hashes en
PHP. 
    + Retornar en tiempo contante, para evitar ataques de
      timing.
+ **OPCIÓN DE CAMBIO DE CONTRASEÑA**: Cuando se desarrolla una
  opción de cambio de contraseña se ha de tener en cuenta lo
siguiente: 
    + Que el usuario este autenticado con una sesión activa.
    + Verificación de la contraseña actual. Esto es para
      asegurar que es el usuario "real" el que esta tratando de
cambiar la contraseña. Considera el siguiente caso de abuso: Un
usuario inicia sesión en un ordenador público y olvida
desloguearse. Otra persona podría utilizar esa sesión activa.
Si no verificamos la contraseña actual, cualquier usuario con
la sesión activa de otro podría cambiarle la contraseña. 

**TRASMITIR CONTRASEÑAS SOLO SOBRE PROTOCOLOS SEGUROS**: La
página de inicio de sesión y todas las páginas posteriores que
requieran autenticación deben ser accesibles exclusivamente a
través de TLS u otro transporte seguro.

No utilizar TLS u otro transporte seguro en la página de inicio
de sesión permite que un atacante modifique la acción del
formulario de inicio de sesión, provocando que las credenciales
del usuario se envíen a una ubicación arbitraria.

No utilizar TLS u otro transporte seguro en las páginas
autenticadas después del inicio de sesión permite que un
atacante vea el ID de sesión sin cifrar y comprometa la sesión
autenticada del usuario.

+ **REQUERIR REAUTENTICACIÓN PARA OPCIONES SENSIBLES**:
Para mitigar ataques CSRF y el sessions hijacking, es
importante requerir las credenciales actuales de la cuenta
antes de actualizar información sensible, como la contraseña o
el correo electrónico del usuario, o antes de realizar
transacciones sensibles, como enviar una compra a una nueva
dirección.

Sin esta medida de protección, un atacante podría ejecutar
transacciones sensibles mediante un ataque CSRF o XSS sin
necesidad de conocer las credenciales actuales del usuario.

Además, un atacante podría obtener acceso físico temporal al
navegador del usuario o robar su ID de sesión para tomar el
control de la sesión autenticada del usuario.

+ **REAUTENTICACIÓN DESPUES DE EVENTOS DE RIESGO**:

