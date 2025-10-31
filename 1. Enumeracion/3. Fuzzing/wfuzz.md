
---

- Enumeracion de directorios
```bash
wfuzz -c --hc=404,403 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ/
wfuzz -c --hc=404,403 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ.html # archivos de la extension 
```

 - Enumeración de subdominios
 
```bash
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -H "Host: FUZZ.logan.hmv" -u 192.168.0.42
wfuzz -c --hc=404 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -H "Host: FUZZ.logan.hmv" -u 192.168.0.42

-c # colores
--hc # Ocultar codigos
--hl # Ocultar lineas
--hw # Ocultar palabras
```

###### Agregar subdominios y dominios al /etc/hosts para que resuelva