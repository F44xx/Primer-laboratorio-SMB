Echamos a correr la maquina 
![](./imagen1.png)
Luego echamos un nmp para poder ver los puertos abiertos en la IP 192.168.1.118
![](./imagen2.png)

Notamos que esta abierto el puerto 445 que es para el protocolo SMB 

Al ver que el puerto SMB esta abierto vamos a hacer un escaneo con "smbmap" para notar si hay carpetas compartidas que podemos ver. 
![](./imagen3.png)
Al correr el comando "smbmap -H (IP)" quisimos ver las carpetas compartidas pero notamos que no tenemos acceso. 
Esto no termina acá, aplicaremos fuerza bruta contra este protocolo con Hydra para ver si hay un usuario valido. 
``` bash 
 hydra -l admin_backup -P /usr/share/wordlists/rockyou.txt smb://192.168.1.118 
``` 

-l : sirve para poder indicar un usuario valido, en este caso sabemos que el usuario valido es admin_backup 
-P : sirve para indicar una ruta de diccionario, en este caso el rockyou 
smb: aclaramos el protocolo y la IP de la maquina 

Aquí haremos algo diferente, no podía correr el Hydra Rockyou, para verificar entonces use "enum4linux" para encontrar los usuarios. 
![](./imagen4.png)
Como vemos si aparece el usuario admin, probaremos solo poniendo ese usuario con Hydra 

Luego de muchos intentos el problema si era el usuario, era solo admin 
![](./imagen5.png)
Si pudimos encontrar el usuario y el password. 
Pero esto no termina acá
 Ahora hacemos un smbclient para ingresar la contraseña 
 ![](./imagen6.png)
encontramos dos archivos y los descargamos con Get 
observemos que tienen 
![](./imagen7.png)
el primer archivo encontramos la contraseña Summer2019!
ahora en root 
![](./imagen8.png)
Obtuvimos la Flag ! :
HL{4dm1n_b4ckup_3xf1ltr4ti0n}
Lab Completado 

Que pude aprender? 
Como vulnerar el protocolo SMB p445
Como usar Hydra 
Como usar smbclient y conectarse de manera remota. 
Fue una experiencia larga, tuve errores que me tomaron tiempo pero pude avanzar. Un comentario que me haría a mi mismo es el prestar atención al escribir el comando, esto si no le presto atención podría hacerme perder mucho tiempo. 
