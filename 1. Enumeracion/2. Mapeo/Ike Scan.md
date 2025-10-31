
---

`ike-scan` es una herramienta de línea de comandos utilizada para **descubrir y enumerar gateways VPN (IPsec/IKE)**. Permite identificar hosts que usan IKE (Internet Key Exchange) y obtener información sobre sus configuraciones.

- Escaneo del dominio ip asociado a un dns

```bash
ike-scan -M expressway.htb
```

- Forzar retorno de hash para descifrar usuario y posible hash de contraseña devuelto 

```bash
sudo ike-scan -A -P -M 10.10.11.87
```

Los hashes que puede devolver estan en formato PSK y se pueden romper con herramientas similares al hasheo como pueden ser [[john]] o [[psk-crack]]


---
### **Comandos más usados:**

- `ike-scan <IP>` → Escanea una dirección IP en busca de IKE (fase 1).
    
- `ike-scan -A <IP>` → Intenta autenticarse e identifica configuraciones de VPN.
    
- `ike-scan -M <IP>` → Modo múltiple (muestra todos los posibles valores de cookies).
    
- `ike-scan -P <archivo>` → Guarda los paquetes de respuesta en un archivo.
    
- `ike-scan -v <IP>` → Muestra salida detallada (verbose).
    
- `ike-scan -n <veces>` → Repite el envío del paquete varias veces.
    
- `ike-scan -D` → Muestra la decodificación detallada del paquete IKE.