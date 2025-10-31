
---

SMTP (Protocolo Simple de Transferencia de Correo) es el protocolo estándar que permite enviar correos electrónicos a través de internet. Funciona como una serie de reglas que los servidores y clientes de correo electrónico utilizan para intercambiar mensajes, desde la conexión inicial hasta la entrega final en la bandeja de entrada del destinatario. Es importante notar que SMTP solo se encarga del envío; otros protocolos como POP3 o IMAP son necesarios para la recuperación del correo


#### Comandos comunes

```bash
telnet <Ip> <Puerto>
telnet 10.10.10.2 25    # Conexion al protocolo smtp
nc 10.10.10.2 25    # Conexion al protocolo smtp 
telnet smtp.ejemplo.com 25  
nc smtp.ejemplo.com 25  
```

```bash
HELO <hostname>           # Saludo simple: identifica el cliente (antiguo; usar EHLO si es posible)
EHLO <hostname>           # Saludo extendido: solicita y muestra las capacidades del servidor (STARTTLS, AUTH, SIZE...)
MAIL FROM:<address>       # Indica el remitente del mensaje (inicia la transacción)
RCPT TO:<address>         # Indica un destinatario (repetible para varios destinatarios)
DATA                      # Inicia el envío del cuerpo del mensaje; terminar con una línea que contenga solo un punto (.)
RSET                      # Reinicia la transacción actual (limpia MAIL/RCPT en curso)
NOOP                      # No hace nada; usado para mantener/comprobar la conexión
QUIT                      # Cierra la sesión ordenadamente
VRFY <user>               # Pide verificar si existe un usuario (a menudo deshabilitado por seguridad)
EXPN <mailing-list>       # Expande una lista de correo (suele estar deshabilitado por privacidad)
HELP [<command>]          # Solicita ayuda o lista de comandos soportados
STARTTLS                  # Solicita pasar a TLS (si el servidor lo soporta); después hay que iniciar TLS real
AUTH LOGIN                # Inicia autenticación método LOGIN (intercambio de usuario/clave en base64)
AUTH PLAIN <base64>       # Autenticación PLAIN en una sola línea (base64 de \0usuario\0contraseña); suele requerir TLS
AUTH CRAM-MD5             # Solicita autenticación CRAM-MD5 (challenge-response; más seguro que LOGIN/PLAIN)
SIZE <bytes>              # Indica el tamaño del mensaje que se enviará (negociable si el servidor lo soporta)
8BITMIME                  # Indica soporte para 8-bit MIME en el cuerpo del mensaje
PIPELINING                # Indica soporte para pipelining (permitir enviar varios comandos en fila)
BINARYMIME                # Indica soporte para transferencia de contenido binario (RFC)
BCC                       # (No es comando SMTP separado; se envía como dirección en RCPT TO sin ponerla en el encabezado visible)
TURN                      # Comando obsoleto (histórico, raramente soportado)
```