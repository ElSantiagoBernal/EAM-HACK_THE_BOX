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

# NMAP A MAQUINA FAWN

![image](https://github.com/ElSantiagoBernal/EAM-HACK_THE_BOX/assets/100774275/758cdf3f-8ceb-4f81-a7ff-6b08408a9f08)

Procedemos a hacer Nmap a la ip de la máquina

[![Screenshot-from-2024-02-21-22-56-00.png](https://i.postimg.cc/430CmCdt/Screenshot-from-2024-02-21-22-56-00.png)](https://postimg.cc/4Kp2SSpN)

En este caso el puerto abierto es 21/TCP ftp vsftpd 3.0.3. Por lo tanto, procedemos a acceder con ftp, en este caso el usuario es anonymous y la contraseña root

[![Screenshot-from-2024-02-21-23-00-15.png](https://i.postimg.cc/ZnTLmnSL/Screenshot-from-2024-02-21-23-00-15.png)](https://postimg.cc/N9zX7gLy)

Una vez iniciada la sesión obtenemos el archivo flag con: get flag.txt

[![Screenshot-from-2024-02-21-23-03-00.png](https://i.postimg.cc/nhQB6BmJ/Screenshot-from-2024-02-21-23-03-00.png)](https://postimg.cc/RW4Wt3Gs)

En este caso quedará guardado localmente en un archivo.




