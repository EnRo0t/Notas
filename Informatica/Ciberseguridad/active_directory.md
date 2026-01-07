# PENTESTING EN ACTIVE DIRECTORY

### REFERENCIAS WEB
+ https://www.youtube.com/watch?v=-bNb4hwgkCo&t=2981s

### LABORATORIO
+ Un DC (Domain Controller) con Windows 2016 Datacenter Eval Edition
+ Un usuario con Windows 10 Eval Edition
+ Todos en una misma red NAT

**Configurando el Domain Controller**
El DC será el servidor que funcionara como nodo central de nuestro directorio activo. 

![ad1](../../Imagenes/ad1.png)

Lo primero que vamos a hacer es cambiar el nombre del equipo para que sea más
sencillo identificarlo.  Esto por cierto no es una práctica aconsejable en un
entorno real. 
 
![ad2](../../Imagenes/ad2.png)

![ad3](../../Imagenes/ad3.png)

![ad4](../../Imagenes/ad4.png)

![ad5](../../Imagenes/ad5.png)

![ad6](../../Imagenes/ad6.png)

![ad7](../../Imagenes/ad7.png)

![ad8](../../Imagenes/ad8.png)

![ad9](../../Imagenes/ad9.png)

![ad10](../../Imagenes/ad10.png)

![ad11](../../Imagenes/ad11.png)

![ad12](../../Imagenes/ad12.png)

![ad13](../../Imagenes/ad13.png)

![ad14](../../Imagenes/ad14.png)

![ad15](../../Imagenes/ad15.png)

![ad16](../../Imagenes/ad16.png)

Desinstalamos el Windows Defender
![ad17](../../Imagenes/ad17.png)

![ad20](../../Imagenes/ad20.png)
Vamos a crear ahora el usuario a nível de directorio activo. 

![ad21](../../Imagenes/ad21.png)

**Configuración PC-User**

![ad18](../../Imagenes/ad18.png)
Tenemos que poner como servidor DNS la IP del DC.
 
![ad19](../../Imagenes/ad19.png)
Comprobamos como ahora tenemos conexión con el DC. 

![ad22](../../Imagenes/ad22.png)
Ahora vamos a añadir este pc al dominio. 

![ad23](../../Imagenes/ad23.png)

![ad24](../../Imagenes/ad24.png)

![ad25](../../Imagenes/ad25.png)

![ad26](../../Imagenes/ad26.png)
