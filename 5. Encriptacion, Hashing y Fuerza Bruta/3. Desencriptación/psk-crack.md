

---

`psk-crack` es una herramienta para **probar (forzar) claves precompartidas (PSK) de VPN IPsec/IKE** usando capturas o respuestas IKE. Se usa en auditorías de seguridad para evaluar la resistencia de los PSK frente a ataques por diccionario/ fuerza bruta. **Úsalo sólo en entornos autorizados** (tu red de pruebas o con permiso explícito).

- Comando usado para romper hash con un diccionario de palabras

```bash
psk-crack -d /usr/share/wordlists/rockyou.txt hash.txt
```

---

### Opciones / comandos más usados 

- `psk-crack -h` → Muestra la ayuda/ayuda rápida.
    
- `psk-crack -i <archivo_pcap>` → Usar una captura (pcap) que contenga el intercambio IKE o paquetes relevantes.
    
- `psk-crack -r <respuesta_ike.txt>` → Usar una respuesta IKE guardada por herramientas como `ike-scan`.
    
- `psk-crack -w <diccionario.txt>` → Archivo de palabras (wordlist) para ataques por diccionario.
    
- `psk-crack -t <N>` → Número de hilos / workers (paralelismo).
    
- `psk-crack -v` → Verbose / salida detallada.
    
- `psk-crack --hash-format <formato>` → Especificar formato de entrada si la herramienta lo soporta.
    
- `psk-crack -o <salida>` → Guardar resultados / credenciales encontradas.  
    (Nota: los nombres exactos de flags pueden variar entre implementaciones; consulta `-h`.)