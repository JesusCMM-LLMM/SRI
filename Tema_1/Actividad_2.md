# Ejercicios archivos de configuracón.

## Apache utilizará el puerto 81 además del 80

Añadimos la línea 'Listen 81' al archivo ports.conf

<img width="814" height="182" alt="image" src="https://github.com/user-attachments/assets/834e453f-a8c4-4a6a-a722-3858fd2921c3" />

Y comprobamos que también esté escuchando ese puerto:

<img width="981" height="274" alt="image" src="https://github.com/user-attachments/assets/eac1203e-4d81-4dd2-8dcd-1560f3896cf0" />


## Añadir el dominio “marisma.intranet” en el fichero “hosts”

Nos vamos a /etc/hosts y añadimos esta línea:

<img width="1217" height="114" alt="image" src="https://github.com/user-attachments/assets/35c2744c-1751-4a85-bbbe-1041fa49d6dd" />

Con esto podemos acceder a localhost con 'marisma.intranet'

<img width="579" height="203" alt="image" src="https://github.com/user-attachments/assets/1675123f-ec25-4744-a846-df90ba0ebdcb" />


## Cambia la directiva “ServerTokens” para mostrar el nombre del producto.

Modificamos la línea ServerTokens de Full a Prod

<img width="813" height="295" alt="image" src="https://github.com/user-attachments/assets/a31d904b-c535-4d3d-8377-ff15d3da54bf" />

Y así logramos que solo nos muestre el nombre del producto y no la versión ni el OS

<img width="623" height="241" alt="image" src="https://github.com/user-attachments/assets/1b34c232-36da-419a-878f-6c7aa2b2f49f" />

## Comprueba si se visualiza el pie de página en las páginas generadas por Apache (por ejemplo, en las páginas de error). Cambia el valor de la directiva "ServerSignature" y comprueba que funciona correctamente.

Introducimos una dirección incorrecta y no da el error 404 con el pie de página completo

<img width="550" height="255" alt="image" src="https://github.com/user-attachments/assets/8b0d6b2a-7e7f-4f31-8ee3-d5b89bbb12a2" />

Y tras modificar la directiva, ya no se muestra el pie de página de antes. 

<img width="519" height="241" alt="image" src="https://github.com/user-attachments/assets/2a8b8795-2422-4dc8-a790-af8e54d93938" />


## Crea un directorio “prueba” y otro directorio “prueba2”. Incluye un par de páginas en cada una de ellas.

<img width="540" height="131" alt="image" src="https://github.com/user-attachments/assets/1f572c7a-be70-47b0-985e-e5e699fe4642" />

Ambas carpetas creadas con un index.html de prueba en cada una, vamos a comprobar que funcionan:

<img width="1180" height="486" alt="image" src="https://github.com/user-attachments/assets/93ecbfcf-5c8f-4c16-9dac-79506bef8704" />

<img width="1194" height="467" alt="image" src="https://github.com/user-attachments/assets/ce31e0e2-9a50-45f4-a3ad-4f01cc0373f3" />

## Redirecciona el contenido de la carpeta “prueba” hacia “prueba2”

Dentro de /etc/apache2/ vamos al archivo apache2.conf y añadimos la línea siguiente:

<img width="317" height="73" alt="image" src="https://github.com/user-attachments/assets/323993e2-8e85-4f5e-915b-7b16ab0bbd6e" />

Y funciona correctamente.


## Es posible redireccionar tan solo una página en lugar de toda la carpeta. Pruébalo.

Sí, es posible. De hecho si en prueba2 ponemos otro archivo html y le indicamos que la redireccion sea de /prueba a /prueba2/test.html, lo podemos comprobar. Esta es la línea del código:

<img width="411" height="74" alt="image" src="https://github.com/user-attachments/assets/6b32819b-b473-40f0-8de2-27b3d27ebcfc" />

<img width="984" height="383" alt="image" src="https://github.com/user-attachments/assets/53ecd13c-1219-4628-a39c-244b2e27a66c" />


## Usa la directiva userdir



## Usa la directiva alias para redireccionar a una carpeta dentro del directorio de usuario.

Vamos al archivo alias.conf dentro de mods-available y añadimos el alias

<img width="446" height="188" alt="image" src="https://github.com/user-attachments/assets/308880b1-d521-4fa7-ac67-addbe89e1a51" />

y vemos que funciona

<img width="524" height="145" alt="image" src="https://github.com/user-attachments/assets/5de225c5-08c6-4c77-bba4-09f19f657e0c" />


## ¿Para qué sirve la directiva Options y dónde aparece? Comprueba si apache indexa los directorios. Si es así, ¿cómo lo desactivamos?

La directiva options sirve para configurar el comportamiento dentro de un directorio. Sí indexa el contenido. 
Lo desativamos en apache2.conf y vemos que en var/www quitando la línea 'Indexes'

<img width="583" height="331" alt="image" src="https://github.com/user-attachments/assets/7fa927e1-cd8d-4bf5-ad61-0a4830d974c6" />



