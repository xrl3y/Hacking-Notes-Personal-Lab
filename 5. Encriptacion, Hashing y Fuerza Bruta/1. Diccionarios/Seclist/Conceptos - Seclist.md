
---

## ¿Qué es SecLists?

SecLists es una colección mantenida en GitHub (por Daniel Miessler y la comunidad) que agrupa **listas para pruebas de seguridad**: usernames, passwords, rutas/URLs para descubrimiento, payloads de fuzzing, firmas para búsquedas de datos sensibles, web shells, etc. Es la “caja de herramientas” de wordlists que muchos pentesters usan como punto de partida. [GitHub+1](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com)

## Dónde conseguirlo / instalarlo

- Clonar el repo oficial (si quieres la última versión):
    

`git clone https://github.com/danielmiessler/SecLists.git`

- En muchas distros de pentesting (Kali, AUR, Snap) puedes instalarlo por paquete: `sudo apt install seclists` o desde AUR / snap. En Kali suele quedar en `/usr/share/seclists`. [Kali Linux+1](https://www.kali.org/tools/seclists/?utm_source=chatgpt.com)
    

## Estructura útil (carpetas comunes)

Dentro del repo verás carpetas como (resumen):

- `Usernames/` — listas de usuarios comunes y por idioma/patron.
    
- `Passwords/` — rockyou, top lists, filtraciones, combinaciones.
    
- `Discovery/Web-Content/` — wordlists para directory busting / content discovery (muy usada con ffuf/gobuster).
    
- `Fuzzing/` — payloads para fuzzing de parámetros.
    
- `Payloads/` y `Web-shells/` — ejemplos y cargas.
    
- `Misc/`, `Creds/`, `DNS/`, etc. (mucha organización por tipo de prueba). [GitHub+1](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com)
    

## Ejemplos prácticos de uso

1. **Directory busting con `ffuf` / `gobuster` (usar listas de `Discovery/Web-Content`)**
    

`ffuf -u https://example.com/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc 200`

(escoge `common.txt` o `big.txt` según tamaño y ruido). [InfoSec Write-ups](https://infosecwriteups.com/content-discovery-with-ffuf-5bc81d2d8db6?utm_source=chatgpt.com)

2. **Brute-force de usuarios con Hydra (usar `Usernames/`)**
    

`hydra -L /usr/share/seclists/Usernames/top-usernames.txt -P /usr/share/wordlists/rockyou.txt ssh://10.0.0.5`

(usa listas pequeñas para pruebas dirigidas; las grandes generan mucho ruido). [GitHub+1](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com)

3. **Fuzzing de parámetros**  
    Combina `Fuzzing/` y `Payloads/` según el vector (ej., headers, JSON, parámetros GET/POST) y la herramienta que uses (ffuf, wfuzz). [GitHub](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com)