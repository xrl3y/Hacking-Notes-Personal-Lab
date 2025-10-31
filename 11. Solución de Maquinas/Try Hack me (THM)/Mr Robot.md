
---

### Enumeración 

*Ip Victima: 10.201.43.196*

- Puertos Abiertos

```bash
PORT    STATE SERVICE REASON
22/tcp  open  ssh     syn-ack ttl 61
80/tcp  open  http    syn-ack ttl 61
443/tcp open  https   syn-ack ttl 61
```

- Enumeración de Scripts de Reconocimiento y Versiones 

```bash
❯ nmap -p22,80,443 -sCV 10.201.43.196 -oN Targeted
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-23 22:30 -05
Nmap scan report for 10.201.43.196
Host is up (0.25s latency).

PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 74:b8:3e:03:b0:6c:4a:9a:71:2e:dd:bc:7c:08:e3:5c (RSA)
|   256 33:b2:7a:65:72:31:29:4e:dd:8d:a4:9e:ac:16:f1:da (ECDSA)
|_  256 cb:ab:1f:1f:ce:a7:2c:1b:c4:9a:da:5d:b9:79:56:58 (ED25519)
80/tcp  open  http     Apache httpd
|_http-title: Site doesnt have a title (text/html).
|_http-server-header: Apache
443/tcp open  ssl/http Apache httpd
| ssl-cert: Subject: commonName=www.example.com
| Not valid before: 2015-09-16T10:45:03
|_Not valid after:  2025-09-13T10:45:03
|_http-title: Site doesnt have a title (text/html).
|_http-server-header: Apache
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


Accedimos al servicio web en el puerto 80 y realizamos fuzzing para identificar puntos de interés. Detectamos un formulario de acceso a WordPress y una sección «license» que requería credenciales; mediante ésta obtuvimos acceso inicial. En la instalación de WordPress alteramos la página 404 para incluir un payload malicioso: al solicitar recursos inexistentes bajo `wp-content` se ejecutaba la conexión inversa. Finalmente, cambiamos de usuario, localizamos binarios con permisos SUID y aprovechamos esos permisos para escalar privilegios hasta obtener root.

# Versión detallada y técnica (sin comandos)

1. Reconocimiento: exploración del puerto 80 y fuzzing de rutas para localizar aplicaciones y puntos de entrada.
    
2. Acceso inicial: descubrimiento de un login de WordPress y de un apartado «license» protegido por credenciales; uso de esa vía para acceder al panel correspondiente.
    
3. Persistencia/ejecución remota: modificación del manejo del error 404 en la instalación de WordPress para incorporar código malicioso de forma que la petición a recursos inexistentes en `wp-content` provocara la ejecución de una reverse shell.
    
4. Escalada de privilegios: cambio de contexto a otro usuario, búsqueda de binarios y ficheros con permisos SUID, y aprovechamiento de esos permisos para elevar privilegios a root.