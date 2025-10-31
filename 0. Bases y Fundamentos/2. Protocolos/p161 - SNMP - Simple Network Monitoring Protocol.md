
---
El Protocolo Simple de Administración de Red (SNMP) es un protocolo de internet para la monitorización y gestión de dispositivos de red como routers, switches y servidores. Permite a un sistema de administración centralizado (el administrador SNMP) recopilar información y realizar cambios en dispositivos remotos (agentes SNMP). Funciona mediante un sistema de consultas y respuestas, usando un modelo de "agente" en cada dispositivo y un "administrador" centralizado que, a través de una [Base de Información de Gestión](https://www.google.com/search?sca_esv=ee8d36becf613b15&sxsrf=AE3TifMBS5d1PnVY61JR3f7hXiCdnIqEuQ%3A1761078803882&q=Base+de+Informaci%C3%B3n+de+Gesti%C3%B3n&sa=X&ved=2ahUKEwjHopvkkbaQAxWeoLAFHdEOChcQxccNegQIQRAB&mstk=AUtExfBzZeFHeW7tiRLQAGPsCe-wQ5R5YY1mQLfXZxRye2I4YVvttshBex6MzKyAzf648uSZ2Rt6pXVA0DpSwLA3z49N5bHUqWrP_HyxxWvTEUlK4UFNOtGk0oguyDNkQGNzi2WrtI2PV9XF2Ibq06FYBCIvBXcDPht_NqsBSZD-CmQ3w5U&csui=3) (MIB), puede supervisar el rendimiento, detectar problemas y planificar el crecimiento de la red

*Este protocolo corre por UDP, para poder enumerarlo usaríamos [[Nmap]] con la enumeración de protocolos por UDP*

- Enumeración de información del protocolo 

```bash
onesixtyone -c /usr/share/wordlist/rockyou.txt <Ipvictima>  # Fuerza bruta para obtener la clave de comunidad
```

- La contraseña debe salir algo como 

![[Pasted image 20251021153929.png]]

- Enumeración del sistema de administración con la clave ya obtenida 

```bash
snmpwalk -v 2c -c <Clave> <Ipvictima>  # Esto te puede dar informacion de usuarios, dominios o contraseñas 

# Si son dominios recordar acceder y editar el /etc/hosts 
```
