
---

**Netdiscover** es una herramienta ligera y muy práctica para **detectar dispositivos activos en una red local (LAN)**. Funciona escuchando y enviando solicitudes **ARP**, al igual que [[Arp-Scan]] , y muestra las **direcciones IP, direcciones MAC y fabricantes** de los dispositivos conectados. Es muy útil para identificar equipos en redes desconocidas o sin un servidor DHCP visible.

```bash
netdiscover -i eth0 -r 192.168.0.0/24 # Escaneo de toda la red mediante el CIDR y la red eth0
```



---
### 🔹 Comandos más usados:

- **Escanear la red local automáticamente (modo pasivo y activo):**
    
    `sudo netdiscover`
    
    Detecta automáticamente tu interfaz y red, mostrando todos los dispositivos conectados.
    
- **Especificar el rango de IP manualmente:**
    
    `sudo netdiscover -r 192.168.1.0/24`
    
    Escanea el rango indicado (en este caso, toda la subred 192.168.1.0/24).
    
- **Elegir la interfaz de red (Wi-Fi o cable):**
    
    `sudo netdiscover -i wlan0`
    
    Usa la interfaz **wlan0** (puedes cambiarla por **eth0**, **enp3s0**, etc., según tu sistema).
    
- **Modo pasivo (sin enviar paquetes, solo escuchando la red):**
    
    `sudo netdiscover -p`
    
    Muestra los dispositivos que comunican en la red sin generar tráfico adicional. Ideal para análisis discretos.
    
- **Guardar los resultados en un archivo:**
    
    `sudo netdiscover -r 192.168.1.0/24 > dispositivos.txt`
    
    Guarda el listado de dispositivos detectados en un archivo de texto.