## REFERENCIAS WEB
---
https://victorhck.gitbook.io/aprende-vim

## MODOS
---

### MODO COMANDO
---
esc

### MODO VISUAL
---
esc + v

### MODO INSERTAR
---
esc + i

## MOVIMIENTOS Y ACCIONES BÁSICAS
---
**MOVIMIENTOS**
h    Izquierda
j    Abajo
k    Arriba
l    Derecha
w    Mover el cursor hacia adelante al principio de la palabra siguiente
}    Saltar al siguiente párrafo
$    Ir al final de la línea

**ACCIONES**
y    Copiar un texto (*yank* en Vim sería la acción de copiar, de ahí la letra `y`)
d    Eliminar un texto y guardarlo en el registro (*delete* en Vim sería la acción de eliminar, de ahí la letra `d`)
c    Eliminar un texto, guardarlo en el registro y comenzar en el modo de insertar

### DIVIDIR UNA VENTANA
---
**horizontalmente**
:split

**verticalmente**
:vsplit

**desplazamiento por ventanas**
cntrl + W + arrows

### BUSCAR UN ARCHIVO
---
:find nombre_archivo

### AÑADIR RUTA AL PATH
---
**Esto se hace para que find pueda buscar en esta ruta**
set path+=/ruta/a/tal

## BUSCAR COINCIDENCIA TEXTO
---
:vim /patron/ archivo

**Una vez encontrado la coincidencia, podremos navegar hacia la siguiente con la ventana quickfix:**
:copen

## NETRW (EXPLORADOR DE ARCHIVOS)
---
**NETRW es el explorador de archivos de VIM.**

:edit /path/to/directory

vim ~/Documents/

**Comandos dentro de NETRW**
%    Crear un nuevo archivo
d    Crear un nuevo directorio
R    Renombra un archivo o directorio
D    Elimina un archivo o directorio

### FORMATEAR TEXTO SELECCIONADO
gq

