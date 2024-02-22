# CONEXIÓN VPN HACK THE BOX

Una vez iniciemos sesión,nos dirigimos a CONNECT TO HTB:

[![Screenshot-from-2024-02-21-20-47-47.png](https://i.postimg.cc/fy0RJTCG/Screenshot-from-2024-02-21-20-47-47.png)](https://postimg.cc/vxbsKyph)

Seleccionamos la opción de Machines

[![Screenshot-from-2024-02-21-21-41-21.png](https://i.postimg.cc/mDbGv3tp/Screenshot-from-2024-02-21-21-41-21.png)](https://postimg.cc/3yb6pvj2)

Luego seleccionamos OpenVPN y descargamos el archivo

[![Screenshot-from-2024-02-21-21-43-17.png](https://i.postimg.cc/rs0Z3zCY/Screenshot-from-2024-02-21-21-43-17.png)](https://postimg.cc/n9x1QFWv)

Ejecutamos el comando de openvpn en la terminal

[![Screenshot-from-2024-02-21-21-54-34.png](https://i.postimg.cc/sD9fN262/Screenshot-from-2024-02-21-21-54-34.png)](https://postimg.cc/bsrjGqjX)

# NMAP A MAQUINA MEOW

Una vez tengamos el Vpn activo procedemos a realizar el Nmap a la maquina

[![Screenshot-from-2024-02-21-22-14-55.png](https://i.postimg.cc/Jz0nHLx4/Screenshot-from-2024-02-21-22-14-55.png)](https://postimg.cc/PCGh000B)
[![Screenshot-from-2024-02-21-22-22-56.png](https://i.postimg.cc/SsNtkgq5/Screenshot-from-2024-02-21-22-22-56.png)](https://postimg.cc/qtSGGXNX)

Una vez realizado el Nmap, podemos ver la siguiente información

[![Screenshot-from-2024-02-21-22-31-38.png](https://i.postimg.cc/kMNzKRYf/Screenshot-from-2024-02-21-22-31-38.png)](https://postimg.cc/DmZxK0TX)

Identificamos sus puertos abiertos, en este caso es el 23/TCP telnet en el cual se está ejecutando un sistema Linux.

Luego procedemos a ejecitar el siguiente comando: telnet (ipMaquina)

[![Screenshot-from-2024-02-21-22-39-54.png](https://i.postimg.cc/t4LG2Q35/Screenshot-from-2024-02-21-22-39-54.png)](https://postimg.cc/gxq727BX)

Procedemos a intentar con la contraseña mas común, que en este caso es: root

[![Screenshot-from-2024-02-21-22-38-57.png](https://i.postimg.cc/q734TMJS/Screenshot-from-2024-02-21-22-38-57.png)](https://postimg.cc/8FNqdGrm)

procedemos a listar y obtener la bandera

[![Screenshot-from-2024-02-21-22-41-36.png](https://i.postimg.cc/hvh2khg7/Screenshot-from-2024-02-21-22-41-36.png)](https://postimg.cc/PvsbZXCt)


