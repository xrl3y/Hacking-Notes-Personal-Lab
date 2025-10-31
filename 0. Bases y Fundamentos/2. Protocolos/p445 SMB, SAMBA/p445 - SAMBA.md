
---

Samba es un conjunto de software libre que implementa el protocolo de comunicación SMB (Server Message Block), también conocido como CIFS, para permitir a sistemas operativos tipo Unix (como Linux y macOS) compartir archivos e impresoras con sistemas Windows. Es decir, actúa como un puente para que distintos sistemas operativos interactúen y compartan recursos en una red, como si todos fueran parte de una red Windows.

- Podemos enumerar usuarios con *rpcclient* en este servicio de la siguiente manera:

```bash
rpcclient -U "" -N 192.168.20.1 # Entramos con un usuario vacio
	srvinfo                     # Dentro de la consola rpcclient este comando lista infrormacion 
	querydispinfo               # Informacion de usuarios
	enumdomusers                # Forma alternativa de enumerar usuarios
```

*Con la enumeración de usuarios ya podríamos explotar el protocolo 445 mediante el uso de hydra o de metaesploit como se ve en [[p445 - SMB - Server Message Block]]*

- Reconocimiento de vulnerabilidades tipicas como smb o samba con *enum4linux*

```bash
enum4linux -a <IP> 
```


