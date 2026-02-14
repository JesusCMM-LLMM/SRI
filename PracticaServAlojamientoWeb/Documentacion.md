# Práctica 2º Trimestre - Servidor de Alojamiento Web

## 0. Punto de partida.

En este primer apartado vamos a crear la máquina virtual y darle una IP estática para facilitarnos la vida más adelante. Nos vamos a nuestro Proxmox y creamos una MV con Ubuntu Server 24.04 LTS:

<img width="719" height="541" alt="image" src="https://github.com/user-attachments/assets/63ba6f82-ec1f-4fbd-af81-a34c41f6e6ec" />

<img width="884" height="392" alt="image" src="https://github.com/user-attachments/assets/341ba216-3cca-4db8-b457-e91c6df37562" />

Una vez hecho esto, vamos a instalar el sistema operativo, parándonos en dos puntos clave: 

<img width="1215" height="299" alt="image" src="https://github.com/user-attachments/assets/72567571-f121-4fa9-ac75-300bbcae942c" />

El primero es en la configuración de red, donde vamos a aprovechar para ponerle una ip estática. Vamos a Edit IPv4: 

<img width="660" height="256" alt="image" src="https://github.com/user-attachments/assets/78f4773c-8805-40d9-b9dd-b4a92ab88203" />

Y lo vamos a configurar de la siguiente manera:

<img width="667" height="430" alt="image" src="https://github.com/user-attachments/assets/55d52c06-6e99-4f5e-b281-1176f52db4e0" />

- La subnet es la subred de nuestro nodo en proxmox (la he visto en la interfaz del router virtual, cogiendo solo los tres primeros octetos)
- La Address va a ser nuestra IP, yo he elegido la 192.168.193.110
- Y el gateway (puerta de enlace) es la IP del router, para tener salida a internet.

<img width="1178" height="270" alt="image" src="https://github.com/user-attachments/assets/d268eacd-06b2-45de-a578-c0082a6909bd" />

Lo siguiente es configurar el perfil del administrador del sistema, de este modo: 

<img width="1223" height="433" alt="image" src="https://github.com/user-attachments/assets/900d51b3-e4cf-4a14-a1ae-6d9e7cfa1f13" />

Por último, dejamos activo ya el servidor SSH:

<img width="1280" height="343" alt="image" src="https://github.com/user-attachments/assets/6aa0717d-efdb-4113-8c6c-5c2447563f2b" />

Una vez finalice de instalarse, nos logueamos y vamos a dejar el sistema actualizado, para hacer un snapshot del estado actual de la máquina en Proxmox:

<img width="760" height="221" alt="image" src="https://github.com/user-attachments/assets/93a799e1-450b-474a-8345-1406a340b22c" />


# 1. Instalación de la base del servidor.

En este paso vamos a instalar los paquetes necesarios para todo lo que se nos pide en la práctica. 
Ésta es la lista de los paquetes que vamos a instalar, agrupados por su función, y la explicación de por qué:

## Servidor Web y PHP
- apache2 : Es el servidor web por excelencia, lo hemos usado ya mucho a lo largo del curso. 
- php y libapache2-mod-php: necesitamos alojar páginas dinámicas con PHP, necesitamos instalar el lenguaje PHP y el módulo que permite a Apache entender e interpretar el código PHP antes de enviarlo al cliente.
- php-mysql: Permite que las páginas web hechas en PHP (y también el programa phpMyAdmin) puedan hablar y extraer datos de tu base de datos MariaDB/MySQL.

## Base de Datos
- mariadb-server: Es el motor de base de datos relacional, compatible con MySQL.

- phpmyadmin: Es una aplicación web (escrita en PHP) con una interfaz gráfica para administrar tus bases de datos MariaDB/MySQL desde el navegador, la hemos usado en IAW.

## Servidor FTP
- vsftpd: Very Secure FTP Daemon. Es el programa que permitirá a tus clientes subir y descargar los archivos de sus páginas web a sus carpetas personales. 

## Servidor DNS
- bind9 (junto con a sus dependencias): Es el software de servidor DNS que hemos usado anteriormente. Lo vamos a necesitar para crear subdominios y configurar la resolución directa e inversa. Bind9 se encargará de traducir nombres como cliente1.midominio.local a nuestra IP 192.168.193.110.

## Soporte para Python en la Web
- python3 y libapache2-mod-wsgi-py3: WSGI (Web Server Gateway Interface) es el estándar que usa Apache para comunicar peticiones web directamente a scripts de Python de forma eficiente y segura.

Lo vamos a instalar todo en un solo comando, que va a quedar algo larguillo:
~~~
sudo apt install apache2 php libapache2-mod-php php-mysql mariadb-server phpmyadmin vsftpd bind9 bind9utils dnsutils python3 libapache2-mod-wsgi-py3 -y
~~~~

<img width="1291" height="131" alt="image" src="https://github.com/user-attachments/assets/e86df4ad-521d-4be2-9e85-c76f1d0bb92a" />

Cuando llegue a la parte de phpmyadmin tendremos que configurarlo correctamente, primero eligiendo apache2:

<img width="1040" height="360" alt="image" src="https://github.com/user-attachments/assets/afd90c04-dc92-41cc-bbb3-f0a6efc5e44a" />

Después nos pedirá configurar la base de datos de phpmyadmin:

<img width="1268" height="314" alt="image" src="https://github.com/user-attachments/assets/8b850bf5-4464-43d5-884e-59b54bcff3a4" />

Necesitaremos proporcionarle una contraseña: 

<img width="1255" height="282" alt="image" src="https://github.com/user-attachments/assets/a59cf03b-a92d-42d3-a059-b805fea9cf58" />

Y ya vemos que se crea correctamente y todos los paquetes se han instalado:

<img width="757" height="255" alt="image" src="https://github.com/user-attachments/assets/40d3f974-f9ac-433d-8304-e032039f940c" />

Como una última comprobación de este apartado, vamos a ver los diferentes servicios y su estado, uno por uno: 

- Apache2:
  <img width="1288" height="379" alt="image" src="https://github.com/user-attachments/assets/fa98618b-ffed-4855-9bbd-104550344e79" />

- Base de Datos (MariaDB):
  <img width="1279" height="401" alt="image" src="https://github.com/user-attachments/assets/8509dbf7-4f0e-4fcc-b60a-759357ed7444" />

- Servidor FTP (vsftpd):
  <img width="1200" height="400" alt="image" src="https://github.com/user-attachments/assets/7622ab73-3b43-4955-acc3-892d94459945" />

- Servidor DNS (Bind9):
  <img width="945" height="339" alt="image" src="https://github.com/user-attachments/assets/7d75770f-9f6b-4c1f-9585-041973e3dccc" />

## 3. 






