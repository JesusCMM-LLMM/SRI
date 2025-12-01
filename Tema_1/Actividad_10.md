# Actividad 10 - SSL
#1. Teniendo una instancia EC2 creada, nos conectamos por SSH desde nuestro equipo. 

<img width="1091" height="788" alt="image" src="https://github.com/user-attachments/assets/5b985e76-9122-4ddb-a9a0-343bca9c8090" />

## 1.1 Instalación del servidor web Apache

Con sudo apt update y sudo apt install apache2 -y completamos este paso:

<img width="501" height="96" alt="image" src="https://github.com/user-attachments/assets/07241f56-e14c-4294-b397-47a12b37945e" />

## 1.2 Creación del certificado autofirmado

Vamos a utilizar openssl con este comando: 
~~~
sudo openssl req \
  -x509 \
  -nodes \
  -days 365 \
  -newkey rsa:2048 \
  -keyout /etc/ssl/private/apache-selfsigned.key \
  -out /etc/ssl/certs/apache-selfsigned.crt
~~~

<img width="469" height="148" alt="image" src="https://github.com/user-attachments/assets/8a93b8ff-f666-452a-a323-e5a4420ddc19" />

Y empezamos a introducir por teclado los datos que se nos piden. 

<img width="667" height="192" alt="image" src="https://github.com/user-attachments/assets/1da8efa8-2c6c-4263-b40c-cfd47b2bd428" />

## 1.3 Cómo automatizar la creación de un certificado autofirmado

Como ya lo hemos creado manualmente, no voy a ejecutar el script ahora mismo, pero está bien guardarlo para un futuro, cuando por ejemplo caduque el que acabo de crear, así que lo voy a guardar. 

<img width="1541" height="441" alt="image" src="https://github.com/user-attachments/assets/11170fb7-9b14-48c7-91c4-628d0af52ebc" />

## 1.4 Cómo consultar la información del sujeto del certificado

Usamos el comando openssl x509 -in /etc/ssl/certs/apache-selfsigned.crt -noout -subject

<img width="1046" height="47" alt="image" src="https://github.com/user-attachments/assets/3fe46b3a-1f0c-45d5-bafb-3cf1b3e9aaff" />

## 1.5 Cómo consultar la fecha de caducidad del certificado

Usamos el comando openssl x509 -in /etc/ssl/certs/apache-selfsigned.crt -noout -dates

<img width="875" height="72" alt="image" src="https://github.com/user-attachments/assets/730666b0-61f6-461c-a6a4-09a21189bfa9" />

## 1.6 Configuración de un VirtualHost con SSL/TSL en el servidor web Apache

utilizaremos el archivo de configuración que tiene Apache por defecto para SSL/TLS, que está en la ruta: /etc/apache2/sites-available/default-ssl.conf y modificaremos esto:

<img width="677" height="210" alt="image" src="https://github.com/user-attachments/assets/19c40850-a7ce-4441-8e9a-5b94d2243cc5" />

Habilitamos este virtual host (sudo a2ensite default-ssl.conf), iniciamos el modulo ssl (sudo a2enmod ssl), reiniciamos apache y seguimos.

Configuramos el virtual host de HTTP para que redirija todo el tráfico a HTTPS, yendo a /etc/apache2/sites-available/000-default.conf y editándolo de la siguiente manera:

<img width="759" height="642" alt="image" src="https://github.com/user-attachments/assets/27f0bbe1-e29f-4dc8-a626-76f6dc9ba5ca" />

Activamos el módulo rewrite (sudo a2enmod rewrite) y reiniciamos para que surtan efecto los cambios. Como estoy desde la consola lo compruebo con un curl:

<img width="520" height="251" alt="image" src="https://github.com/user-attachments/assets/e1a76fa7-4065-42f8-a968-3b1aaa4b1d38" />


#2. CERTBOT
Vamos a usar una Autoridad de Certificación (Let's Encrypt) para tener un certificado válido que los navegadores no marquen como peligroso.
Nos registramos en https://www.noip.com/es-MX y creamos un hostname con la ip pública de nuestra instancia de EC2: 
<img width="1266" height="258" alt="image" src="https://github.com/user-attachments/assets/bebb406e-ea9e-4406-8a3a-6dbba76fff83" />

De nuevo en nuestra consola conectada por SSH a nuestra instancia, instalamos certbot con:

<img width="698" height="57" alt="image" src="https://github.com/user-attachments/assets/9a2708b2-7539-4692-af8c-16d21523353b" />

Y ya solicitamos el certificado con certbot:

~~~
sudo certbot --apache
~~~
<img width="754" height="565" alt="image" src="https://github.com/user-attachments/assets/fcca160f-42dd-413f-8070-043b9ced79f1" />

<img width="880" height="399" alt="image" src="https://github.com/user-attachments/assets/90a0f218-f90f-4b32-9ebe-f292504ba51f" />

Y con esto ya hemos acabado. 


























