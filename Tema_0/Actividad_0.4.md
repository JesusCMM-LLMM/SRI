# Actividad 0.4 - CURL

## Busca información sobre el comando curl y muestra al menos cinco ejemplos de uso

cURL es una herramienta de línea de comandos muy usada para transferir datos desde o hacia un servidor, usando los protocolos más comunes de Internet como HTTP, HTTPS, FTP, SFTP, SCP, DICT, LDAP, entre otros. 

Internamente emplea la librería libcurl (por eso muchos programas también la usan). 
Su sintaxis básica es: 
~~~
curl [OPCIONES] URL
~~~

Permite hacer peticiones HTTP (GET, POST, PUT, DELETE…), subir archivos, autenticarse con usuario/contraseña, manejar cabeceras, seguir redireccionamientos, etc. También soporta muchas opciones para modificar el comportamiento: mostrar cabeceras, hacer modo silencioso, limitar velocidad, usar certificados, etc.

### Cinco ejemplos de uso

  1.-	curl https://www.ejemplo.com/	-> Realiza una petición HTTP GET al sitio y muestra el contenido HTML en la salida estándar. 

  2.- curl -I https://www.ejemplo.com/	-> Obtiene solo las cabeceras HTTP (usando el método HEAD). No descarga el cuerpo de la página. 

  3.- curl -o archivo.html https://www.ejemplo.com/pagina.html	Descarga la página y la guarda localmente con el nombre archivo.html. 

  4.- curl -O https://www.ejemplo.com/imagen.jpg	Descarga la imagen y la guarda con el nombre original (imagen.jpg). La opción -O toma el nombre del recurso remoto. 

  5.-	curl -X POST -d "usuario=juan&clave=secreto" https://api.ejemplo.com/login	Envía datos (formato application/x-www-form-urlencoded) mediante POST a una API o formulario web. 

  6.-	curl -L https://www.ejemplo.com	Sigue redirecciones HTTP (por ejemplo, si el servidor responde con código 301/302). La opción -L hace que curl siga los redireccionamientos automáticamente. 
