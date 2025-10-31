
---

Wireshark es un analizador de paquetes de red gratuito y de código abierto que captura y muestra el tráfico de red para su análisis, diagnóstico y resolución de problemas. Permite a los usuarios ver los detalles de los paquetes, como los encabezados y el contenido, descomponer el tráfico de la red y utilizar filtros para encontrar información específica. Es una herramienta utilizada por profesionales para el desarrollo de software, auditorías de seguridad y la enseñanza.

- El comando para iniciarlo en segundo plano es:

```bash
wireshark &> /dev/null & disown
```

Podemos registrar trafico en texto  claro de protocolos inseguros como lo son el [[p21 - FTP (File Transfer Protocol)]] o el *http del puerto 80* , un ejemplo de esto es el siguiente:

![[Pasted image 20251020231415.png]]


