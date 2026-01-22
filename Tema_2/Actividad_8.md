# Subdominios
El ejercicio pide crear iesmarisma.intranet, pero como ya tengo montada y funcionando marisma.intranet, lo que voy a hacer es crear el subdominio informatica.marisma.intranet.
Voy usar el método de Subdominio Virtual, que es escribirlo todo en el mismo fichero. Es lo más fácil y menos propenso a errores.

Para esto, lo que tengo que hacer es editar el fichero de zona de marisma.intranet. Aquí nos aseguraremos de tener los hosts principales (smtp, ftp. www) y crearemos los del subdominio:

<img width="1295" height="798" alt="image" src="https://github.com/user-attachments/assets/0cd874ad-e289-43fe-b15a-5e461ed833fb" />

Al escribir www.informatica dentro de la zona marisma.intranet, BIND entiende automáticamente que el nombre completo (FQDN) es www.informatica.marisma.intranet.

Comprobamos la sintaxis y una vez esté todo OK, reiniciamos BIND:

<img width="854" height="75" alt="image" src="https://github.com/user-attachments/assets/abf0566a-77f7-4121-982e-3fb677c77089" />

Ahora nos vamos al cliente y vamos a comprobar las modificaciones hechas:

- Probar el www de informática:

<img width="596" height="182" alt="image" src="https://github.com/user-attachments/assets/b1a11210-4f72-445a-8e31-80da926fbae5" />

- Probar el smtp de informática:

<img width="750" height="459" alt="image" src="https://github.com/user-attachments/assets/696805be-8709-4a9e-855f-12f5650900ad" />

- Probar el dominio principal (para ver que no se rompió):

<img width="501" height="205" alt="image" src="https://github.com/user-attachments/assets/7e25f57d-1b53-4272-8bd7-0c10b178420d" />

# Opcional - Scripts para crear subdominios.

Vamos a dividir este apartado en tres subapartados, y cambiarle ligeramente el orden: primero vamos a ver que es el $INCLUDE, luego vamos a hacer un script en bash y por último lo intentaremos en python. 

## La directiva $INCLUDE

La directiva $INCLUDE nos permite separar el archivo de la zona principal de los archivos que describen los subdominios. Tomando como referencia nuestro ejemplo, vamos a tener el archivo de zona "marisma.intranet" por un lado, y el archivo de zona del subdominio "informatica.marisma.intranet" por otro, pero en el archivo de zona principal, le vamos a decir que lea el archivo del subdominio y lo incluya, tratándolo como si estuviera dentro. 

## Script en bash

~~~
#!/bin/bash

# Pide subdominio e ip al usuario por teclado
read -p "Introduce el nombre del subdominio (ej: ventas): " SUBDOMINIO
read -p "Introduce la IP para este subdominio: " IP

ARCHIVO_MAIN="/etc/bind/db.marisma.intranet"
ARCHIVO_SUB="/etc/bind/db.$SUBDOMINIO"

# Crea el archivo .db con lo básico, los 3 hosts y lo guarda en el fichero del subdominio
echo "; Configuración para $SUBDOMINIO" | sudo tee $ARCHIVO_SUB
echo "www.$SUBDOMINIO   IN   A   $IP" | sudo tee -a $ARCHIVO_SUB
echo "ftp.$SUBDOMINIO   IN   A   $IP" | sudo tee -a $ARCHIVO_SUB
echo "smtp.$SUBDOMINIO  IN   A   $IP" | sudo tee -a $ARCHIVO_SUB

# Añade el INCLUDE al archivo principal comprobando si ya existe
if grep -q "$ARCHIVO_SUB" "$ARCHIVO_MAIN"; then
    echo "El subdominio ya estaba incluido en el archivo principal."
else
    echo "\$INCLUDE $ARCHIVO_SUB" | sudo tee -a $ARCHIVO_MAIN
    echo "Incluido nuevo archivo en la zona principal."
fi

# Reinicia BIND y comprueba
echo "Reiniciando BIND9..."
sudo systemctl restart named
sudo systemctl status named --no-pager
~~~

Captura de su funcionamiento:

<img width="884" height="613" alt="image" src="https://github.com/user-attachments/assets/6513f7e2-eb7d-4da2-8495-767d197f3f77" />

Captura de la creación del archivo db.alumnos:

<img width="455" height="125" alt="image" src="https://github.com/user-attachments/assets/3d5bfabf-fb20-4e6b-b57a-08c07804be56" />

Y vemos que desde el cliente resuelve este subdominio:

<img width="553" height="200" alt="image" src="https://github.com/user-attachments/assets/748c59cc-c590-4aba-8f58-bf7979bb8e37" />


## Script en python



