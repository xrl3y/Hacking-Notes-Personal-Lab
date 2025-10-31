
---
¿Qué es **arp-scan**?

Es una herramienta de línea de comandos que envía peticiones **ARP** en una red local para descubrir rápidamente qué dispositivos responden. Devuelve IP, dirección MAC y, cuando es posible, el fabricante (vendor) de la tarjeta de red. Es muy eficaz en LANs Ethernet/Wi-Fi porque usa ARP (nivel 2), por eso detecta equipos incluso aunque estén detrás de firewalls a nivel IP.

- Escaneo de Hosts por ARP

```bash
arp-scan -I ens33 --localnet # Escaneara todos los hosts de la interfaz de red ens33
```

- Ignorar Duplicados de Ip

```bash
arp-scan -I ens33 --localnet --ignoredups
```
###### Las mascaras de red que comienzan con un numero por ejemplo *08:00:27:dd:46:de* son maquinas virtualizadas 







---

### Comandos más usados (ejemplos prácticos):

- Escaneo rápido de tu red local (auto-detecta subred):
    

`sudo arp-scan --localnet`

- Escanear una subred específica usando una interfaz concreta:
    

`sudo arp-scan --interface=eth0 192.168.1.0/24`

- Guardar resultado en un archivo para revisar después:
    

`sudo arp-scan --localnet | tee arp-hosts.txt`

- Escanear una lista de rangos (desde un fichero):
    

`sudo arp-scan --interface=eth0 -f rangos.txt`

(donde `rangos.txt` contiene líneas con subredes o IPs)

Notas útiles:

- **Requiere permisos de root** (por eso `sudo`) porque envía paquetes a bajo nivel.
    
- Es ideal para descubrir dispositivos en una LAN (impresoras, cámaras, móviles, PCs, routers).