# XML EXTERNAL ENTITY XXE

## RECURSOS WEB

https://portswigger.net/web-security/xxe

## ¿QUÉ ES XML?

XML son las siglas de Extensible Markup Language, lenguaje de marcado
extensible. Este lenguaje comprende etiquetas y datos, como HTML, pero a
diferencia de este, las etiquetas no están predefinidas y se pueden crear para
encapsular los datos que deseamos. 

XML tiene forma de árbol y se utiliza principalmente para almacenar y
transportar información y es fácilmente legible tanto para seres humanos como
para máquinas. 

El uso de XML ha ido en decadencia en favor del formato JSON, pero se sigue
utilizando y mucho. 

La estructura de XML sigue un patrón de padre/hijo, existiendo una etiqueta
raíz que engloba todas las demás:

```xml
<raiz>
	<tronco>
		<ramas>
			<hojas>Datos sobre las hojas</hojas>
		</ramas>
	</tronco>
</raiz>
```

También pueden tener atributos como los HTML. 

```xml
<etiqueta atributo="valor_atributo"></etiqueta>
```

## ¿QUÉ SON LAS ENTIDADES?

Las entidades XML son una manera de referenciar un dato sin utilizar el dato en
si. En pocas palabras, son algo así como las variables en programación. 

Ejemplo de entidad:

```xml
&lt; = <
&gt; = >
```

Es decir, cuando llamamos a la entidad lt, estamos llamando al dato “<”.

Estas son **entidades predefinidas**, entidades que ya existen dentro de la
lógica del lenguaje XML.

Existen algunas más como: 

```xml
&amp = &
&quot = "
&apos = '
```

Pero podemos definir nuevas entidades, las llamadas **Entidades custom**
mediante un DTD.

DTD son las siglas de Document Type Definition, y como dice el nombre, este es
un documento donde se definen los tipos de datos que se pueden utilizar en el
XML, así como sus entidades. Una forma de declarar un DTD y una entidad es la
siguiente:

```xml
<!DOCTYPE foo [ <!ENTITY myentity "my entity value" > ]>
```

Aquí creamos un DTD y establecemos que la entidad myentity tiene el valor “my
entity value”, de tal forma que si la llamáramos en un XML:

```xml
<etiqueta>&myentity</etiqueta> <!-- Esto -->

<etiqueta>my etity value</etiqueta> <!-- Es igual a esto -->
```

Pero todavía existen otro tipo de entidades y son estas últimas las que nos
interesan como atacantes, son las **entidades externas**. Estas son entidades
custom que referencian datos externos al DTD donde se declaran.

```xml
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>
```

Un ejemplo donde se declara una entidad externa desde el DTD que llamaría a una
URL.

**XXE TO LFI**

Un vector de ataque común es utilizar estas entidades externas para llamar a
archivos del sistema:

```xml
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
```
