# Ejercicios Actividad 5
## 1. Crea un directorio llamado "dir1" y otro llamado "dir2".

<img width="626" height="202" alt="image" src="https://github.com/user-attachments/assets/d7489989-68f7-415d-854c-87c192deadbc" />


## 2. Explica qué diferencia existe entre ambos y muestra su equivalencia con la directiva Require:
~~~
<Directory /var/www/example1>
Order Deny,Allow
Deny from All
Allow from 192.168.1.100
</Directory>


<Directory /var/www/example1>
Order Allow,Deny
Deny from All
Allow from 192.168.1.100
</Directory>
~~~~
La diferencia radica en el orden en el que Apache va a permitir/denegar el acceso en este ejemplo concreto. En el primer caso, primero denegará todo el acceso de forma predeterminada y luego permitirá la conexión desde 192.168.1.100; y en el segundo ejemplo primero permitirá todo el acceso de forma predeterminada y luego denegará el acceso a todos excepto a 192.168.1.100.
Esta sería la sintaxis de la directiva "require" que haría lo mismo. Esta directiva solo nos permite la conexión desde esa ip en específico. 
~~~
<Directory /var/www/example1>
    Require ip 192.168.1.100
</Directory>
~~~

## 3. Para dir1

Vamos a trabajar dentro de etc/apache2/apache2.conf:

   ### a. Permite el acceso de las peticiones provenientes de 10.3.0.100

<img width="335" height="84" alt="image" src="https://github.com/user-attachments/assets/f1a597e6-c84b-46d0-9497-9acdb3857713" />

   ### b. Permite el acceso desde "marisma.intranet"

<img width="413" height="93" alt="image" src="https://github.com/user-attachments/assets/583a227e-8f36-4d24-88d6-7261516b968e" />
   
   ### c. Permite el acceso desde cualquier subdominio de "marisma.intranet"
   
<img width="409" height="92" alt="image" src="https://github.com/user-attachments/assets/a6a84923-45b3-45ca-911e-e726ebf21d6c" />
   
   ### d. Permite el acceso de las peticiones provenientes de "10.3.0.100" con máscara "255.255.0.0"

<img width="344" height="91" alt="image" src="https://github.com/user-attachments/assets/275b46fa-46bb-4cf8-857e-8542641a4d54" />

## 4. Modifica la configuración de forma que el acceso a dir1 se permita a "marisma.intranet" y no se permita desde 10.3.0.101"

Aquí usamos "RequireAll" para que se cumplan ambas condiciones. 
<img width="485" height="149" alt="image" src="https://github.com/user-attachments/assets/fca04242-f8de-4ad2-95c4-17c2b980b03e" />

## 5. Modifica la configuración de forma que el acceso a dir2 se permita a "10.3.0.100/8" y no a "marisma.intranet"

<img width="521" height="157" alt="image" src="https://github.com/user-attachments/assets/e30f3cbd-e9ec-4d97-b1a7-5b1aed947e93" />

