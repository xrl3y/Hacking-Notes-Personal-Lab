
---

SSH (Secure Shell) es un protocolo seguro para acceso remoto a máquinas y ejecución de comandos sobre una red cifrada. Se usa para administración remota, túneles seguros, transferencia de archivos y autenticación con claves públicas —más seguro que usar contraseñas—. Usa criptografía para proteger la confidencialidad e integridad de la sesión.

Te puede conectar a ssh mediante el dominio o la ip a la que quieras acceder:

-  Dominio
```bash
ssh lucas@machine.htb
```

-  IP
```bash
ssh lucas@10.10.11.88
```

---
### Vulnerabilidades mas comunes 

#### Hydra

- Generalmente es susceptible a ataques de fuerza bruta empleando [[Hydra]]  

---
### Comandos más usados 

- `ssh usuario@host` — Conectar al servidor.  
    Ej.: `ssh juan@192.168.1.50`
    
- `ssh -p <puerto> usuario@host` — Conectar especificando otro puerto.  
    Ej.: `ssh -p 2222 admin@ejemplo.com`
    
- `ssh -i /ruta/clave.pem usuario@host` — Usar una clave privada concreta.  
    Ej.: `ssh -i ~/.ssh/id_ed25519 ec2-user@52.1.2.3`
    
- `ssh usuario@host 'comando'` — Ejecutar un comando remoto y salir.  
    Ej.: `ssh juan@servidor.com 'ls -la /var/www'`
    
- `ssh -L <puerto_local>:<destino>:<puerto_remoto> usuario@host` — Túnel local (acceder a un servicio remoto como si fuera local).  
    Ej.: `ssh -L 8888:localhost:8080 juan@servidor.com`
    
- `scp archivo usuario@host:/ruta/destino` — Copiar archivo al servidor (sobre SSH).  
    Ej.: `scp backup.tar.gz juan@192.168.1.50:/home/juan/`
    
- `rsync -avz -e "ssh" ./carpeta/ usuario@host:/ruta/` — Sincronizar carpetas eficientemente (usa SSH).  
    Ej.: `rsync -avz -e "ssh -p 2222" ./mi_web/ admin@ejemplo.com:/var/www/`
    
- `ssh-keygen` y `ssh-copy-id` — Generar par de claves y copiar la pública al servidor (autenticación por clave).  
    Ej.: `ssh-keygen -t ed25519` → `ssh-copy-id -i ~/.ssh/id_ed25519.pub usuario@host`