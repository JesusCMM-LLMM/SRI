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

<img width="464" height="154" alt="image" src="https://github.com/user-attachments/assets/960f5264-e8e2-47e3-990e-780321e11666" />

Y comprobamos ambos dominios:

<img width="546" height="173" alt="image" src="https://github.com/user-attachments/assets/4c1e1b08-0796-4097-98da-753f734ab9cd" />

<img width="551" height="176" alt="image" src="https://github.com/user-attachments/assets/060f3a76-3e87-4317-9b00-c2f2559c29db" />

