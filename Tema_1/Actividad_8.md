# VirtualHost

## Paso 1 - Crear la Estructura del Directorio

Vamos a crear la estructura del sitio, creando dos directorios para alojar la información del sitio y sus archivos:

![alt text](image.png)

## Paso 2 - Otorgar permisos

Para poder modificar los archivos en nuestro directorio web, necesitamos cambiar el propietario haciendo lo siguiente:

![alt text](image-1.png)

Aparte, vamos a modificar ciertos permisos de lectura:

![alt text](image-2.png)

## 3.- Crear una Página de Prueba para cada Virtual Host

Vamos a copiar el archivo de configuración de configuración por defecto para ejemplo.com, y una vez copiado lo editamos:

![alt text](image-3.png)

Una vez copiado, vamos a editarlo: 


![alt text](image-4.png)

Ahora hacemos lo mismo para el segundo dominio. Copiamos este archivo que acabamos de crear y lo editamos para que funcione con 'pruebas.com':

![alt text](image-5.png)

## 5.- Habilita los nuevos Archivos Virtual Host

Vamos a usar a2ensite para habilitarlos

![alt text](image-6.png)

Modificamos el archivo /etc/hosts:

![alt text](image-7.png)

