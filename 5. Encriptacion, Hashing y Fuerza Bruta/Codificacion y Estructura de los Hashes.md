
---


### 🔒 Hashes más conocidos

| Nombre             | Longitud típica                       | Ejemplo                                       | Descripción                                               |
| ------------------ | ------------------------------------- | --------------------------------------------- | --------------------------------------------------------- |
| **MD5**            | 32 caracteres (128 bits)              | `5d41402abc4b2a76b9719d911017c592`            | Antiguo y rápido, pero **inseguro** por colisiones.       |
| **SHA-1**          | 40 caracteres (160 bits)              | `2fd4e1c67a2d28fced849ee1bb76e7391b93eb12`    | Mejor que MD5, pero **ya obsoleto** para seguridad.       |
| **SHA-256**        | 64 caracteres (256 bits)              | `9c56cc51b374c3b2f36e5f7a6a2e48a9e9e2b8b9...` | Estándar actual en seguridad y certificados.              |
| **SHA-512**        | 128 caracteres (512 bits)             | `1f40fc92da241694750979ee6cf582f2...`         | Más robusto que SHA-256; más lento.                       |
| **CRC32**          | 8 caracteres (32 bits)                | `1c291ca3`                                    | Checksum rápido para detectar errores, no para seguridad. |
| **NTLM (Windows)** | 32 caracteres                         | `32ed87bdb5fdc5e9cba88547376818d4`            | Hash de contraseñas en Windows; vulnerable.               |
| **bcrypt**         | 60 caracteres, formato `$2b$cost$...` | `$2b$12$eImiTXuWVxfM37uY4JANjQ==`             | Usa **sal y costo**, muy seguro para contraseñas.         |
| **scrypt**         | Variable                              | `$s0$e0801$...`                               | Más resistente a GPUs/ASICs que bcrypt.                   |
| **PBKDF2**         | Variable                              | `sha256:100000$abc$12345...`                  | Usa iteraciones + sal; muy usado en apps seguras.         |

---
### 🔠 Codificaciones y representaciones comunes

| Nombre                | Longitud típica           | Ejemplo                                                  | Descripción                                                                                           |
| --------------------- | ------------------------- | -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Base64**            | Variable (múltiplo de 4)  | `SGVsbG8gV29ybGQh` → “Hello World!”                      | Convierte datos binarios a texto ASCII. Muy usada en correos, JSON, JWT, etc. **Reversible.**         |
| **Hexadecimal (Hex)** | Doble del tamaño original | `48656c6c6f` → “Hello”                                   | Representa bytes en formato base 16 (0–9, A–F). Muy usada en hashes y claves.                         |
| **Binario (Base 2)**  | 8 bits por carácter       | `01001000 01100101 01101100 01101100 01101111` → “Hello” | Representa cada byte como 8 bits. Base fundamental de todos los datos digitales.                      |
| **Decimal (Base 10)** | Variable                  | `72 101 108 108 111` → “Hello”                           | Representa cada carácter como su valor ASCII decimal. Usada para depuración o protocolos simples.     |
| **Octal (Base 8)**    | Variable                  | `110 145 154 154 157` → “Hello”                          | Representación en base 8, usada en sistemas Unix y permisos de archivos (ej. `chmod 755`).            |
| **URL Encoding**      | Variable                  | `Hello%20World%21`                                       | Sustituye caracteres especiales por `%` + código Hex. Usada en HTTP y navegadores. [[URL Encode]]     |
| **HTML Encoding**     | Variable                  | `Hello&nbsp;World!` o `&#72;&#101;&#108;`                | Escapa caracteres para que no se interpreten como HTML.                                               |
| **ASCII / UTF-8**     | Variable                  | `Hello World!`                                           | Codificación estándar de texto. UTF-8 es compatible con ASCII y soporta todos los caracteres Unicode. |
| **Base32**            | Variable                  | `JBSWY3DPEBLW64TMMQ======` → “Hello”                     | Codifica en base 32 (A–Z, 2–7). Menos densa que Base64, pero más legible.                             |
| **Base58**            | Variable                  | `JxF12TrwUP45BMd`                                        | Usada en criptomonedas (Bitcoin) para evitar caracteres ambiguos (0/O, l/I).                          |
| **Morse**             | Variable                  | `.... . .-.. .-.. ---`                                   | Representación antigua basada en puntos y rayas, usada en telecomunicaciones.                         |
