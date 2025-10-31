
---
# Movimiento en Consola

```powershell
cd                # Muestra la ruta actual o cambia de directorio
cd ..             # Sube un nivel en el árbol de directorios
dir               # Lista los archivos y carpetas del directorio actual
mkdir             # Crea un nuevo directorio
rmdir             # Elimina un directorio vacío
del               # Elimina uno o varios archivos
copy              # Copia archivos de un lugar a otro
move              # Mueve o renombra archivos o carpetas
type              # Muestra el contenido de un archivo de texto
cls               # Limpia la pantalla de la consola
echo              # Muestra un texto o variable por pantalla
whoami            # Muestra el nombre del usuario actual
hostname          # Muestra el nombre del equipo
tree              # Muestra la estructura de directorios
attrib            # Muestra o cambia los atributos de un archivo (oculto, solo lectura, etc.)
systeminfo        # Muestra información detallada del sistema
tasklist          # Muestra los procesos en ejecución
taskkill /PID #   # Finaliza un proceso según su ID (PID)
exit              # Cierra la ventana de la consola
help              # Muestra la lista de comandos disponibles
```

---
### Descarga de Archivos 

- Descarga de Archivos de un servidor con certutil 

```powershell
certutil -split -urlcache -f http://192.168.1.19/ejemplo.txt ejemplo.txt # Descarga el documento ejemplo y lo guarda como ejemplo
```

Ejecución Correcta Realizada 

![[Pasted image 20251017213620.png]]


---

### Enumeración de HotFixes en Windows

los HotFixes son parches de actualización que realiza windows a la hora de arreglar vulnerabilidades, una forma de enumerarlos es la siguiente:

*Sesion de Power Shell*

```powershell
Get-HotFix  # Muestra todos los HotFix
wmic qfe list brief /format:table   # Lista los hotfix tambien por si el anterior falla
(Get-HotFix).count # Contabiliza todos los HotFix

```

---

### Enumeración de usuarios 

```cmd
net users   # Muestra los usuarios que hay en el sistema

```