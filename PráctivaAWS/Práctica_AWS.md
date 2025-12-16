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

Con esto nos aseguramos la conexión SSH y que el puerto 80 esté abierto. 

































