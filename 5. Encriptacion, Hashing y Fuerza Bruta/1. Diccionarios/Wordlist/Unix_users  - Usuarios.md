
---

# ¿Qué es `unix_users`?

`unix_users` es una _wordlist_ de **nombres de usuario típicos en sistemas Unix/Linux** (nombres de cuentas de sistema, cuentas comunes como `root`, `daemon`, `www-data`, `vagrant`, `ubuntu`, etc.). Se distribuye con proyectos de seguridad como Metasploit y aparece en colecciones de wordlists usadas en pentesting y CTFs. [cocalc.com+1](https://cocalc.com/github/rapid7/metasploit-framework/blob/master/data/wordlists/unix_users.txt?utm_source=chatgpt.com)

# Dónde la encuentras (rutas típicas)

### Mejor ruta 

```bash
/usr/share/wordlist/metaesploit/unix_users.txt
```


---

- Metasploit: `.../data/wordlists/unix_users.txt` (el repositorio/paquete incluye este archivo). [cocalc.com](https://cocalc.com/github/rapid7/metasploit-framework/blob/master/data/wordlists/unix_users.txt?utm_source=chatgpt.com)
    
- En kits/paquetes de wordlists y repositorios como **SecLists**, que agrupan listas de usuarios y passwords útiles para pruebas. Si instalas `seclists` en Kali/apt queda disponible en `/usr/share/seclists/...`. [GitHub+1](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com)
    

# ¿Para qué sirve? (casos de uso)

- **Enumeración/Brute-force de usuarios**: cuando un servicio permite probar usuarios (p. ej. SMTP, SSH, FTP, HTTP forms) se usan listas como `unix_users` para probar nombres válidos antes de intentar contraseñas.
    
- **Reconocimiento en CTFs** y pruebas rápidas: acelera hallar cuentas por defecto o comunes.