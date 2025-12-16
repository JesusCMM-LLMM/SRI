# 1. Creación de VPC

Para esta práctica necesitamos crear una VPC que tenga dos subredes públicas y dos privadas. Voy a eliminar todo lo hecho en AWS hasta ahora como prueba, así puedo empezar con todo de cero. 
Nos vamos al apartado de VPC y le damos a 'VPC y más'. Le vamos a asignar la ip que vemos en la captura (10.2.0.0/16) y no vamos a poner bloque IPv6. 

<img width="1754" height="753" alt="image" src="https://github.com/user-attachments/assets/bad26a14-18ea-41cf-9643-6140eef3ce49" />

Personalizamos las zonas de disponibilidad en us-east-1a y us-east-1b:

<img width="484" height="313" alt="image" src="https://github.com/user-attachments/assets/303c3d10-68e8-44e6-8350-b36f7caea6b8" />

Ponemos 2 subredes privadas y 2 subredes públicas con estos bloques CIDR:

<img width="487" height="566" alt="image" src="https://github.com/user-attachments/assets/ad23abd4-b564-4040-942f-7ac38e97f2c2" />

Dejamos el NAT y la puerta de enlace en 'ninguna' y creamos:

<img width="495" height="520" alt="image" src="https://github.com/user-attachments/assets/8aebf269-5ed1-4e24-aa0a-2adfb1309f77" />

Una vez creado, ya podemos seguir: 

<img width="1618" height="648" alt="image" src="https://github.com/user-attachments/assets/987bc4ff-7365-48b1-a0b5-b42fa6c7d733" />

Y vemos el mapa de recursos:

<img width="1628" height="496" alt="image" src="https://github.com/user-attachments/assets/ac943a6d-b7a3-45ca-971c-1699b3f39c3b" />


# 2. Creación de instancias

Vamos a lanzar una instancia Debian dentro de la subred pública 1. Nos vamos al apartado de EC2 y le damos a 'Lanzar instancia': 

<img width="1094" height="712" alt="image" src="https://github.com/user-attachments/assets/f90bf60d-6dc8-4805-84e1-6499ec696cbf" />

La llamamos como nos pide la práctica, dejamos la instancia como tipo t3.micro, pero en 'Configuraciones de red', le damos a editar para seleccionar la VPC que hemos creado:

<img width="1070" height="314" alt="image" src="https://github.com/user-attachments/assets/ec8785b7-3bd7-4be4-bbe0-71bf2e2976b8" />

Habilitamos la IP pública de forma automatica, y vamos a proceder a crear un grupo de seguridad: 

<img width="1076" height="743" alt="image" src="https://github.com/user-attachments/assets/df8bac0d-9de6-4927-814a-20b1f1b284d0" />

Con esto nos aseguramos la conexión SSH y que el puerto 80 esté abierto. Finalmanta la lanzamos y se crea:

<img width="754" height="288" alt="image" src="https://github.com/user-attachments/assets/a6da2243-7048-433e-bf57-0f578dab902d" />

<img width="1607" height="592" alt="image" src="https://github.com/user-attachments/assets/53a4fb05-2de1-4381-a857-72eab7bed466" />

Me voy a conectar por SSH:

<img width="1111" height="400" alt="image" src="https://github.com/user-attachments/assets/b536e6fb-0115-451e-ad34-39a54c259204" />

# 3. Apache y PHP

Hemos puesto los paquetes del repositorio apt al día,m y ahora vamos a instalar apache:

<img width="920" height="386" alt="image" src="https://github.com/user-attachments/assets/fb93361e-db4d-46aa-a47c-ec0f376046f9" />

Lo iniciamos y lo dejamos configurado para que se inicie cada vez que se lance la instancia:

<img width="1001" height="102" alt="image" src="https://github.com/user-attachments/assets/ebca2cb8-d3fb-4b8d-a245-0c89d00a872e" />

En el navegador, uso la ip pública de mi instancia que me da AWS y entro para comprobar que apache esté corriendo: 

<img width="1238" height="759" alt="image" src="https://github.com/user-attachments/assets/63934b63-3958-4028-aacf-64bcab4644a9" />

Vamos a instalar PHP como módulo de apache:

<img width="1067" height="318" alt="image" src="https://github.com/user-attachments/assets/11fe02a0-7e57-4984-871c-3f1ab2b78bcc" />

<img width="630" height="132" alt="image" src="https://github.com/user-attachments/assets/42d401d4-f9e6-4208-83db-05aef1839278" />

Y también instalamos mysql, y después comprobamos que esté dentro de los módulos de PHP:

<img width="595" height="261" alt="image" src="https://github.com/user-attachments/assets/8b2d646a-a25d-445a-8ccf-4200dd5c9106" />

<img width="409" height="95" alt="image" src="https://github.com/user-attachments/assets/999dae56-2e12-4434-8a50-e9e2d59e7deb" />

# 4. Creación de la base de datos.

Vamos al servicio RDS y creamos una base de datos del tipo MySQL:

<img width="1646" height="578" alt="image" src="https://github.com/user-attachments/assets/bf2d3255-52b6-47ad-9f5e-41164c234fbf" />

Le damos el nombre requerido y el usuario será admin con contraseña 'administrador':

<img width="1621" height="674" alt="image" src="https://github.com/user-attachments/assets/3301ab7f-6b90-4f4b-b3e6-e1c167641f4d" />

Esta es nuestra configuración: 

<img width="1190" height="380" alt="image" src="https://github.com/user-attachments/assets/8c7939a2-c674-46b7-a92d-7d2b283d11fa" />

Y este nuestro almacenamiento: 

<img width="1147" height="307" alt="image" src="https://github.com/user-attachments/assets/92048a86-2549-4039-84f8-e55cc6a73a90" />

En conectividad nos aseguramos de poner la VPC que hemos creado para esta práctica: 

<img width="1617" height="446" alt="image" src="https://github.com/user-attachments/assets/2f0a5951-51a4-4452-a931-c307346cf08b" />

<img width="1621" height="519" alt="image" src="https://github.com/user-attachments/assets/63078a19-1583-4880-8e11-a509ee795827" />

En configuración adicional: 

<img width="1183" height="368" alt="image" src="https://github.com/user-attachments/assets/f063bf9c-fb09-49ae-acbd-1ce1f9f3e745" />

Y ya le damos a crear. 

<img width="1327" height="286" alt="image" src="https://github.com/user-attachments/assets/a4fdc2f1-ef6f-471b-8443-b96ecc5cce2d" />

Una vez creada la base de datos,vamos a establecer la conexión con la instancia con el asistente que RDS nos proporciona. Establecerá los permisos necesarios en los grupos de seguridad de la instancia y la BD sin mayor complicación.

<img width="1425" height="304" alt="image" src="https://github.com/user-attachments/assets/3894c948-54ef-470e-a9b7-dfedfb7b53ec" />

Simplemente le damos a conectar: 

<img width="1362" height="401" alt="image" src="https://github.com/user-attachments/assets/8d3fe0db-519c-4528-84df-8ca50ff19567" />

Y esperamos hasta que se completa: 

<img width="1613" height="294" alt="image" src="https://github.com/user-attachments/assets/484b4061-e35c-4cbc-be43-59c9c06fcee0" />


# 5. Elastic File System.

Nos vamos al apartado de EFS para crear el sistema de almacenamiento externo que vamos a conectar a la instancia y que más tarde conectaremos a wordpress.

<img width="818" height="829" alt="image" src="https://github.com/user-attachments/assets/222cb4c2-3198-4c1e-a1bc-a240c5f4da20" />

Comprobamos que está bien creado:

<img width="1578" height="338" alt="image" src="https://github.com/user-attachments/assets/53e10c2d-a038-4398-abef-68fadf3e2ff8" />

Ahora, en los grupos de seguridad de la instancia EC2 que tenemos, vamos a editar el grupo de seguridad para permitir el acceso de la instancia al EFS. 
Ahora le damos a asociar y usamos la opción del DNS: 

<img width="1794" height="513" alt="image" src="https://github.com/user-attachments/assets/9e454a75-50c6-43d2-8723-1c57fc80f4f8" />






























