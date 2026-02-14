# Práctica 2º Trimestre - Servidor de Alojamiento Web

# 0. Punto de partida.

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

# 3. Configuraciones

El objetivo aquí es dejar el terreno preparado para que, cuando ejecutemos el script, este solo tenga que añadir usuarios y no preocuparse de configurar los servicios desde cero. Lo dividiremos en tres pasos clave.

## 3.1. Asegurar el FTP con certificados TLS.

Vamos a hacer que el acceso FTP configure adecuadamente TLS: esto convierte el FTP normal, que es inseguro, en FTPS, cifrando las contraseñas y archivos. Para esto vamos a crear un certificado autofirmado válido por un año, con este comando en el cual ya le pasamos los datos con -subj: `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/vsftpd.key -out /etc/ssl/certs/vsftpd.crt -subj "/C=ES/ST=Andalusia/L=Huelva/O=Hosting/CN=192.168.193.110"`

<img width="1895" height="387" alt="image" src="https://github.com/user-attachments/assets/a5d1e914-6ac3-49c4-a17e-04e405d2d525" />

Ahora vamos a configurar vsftpd para que lo use. Nos vamos a su archivo de configuración: 

<img width="731" height="426" alt="image" src="https://github.com/user-attachments/assets/fba2d7dc-8c4d-4b7d-a909-2cc99a5b5df4" />

Descomentamos el write_enable para permitir que los usuarios puedan subir sus archivos mediante FTP:

<img width="558" height="62" alt="image" src="https://github.com/user-attachments/assets/27b160b3-3cf3-4fa4-9fed-4fc0c2bae447" />

Y también borramos al final del todo las líneas relacionadas con el certificado RSA para añadirles las que apuntan a nuestro certificado TSL: 

<img width="495" height="244" alt="image" src="https://github.com/user-attachments/assets/79d65861-53c4-4458-be91-3fc037c940f0" />

Guardamos los cambios y reiniciamos el servicio. Para comprobar que el certificado esté aplicado correctamente, usamos este comando -> `openssl s_client -connect 127.0.0.1:21 -starttls ftp`:

<img width="755" height="147" alt="image" src="https://github.com/user-attachments/assets/0357e092-a58c-4630-a37e-e7ac03a7cb91" />

Ahí vemos que esta conectado (CONNECTED(00000003)) y que tiene los datos de nuestro certificado (subject=C = ES, ST = Andalusia, L = Huelva...).

## 3.2. Preparar las Zonas del DNS (Bind9).

Nuestro script creará los subdominios (ej. cliente1.midominio.local), pero para que pueda hacerlo, primero debe existir el dominio principal. Vamos a llamarlo midominio.local y a declarar las zonas en bind poniéndolas en el archivo de configuración: 

<img width="724" height="416" alt="image" src="https://github.com/user-attachments/assets/2ad163af-8f6c-4cc8-8cff-3995d237c461" />

Ahora vamos a crear el archivo de la zona directa:

<img width="724" height="330" alt="image" src="https://github.com/user-attachments/assets/99321bea-d844-43f8-95dc-ed30bc6d291a" />

Y lo comprobamos: 

<img width="865" height="51" alt="image" src="https://github.com/user-attachments/assets/b4a81af3-bf41-4033-a1f8-2694240e29eb" />

Y también el de la zona inversa: 

<img width="737" height="422" alt="image" src="https://github.com/user-attachments/assets/12a190b1-0048-46d5-bae2-ad6333bded2d" />

Con su correspondiente comprobación: 

<img width="830" height="56" alt="image" src="https://github.com/user-attachments/assets/b35c92f5-d4ae-4bac-87cb-00a4a1f449a8" />

Reiniciamos Bind9 para que cargue el nuevo dominio:

<img width="727" height="226" alt="image" src="https://github.com/user-attachments/assets/99d2399d-cde3-4c2d-a57a-3b521570dce8" />

Y lo comprobamos con dig:

<img width="628" height="58" alt="image" src="https://github.com/user-attachments/assets/0c6cf748-8028-45cd-9e1a-9722c4492d3d" />

## 3.3. Habilitar Python en Apache.

Como ya instalamos el paquete `libapache2-mod-wsgi-py3` en la fase anterior, solo tenemos que decirle a Apache que lo active. Usamos estos dos comandos:

<img width="548" height="83" alt="image" src="https://github.com/user-attachments/assets/1a711d43-7813-4ba6-a58c-7f33acb99047" />

Comprobación:

<img width="1645" height="135" alt="image" src="https://github.com/user-attachments/assets/c9e3b117-99d4-42b8-a105-3956accff8cf" />

Llegados a este punto, el servidor está 100% preparado. Tiene el motor listo, el FTP seguro, el DNS sabe quién es, y Apache entiende Python.

# 4. El Script de Automatización.

Creamos un archivo para el script (nuevo_cliente.sh) y este sería el script:

~~~
#!/bin/bash

# Script de automatización de alojamiento
################################################################################

# Validación inicial
if [ "$#" -ne 2 ]; then
    echo "Introduzca los parámetros cliente y contraseña, por ese orden."
    echo "Ejemplo: sudo ./crear_cliente.sh cliente1 password123"
    exit 1
fi

USUARIO=$1
PASS=$2
DOMINIO="${USUARIO}.midominio.local"
IP_SERVIDOR="192.168.193.110"
OCTETO_FINAL="110" 

echo "*** Iniciando despliegue para el usuario: $USUARIO ***"

# Creación del usuario del sistema (Acceso FTP, SSH y SFTP) y Directorio Web
#################################################################################


echo "[1/5] Creando usuario del sistema y directorio web..."
# -m crea el home, -s /bin/bash permite acceso por SSH/SFTP
useradd -m -s /bin/bash $USUARIO
echo "$USUARIO:$PASS" | chpasswd

DIR_WEB="/home/$USUARIO/public_html"
mkdir -p $DIR_WEB

# Página web dinámica por defecto (PHP)
cat <<EOF > $DIR_WEB/index.php
<!DOCTYPE html>
<html>
<head><title>Bienvenido $USUARIO</title></head>
<body>
    <h1>Hosting configurado correctamente para $DOMINIO</h1>
    <?php echo "<p>Soporte PHP activado. ¡Hola mundo!</p>"; ?>
</body>
</html>
EOF

# Permisos para que Apache pueda leer, pero el dueño sea el usuario
chown -R $USUARIO:www-data /home/$USUARIO
chmod -R 755 /home/$USUARIO

# Base de datos MySQL / MariaDB (ALL PRIVILEGES)
################################################################################

echo "[2/5] Creando base de datos y usuario SQL..."
DB_NAME="${USUARIO}_db"
mysql -u root -e "CREATE DATABASE ${DB_NAME};"
mysql -u root -e "CREATE USER '${USUARIO}'@'localhost' IDENTIFIED BY '${PASS}';"
mysql -u root -e "GRANT ALL PRIVILEGES ON ${DB_NAME}.* TO '${USUARIO}'@'localhost';"
mysql -u root -e "FLUSH PRIVILEGES;"

# Virtual Host en Apache (Web normal y Python)
################################################################################

echo "[3/5] Configurando Virtual Host en Apache..."
VHOST_FILE="/etc/apache2/sites-available/${DOMINIO}.conf"

cat <<EOF > $VHOST_FILE
<VirtualHost *:80>
    ServerName $DOMINIO
    DocumentRoot $DIR_WEB

    <Directory $DIR_WEB>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    # Configuración para ejecutar Python (WSGI)
    WSGIScriptAlias /python $DIR_WEB/app.wsgi
    <Directory $DIR_WEB>
        <Files app.wsgi>
            Require all granted
        </Files>
    </Directory>

    ErrorLog \${APACHE_LOG_DIR}/${USUARIO}_error.log
    CustomLog \${APACHE_LOG_DIR}/${USUARIO}_access.log combined
</VirtualHost>
EOF

# App Python de prueba
cat <<EOF > $DIR_WEB/app.wsgi
def application(environ, start_response):
    status = '200 OK'
    output = b'Hola! La aplicacion Python funciona en tu hosting. \n'
    response_headers = [('Content-type', 'text/plain'),
                        ('Content-Length', str(len(output)))]
    start_response(status, response_headers)
    return [output]
EOF
chown $USUARIO:www-data $DIR_WEB/app.wsgi

# Activamos el sitio en Apache
a2ensite ${DOMINIO}.conf
systemctl reload apache2

# DNS (Subdominio y Resolución Inversa)
################################################################################

echo "[4/5] Configurando registros DNS en Bind9..."
ZONA_DIRECTA="/etc/bind/db.midominio.local"
ZONA_INVERSA="/etc/bind/db.193"

# Añadir a zona directa
echo "${USUARIO}    IN    A    ${IP_SERVIDOR}" >> $ZONA_DIRECTA
# Añadir a zona inversa
echo "${OCTETO_FINAL}      IN    PTR  ${DOMINIO}." >> $ZONA_INVERSA

systemctl restart bind9

# TODO LISTO

echo "[5/5] ¡Proceso completado con éxito!"
echo "-----------------------------------------------------"
echo "Resumen de acceso:"
echo "- Web (PHP): http://$DOMINIO"
echo "- Web (Python): http://$DOMINIO/python"
echo "- Base de datos: $DB_NAME (Usuario: $USUARIO)"
echo "- FTP/SSH/SFTP: Usuario $USUARIO"
echo "¡GRACIAS POR CONTRATAR NUESTROS SERVICIOS!"
echo "-----------------------------------------------------"
~~~

<img width="748" height="741" alt="image" src="https://github.com/user-attachments/assets/3b414ea3-25f4-44ca-82f5-9e814e4f0216" />

Le damos permisos de ejecución y ya estaría listo para usar. Como prueba, vamos a crear al usuario Pepe con contraseña 6767:

<img width="507" height="312" alt="image" src="https://github.com/user-attachments/assets/274e6271-459a-4f95-9a8c-0a3a1b5393fe" />

## 4.1 Comprobaciones usando curl:

Primero probamos que el DNS resuelve el subdominio del cliente:

<img width="544" height="385" alt="image" src="https://github.com/user-attachments/assets/9dd38f57-e101-47be-93bc-3962b9d3c980" />

Vale, esto es un error que no indica que hayamos hecho nada mal. Parece que el despliegue está correcto, pero como antes configuramos el DNS con 8.8.8.8 pues estamos preguntando a Google (8.8.8.8) y ninguno de esos servidores externos sabe qué es midominio.local. Creo que todo lo que necesitamos lo tenemos en el propio bind9. Podemos comprobar que esto es así si a usamos dig preguntandole directamente al localhost:

<img width="581" height="61" alt="image" src="https://github.com/user-attachments/assets/395349bd-3933-42cf-917c-f36762c00d50" />

Ahí veo que estaba en lo correcto. Así que vamos a cambiar el netplan para que el servidor DNS sea el propio localhost. Buscamos el archivo con ls /etc/netplan/ y el mío es 50-cloud-init.yaml asi que lo edito con sudo nano /etc/netplan/50-cloud-init.yaml añadiendo a los nameservers mi dirección localhost y dejando como secundaria la de Google:

<img width="343" height="295" alt="image" src="https://github.com/user-attachments/assets/e2c72b0b-fb6f-4e2c-9e31-fd325a908f3e" />

Aplicamos los cambios con sudo netplan apply y listo. Ya podemos comprobar con ping:

<img width="581" height="167" alt="image" src="https://github.com/user-attachments/assets/7743bd5b-1d80-4e49-9ab8-3496ca97139c" />

Aunque ping sigue sin funcionar, puede deberse a que el servicio interno de red de Ubuntu (systemd-resolved) tiene una medida de seguridad por la cual a veces ignora la dirección 127.0.0.1 para evitar "bucles infinitos" de red, y se empeña en preguntarle al DNS secundario. Pero con dig nos devuelve la IP sin problemas. 

Vamos a probar la web/PHP con curl:

<img width="715" height="167" alt="image" src="https://github.com/user-attachments/assets/61c5337b-23ee-456a-bc25-f0bcf6c734ce" />

Y la aplicación de Python:

<img width="723" height="40" alt="image" src="https://github.com/user-attachments/assets/eb072c6a-5ded-4298-aadc-44ef1804c459" />

* Fixed -> el salto de línea en el script original

# 5. Docker.




