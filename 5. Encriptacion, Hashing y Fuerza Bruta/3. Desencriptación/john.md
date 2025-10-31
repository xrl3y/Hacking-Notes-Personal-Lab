
---

**John the Ripper** (a menudo sólo _John_) es un popular _cracker_ de contraseñas de línea de comandos: prueba palabras/reglas e intenta recuperar contraseñas a partir de hashes. Se usa en auditorías de seguridad y recuperación de contraseñas — siempre en sistemas donde tengas permiso.

- Comando usado para romper hash con un diccionario de palabras

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt 
```

- Romper archivos .zip con contraseña

```bash
zip2john <archivo.zip> > hash # Extraer primero el hash del .zip
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

- Romper Archivos de Bases de datos de KeePass

```bash
keepass2john <database.kdbx> > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

- Para identificar un hash podemos ir a [[Codificacion y Estructura de los Hashes]] o instalar la herramienta hash-identifier y usarla de la siguiente manera:

```bash
apt install hash-identifier
hash-identifier # Se abre una consola interactiva donde podemos pasarle el hash para saber el formato
john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt hash # Crackear formato md5 , Raw-SHA1,  Raw-SHA256 , Raw-SHA512
```

---

- Romper hash de clave privada de un archivo *id_rsa*

```bash
ssh2john id_rsa > hash  # Extraemos el hash del passphrase del id_rsa
john --wordlist=/usr/share/wordlist/rockyou.txt hash # Crakeamos el hash
```

---
- Romper hash con un diccionario dado 

```bash
john --wordlist=/home/xrl3y/TryHackMe/Easy-Peasy/content/easypeasy.txt --format=gost hash
```

---
 
### Opciones / comandos más usados 


- `john -h` → Muestra la ayuda y opciones rápidas.
    
- `john <archivo_hashes>` → Ejecuta John sobre un archivo de hashes (detecta formato si puede).
    
- `john --wordlist=<ruta>` (o `--wordlist:<ruta>`) → Ataque por diccionario usando la wordlist indicada. Ejemplo: `john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt`.
    
- `john --rules` → Aplica reglas de mutación a la wordlist (mejora efectividad). Se usa junto a `--wordlist`.
    
- `john --format=<FORMATO>` → Fuerza el formato de hash (p. ej. `nt`, `raw-md5`, `sha512crypt`, `ikev2`). Ejemplo: `john --format=sha512crypt hashes.txt`.
    
- `john --incremental` → Modo incremental (fuerza bruta dirigido por estadísticas).
    
- `john --fork=<N>` → Paraleliza el cracking en N procesos (útil en CPUs multinúcleo). Ejemplo: `john --wordlist=words.txt --fork=4 hashes.txt`.
    
- `john --session=<nombre>` → Inicia/nombrar una sesión para poder luego restaurarla.
    
- `john --restore=<nombre>` → Restaura una sesión previamente guardada.
    
- `john --status[=<nombre>]` → Muestra el estado/progreso de la sesión activa (opcionalmente por nombre).
    
- `john --show <archivo_hashes>` → Muestra las contraseñas ya crackeadas (usa el archivo `.pot` por defecto).
    
- `john --pot=<archivo.pot>` → Especifica un archivo `.pot` alternativo para almacenar/leer pares hash/contraseña.
    
- `john --list=formats` → Lista los formatos de hash soportados por la instalación actual.
    
- `unshadow /etc/passwd /etc/shadow > mypasswd` → (preparación en Unix) Combina passwd+shadow para crear un archivo aceptable por John.
    
- `john --make-charset=<archivo_charset> <archivo>` → Crea un conjunto de caracteres personalizado (avanzado).
    
- `john --rules=<nombre_reglas>` → Usar un conjunto de reglas nombrado distinto al predeterminado (si existe).