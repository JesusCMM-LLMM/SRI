# Punto de partida e instalación de bind

- DNS Server 192.168.197.99/24 (Ubuntu server con lightdm)
- Cliente 

Lo primero que vamos a hacer es instalar bind9 mediante apt: 

<img width="615" height="158" alt="image" src="https://github.com/user-attachments/assets/e5485940-5e6d-4b65-9563-fccd73679add" />

# Caching & Forwarding

Para configurarlo primero como un servidor de caché de DNS, nos vamos a la carpeta donde están los archivos de configuración en /etc/bind y el fichero que vamos a modificar es el named.conf.options:

<img width="601" height="338" alt="image" src="https://github.com/user-attachments/assets/3ab2c7cc-fd9f-402e-b55c-0f0d44419986" />

Aquí lo que vamos a declarar es una lista de control de entrada con el rango de IP que vamos a permitir que escuchen las peticiones que hagamos a nuestro servidor DNS. Vamos a añadir este bloque de ACL arriba del bloque options y a especificar los clientes en los que confiamos: 

<img width="366" height="158" alt="image" src="https://github.com/user-attachments/assets/94c64fee-a60e-4abe-8445-e7972dd72db0" />

Ahora que ya tenemos estos clientes definidos, dentro de options vamos a permitir las consultas:

<img width="409" height="287" alt="image" src="https://github.com/user-attachments/assets/dd327996-31a7-4112-8177-803c89a03319" />

Guardamos, y vamos a comprobar la sintaxis de nuestro archivo de configuración con sudo named-checkconf:

<img width="498" height="75" alt="image" src="https://github.com/user-attachments/assets/bf9f1922-d3e6-47f6-85c2-c42768a8db52" />

Y reiniciamos bind para aplicar los cambios con sudo systemctl restart bind9. En los logs vemos que está escuchando la IP de nuestro servidor:

<img width="1086" height="191" alt="image" src="https://github.com/user-attachments/assets/edeb9714-038f-4a22-a3bf-fcd0092f162d" />

# Forwarding

Ahora vamos a configurarlo además como un servidor forwarding. Para esto, en el mismo archivo que hemos modificado, simplemente descomentamos el bloque de forwarders y añadimos otras opciones: 

<img width="565" height="360" alt="image" src="https://github.com/user-attachments/assets/edea9e70-712a-44f0-bf3a-1aa4ebd68f61" />

Comprobamos la sintaxis y vemos este error: 

<img width="661" height="69" alt="image" src="https://github.com/user-attachments/assets/b01fdbfe-c208-4131-8331-1fbee6b960cd" />

Simplemente eliminamos esa línea y la de dnssec-validation auto porque está repetida y comprobamos de nuevo. Una vez todo esté correcto, vamos a reiniciar el servicio. 

# Comprobación en un cliente: 

Después de configurar el archivo /etc/resolve.conf de la siguiente manera:

<img width="286" height="117" alt="image" src="https://github.com/user-attachments/assets/91e4a33f-ce24-4a57-a89d-35b41994a339" />

Ya podemos empezar a comprobar con el cliente. 

<img width="781" height="188" alt="image" src="https://github.com/user-attachments/assets/d70d90e3-50d6-4cfc-ac3b-eb73bb6afd4d" />

<img width="647" height="719" alt="image" src="https://github.com/user-attachments/assets/1229184c-b0bb-44aa-be0c-dfd9d783ba2d" />

Y la comprobación inversa:

<img width="836" height="350" alt="image" src="https://github.com/user-attachments/assets/62b613ac-d9ff-4485-a5cc-18ae02558884" />

También vamos a comprobar los logs que dejamos corriendo en el servidor:

<img width="1250" height="322" alt="image" src="https://github.com/user-attachments/assets/229414c0-1169-4b56-ad7c-a3d9d6b4f1bf" />

Y con esto habríamos terminado. 







