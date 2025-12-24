# NOTAS LIBRO HACKING THE ART OF EXPLOTATION

## ASSEMBLY LANGUAGE

**CONFIGURANDO DEBBUGER GDB PARA SINTAXIS INTEL**
Los comandos mostrados en el libro estan desactualizados. 
```bash
gbd -q 
set dissasembly-flavor intel
quit
```
```bash
echo "set dissasembly-flavor intel" > ~/.gdbinit
```
