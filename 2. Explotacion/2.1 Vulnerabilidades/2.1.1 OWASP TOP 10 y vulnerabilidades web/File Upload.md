
---

Esta es una vulnerabilidad que permite subir archivos maliciosos a un sitio web, para crear el archivo malicioso podemos hacerlo con [[1. MsfVenom]] o mediante la pagina web [Rev Shell](https://www.revshells.com/) en el siguiente apartado:

- Código malicioso que copiaremos del apartado de **PHP PentestMonkey**  y lo pegaremos a un archivo.php

- Si al momento de intentar subir el archivo hay restricciones de la extensión php podemos guardarlo con este otro tipo de extensiones que leen el mismo codigo:

	- *phar*
	- *phtml*
	- *ph5*

---
# Web Shell
### Subida de archivo php con control mediante url y comando CMD 

Aqui lo que permite realizar es crear un archivo php en cual en la subida podramos ejecutar comandos desde la url mediante el parametro cmd, algunos codigos de estos son los siguientes:

- Archivo Llamado *cmd.php*

![[Pasted image 20251019195326.png]]

- Archivo de cualquier nombre con extensión php:

![[Pasted image 20251019195356.png]]

- Posteriormente a esto podremos controlar los comandos mediante la url ingresando al destino de donde se guardo el archivo malicioso y con los parametros

```bash
?cmd=<Comando>
```

Un ejemplo seria:

![[Pasted image 20251019200220.png]]

Si queremos una reverse shell en la consola podemos ir a [[2. Reverse Shell]]
