
---
El Protocolo de Escritorio Remoto (RDP) es un protocolo de Microsoft que permite controlar un ordenador a distancia a través de una red segura y cifrada. Facilita la administración remota y el soporte técnico, y permite a los usuarios trabajar en sus equipos desde cualquier lugar, utilizando su teclado y ratón locales para interactuar con el escritorio remoto.

*Para acceder a este protocolo primero debemos tener con anterioridad credenciales de usuario y contraseña para el acceso*

- Acceso via rdp 

```bash
xfreerdp /u:<Usuario> /p:<Contraseña> /v:<Ipmaquinavitima>:<PuertoRDP>  # Ingresar remotamente a la maquina victima con una terminal grafica tambien
```

- Algunos comandos para el movimiento de consola los podemos encontrar en [[10. Comandos Comunes/Windows/Comandos Comunes|Comandos Comunes]] , algunos de ellos son los siguientes:

 ```cmd
 net user  # Listar usuarios 
 net user <Usuario> # Ver informacion del usuario
 net localgroup Administrators # Ver que usuarios se encuentran en el grupo de administradores
 ```

