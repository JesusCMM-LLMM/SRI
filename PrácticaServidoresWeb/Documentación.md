# Práctica Primer  Trimestre - Servidores Web

## 0. Preparación. 

Partiendo desde una instalación limpia de Ubuntu 25.01, lo primero que vamos a hacer es actualizar todos los paquetes: 

<img width="662" height="476" alt="image" src="https://github.com/user-attachments/assets/594e42e9-02c3-4627-87fe-6a4f71b5efcf" />

Esperamos a que se complete y vamos a por el primer punto.

## 1.- Dominios mediante el archivo hosts.

Según el enunciado, necesitamos simular dos dominios primero (centro.intranet y departamentos.centro.intranet) y un tercero para la parte final de la práctica con nginx ( servidor2.centro.intranet). Para esto nos vamos al archico hosts y lo editamos: 

<img width="571" height="175" alt="image" src="https://github.com/user-attachments/assets/67b04454-1de6-43c9-9310-bae92cf1891c" />

Para comprobar que esto se ha ejecutado correctamente, vamos a hacer ping a esos dominios que hemos añadido: 

<img width="577" height="186" alt="image" src="https://github.com/user-attachments/assets/76579577-1bec-4551-aad8-299e9eb44cb1" />

<img width="571" height="175" alt="image" src="https://github.com/user-attachments/assets/fa93e7c4-9280-440d-9954-ae83e78b1472" />

<img width="565" height="168" alt="image" src="https://github.com/user-attachments/assets/167887eb-4f63-421d-9648-de7252b26ea0" />

## 2.- Instalación de la pila LAMP

Vamos a instalar Apache, MySQL y PHP todo a la misma vez mediante el repositorio apt:

<img width="1148" height="302" alt="image" src="https://github.com/user-attachments/assets/2095d1e2-5137-4966-ab1c-6e59e9ea3c8e" />

Una vez se ha instalado, vamos a activar el servicio de apache:

<img width="859" height="478" alt="image" src="https://github.com/user-attachments/assets/4d346f6f-7b17-403b-b5bb-b39bc02199d1" />

Con esto ya quedaría instalada la pila LAMP, más adelante configuraremos los elementos por separado.

## 3.- Instalación y Configuración de WordPress

El dominio centro.intranet será el que servirá el wordpress. Lo primero que vamos a hacer es crear la base de datos, sin ella el wordpress no funciona:

<img width="771" height="362" alt="image" src="https://github.com/user-attachments/assets/5372f1eb-3ad5-4b78-b2b4-d986d7c67929" />

Dentro de sql, creamos la base de datos con estos parámetros: 
~~~
CREATE DATABASE wordpressdb;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'user';
GRANT ALL PRIVILEGES ON wordpressdb.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
~~~
Según he visto, es la base de datos más sencilla para que Wordpress funcione. 

<img width="587" height="257" alt="image" src="https://github.com/user-attachments/assets/d9b872d1-0556-481e-bb0f-6a5a20fbb163" />

Después de esto, vamos a descargar Wordpress:

<img width="705" height="234" alt="image" src="https://github.com/user-attachments/assets/590d5da5-1cf6-461c-bec6-4ef9755b1375" />

Lo descomprimimos, movemos y le cambiamos los permisos:

<img width="420" height="63" alt="image" src="https://github.com/user-attachments/assets/dc836d4b-7dee-450a-a1bf-d4ac51ad5a76" />

<img width="601" height="87" alt="image" src="https://github.com/user-attachments/assets/66f27f23-3c67-44e2-b6b9-a89acd31b9bf" />

Por último, vamos a configurar el VirtualHost, creando el archivo de configuración para el sitio:

<img width="609" height="31" alt="image" src="https://github.com/user-attachments/assets/86ff82ab-5b87-4f84-adaf-67227861c167" />

Lo creamos con esta configuración:

<img width="879" height="219" alt="image" src="https://github.com/user-attachments/assets/393f0a14-1038-467b-bd6c-402407a6cab2" />

Habilitamos el sitio con el modulo a2ensite:

<img width="444" height="126" alt="image" src="https://github.com/user-attachments/assets/d06c3afb-8b30-47bc-8183-3bf6d79259f4" />

Para comprobar que esto se ha realizado correctamente, vamos al navegador y ponemos en la barra de búsqueda “centro.intranet” y nos debería aparecer la página de configuración de wordpress:

<img width="1211" height="768" alt="image" src="https://github.com/user-attachments/assets/409c6a74-209f-488b-9e8a-2f8cf1f29b99" />

Podemos completarla para finalizar la instalación. Ponemos los datos y en la siguiente ventana nos conectamos a la base de datos: 

<img width="744" height="589" alt="image" src="https://github.com/user-attachments/assets/f9dab058-6357-4061-8fc4-c06ed3ec6513" />

Rellenamos el nombre, nombre de usuario...

<img width="743" height="632" alt="image" src="https://github.com/user-attachments/assets/7b0063a7-35ff-4251-8e08-48f7f7ea6846" />

<img width="741" height="306" alt="image" src="https://github.com/user-attachments/assets/e5e4e91e-d8ed-4abb-a812-3ac6c8910ccf" />

Y con esto ya quedaría instalado.

<img width="1195" height="668" alt="image" src="https://github.com/user-attachments/assets/06463d57-a808-4df9-9eb1-b0f94cf470de" />

## 4.- Aplicación Python con WSGI 

El dominio departamentos.centro.intranet es el que servirá la aplicación de python. Primero de todo necesitamos instalar el módulo WSGI: 

<img width="565" height="51" alt="image" src="https://github.com/user-attachments/assets/bb09a4b5-6d01-420b-a7fb-4f0b8e5f3f3e" />

Una vez instalado, vamos a crear la carpeta donde estará el script, así como el propio script:

<img width="519" height="51" alt="image" src="https://github.com/user-attachments/assets/1cbec2ae-e7b7-42b8-a040-4f2ddcb755ad" />

En cuanto al script, voy a usar uno de mi repositorio de github, así que copiaré el código directamente. 
Vamos a configurar el VirtualHost para Python: 

<img width="652" height="32" alt="image" src="https://github.com/user-attachments/assets/34465c9b-0977-4a92-a8c9-f1f5d18feb9c" />

<img width="946" height="286" alt="image" src="https://github.com/user-attachments/assets/0799608c-7c3f-4fa4-89f8-4001d018b4f6" />

Para terminar, vamos a habilitar el sitio:

<img width="479" height="129" alt="image" src="https://github.com/user-attachments/assets/bc23a807-11a0-4835-a97b-f310dc63a211" />

Para demostrar que funciona vamos a hacer lo mismo que para demostrar el wordpress, pero con el dominio “departamentos.centro.intranet”:

<img width="697" height="278" alt="image" src="https://github.com/user-attachments/assets/3f450719-788b-4cf7-95dc-e1cce7349e95" />

## 5.- Proteger Python con Autenticación

Lo primero que hacemos es crear el archivo de contraseñas:

<img width="598" height="102" alt="image" src="https://github.com/user-attachments/assets/b4812ef7-b7ae-4c6c-bd56-decddcb8c215" />

Y ahora vamos a modificar el archivo de configuración del VirtualHost, dentro de directory vamos a añadir el método de autenticación:

<img width="491" height="340" alt="image" src="https://github.com/user-attachments/assets/eaa4f640-a923-4161-9830-8c56ac743968" />

Recargamos apache y comprobamos que nos pide usuario y contraseña en el navegador:

<img width="1178" height="406" alt="image" src="https://github.com/user-attachments/assets/e1597eaf-d4ec-40d9-86ec-4021756e742f" />

Ingresamos el nombre y usuario y ya podemos acceder:

<img width="806" height="338" alt="image" src="https://github.com/user-attachments/assets/31f9cdb7-ceb4-4352-a487-3c05fe67d809" />

## 6.- Instalar y Configurar AWStats

Vamos a instalar awstats, que es una herramienta de estadisticas:

<img width="534" height="207" alt="image" src="https://github.com/user-attachments/assets/26d3744d-fc84-4dab-bfaa-192696026656" />

Vamos a configurarla para centro.intranet, copiando la configuración base:

<img width="804" height="49" alt="image" src="https://github.com/user-attachments/assets/a2198a7a-b9b0-4fb2-a323-0beb77c79d21" />

Y modificamos estas líneas:

<img width="383" height="49" alt="image" src="https://github.com/user-attachments/assets/40671b68-872b-4292-bfb2-07b3e52875e3" />

<img width="263" height="52" alt="image" src="https://github.com/user-attachments/assets/df454234-0e20-47a7-951c-cd184d69b2b4" />

Guardamos el archivo y vamos a hablitar CGI en Apache, puesto que lo necesitamos para ver las gráficas:

<img width="455" height="158" alt="image" src="https://github.com/user-attachments/assets/29b0d47e-7e99-48c4-a492-d8f20d091fb1" />

Como último paso, generamos las estadísticas iniciales:

<img width="968" height="263" alt="image" src="https://github.com/user-attachments/assets/cbc0cde3-e0fa-4ca9-ab55-2f747c977d7d" />

Y para comprobarlo, nos vamos al navegador y ponemos lo siguiente:

<img width="970" height="326" alt="image" src="https://github.com/user-attachments/assets/63968776-6b15-44b5-84fb-cf7811330db6" />

## 7.- NGINX y PHPMyAdmin

Para que no haya interferencias entre apache y nginx, nginx y phpmyadmin lo vamos a poner en el puerto 8080. Primero, lo instalamos. Como Apache usa PHP como módulo, Nginx necesita php-fpm:

<img width="483" height="40" alt="image" src="https://github.com/user-attachments/assets/f19ad461-515f-4c7c-86ed-c09b7831e3ec" />

Si Nginx falla al iniciarse es porque el puerto 80 está ocupado por Apache. Eso es normal, ahora lo cambiamos. Editamos la configuración por defecto: 

<img width="559" height="31" alt="image" src="https://github.com/user-attachments/assets/62e3a884-993f-4a51-83bc-04eed85b4c73" />


Y editamos las líneas: 

<img width="368" height="75" alt="image" src="https://github.com/user-attachments/assets/209b86fb-aea5-440e-ab7d-74fbf259de1d" />

<img width="528" height="44" alt="image" src="https://github.com/user-attachments/assets/fadbbf33-6bad-4311-86af-cd16a083d688" />

<img width="429" height="157" alt="image" src="https://github.com/user-attachments/assets/6113ac90-9ff9-4f58-8e2c-792f26462e46" />


Y reiniciamos ngincx con sudo systemctl restart nginx. Comprobamos su estado:

<img width="1016" height="407" alt="image" src="https://github.com/user-attachments/assets/e56d4476-3535-48d0-891b-6a360a17315c" />


Lo siguiente va a ser instalar PHPMyAdmin, con sudo apt install phpmyadmin -y, y se nos va directamente a la configuración de phpmyadmin.
No marcamos ninguna de las dos opciones, nos vamos directamente a Aceptar:

<img width="866" height="227" alt="image" src="https://github.com/user-attachments/assets/da2a6069-2ce7-4cba-8462-58a9d487bcb5" />

<img width="1178" height="291" alt="image" src="https://github.com/user-attachments/assets/340f3b81-e215-4dab-8428-2124401c7087" />

<img width="1136" height="205" alt="image" src="https://github.com/user-attachments/assets/c222598c-1d63-40dd-9b56-041025409593" />

Una vez instalado, vamos a vincular a nginx mediante un enlace simbólico. 

<img width="670" height="54" alt="image" src="https://github.com/user-attachments/assets/d66e9405-01bb-4b48-92f6-bdbede49618c" />

Y para terminar vamos a http://servidor2.centro.intranet:8080/phpmyadmin : 

<img width="1213" height="582" alt="image" src="https://github.com/user-attachments/assets/a144288d-d718-4c65-b3cf-7bd99c71e3e2" />














