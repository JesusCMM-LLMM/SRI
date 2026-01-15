# Caching & Forwarding

Vamos a partir de una máquina con Ubuntu Server cuya IP es 192.168.1.1/24 y una máquina Ubuntu Escritorio con IP 192.168.1.11/24. 
Lo primero que vamos a hacer es descargar bind9 y sus complementos: 

<img width="530" height="232" alt="image" src="https://github.com/user-attachments/assets/3e9ccccd-fe1f-49e3-a876-334d019ed55e" />

## Configurar como Caching DNS Server

Ahora nos vamos a la  carpeta donde están guardados los archivos de configuración: 

<img width="548" height="303" alt="image" src="https://github.com/user-attachments/assets/57c19b89-2b9b-4a2c-bf20-f35a71416f85" />

Vamos a modificar named.conf.options para otorgar permisos de acceso mediante una lista ACL:

<img width="887" height="513" alt="image" src="https://github.com/user-attachments/assets/d70559a6-7bf3-4ea4-948e-6d57e14bbe3d" />

Así está nuestro archivo, ahora vamos a crear, por encima de < options {.. >, una etiqueta acl: 

<img width="777" height="162" alt="image" src="https://github.com/user-attachments/assets/22b344bf-8903-4e67-8be3-e088452330e0" />

Donde especificamos la subred en la que vamos a permitir acceso, ya que ambas máquinas están en la misma. Una vez que tenemos esta lista permitida de clientes, vamos a añadir en options las capacidades que debe tener añadiendo estas líneas:

<img width="757" height="466" alt="image" src="https://github.com/user-attachments/assets/c422ab91-45b3-4870-a9f9-3f883fab8c0b" />

Guardamos y con esto ya tendríamos todo lo necesario para usar este Ubuntu Server como Servidor de caché DNS

## Forwarding

Como vemos en las capturas anteriores, esto es algo que tenía configurado previamente, con el DNS de nuestro router virtual y el DNS de Google. 

<img width="604" height="164" alt="image" src="https://github.com/user-attachments/assets/49cdec87-330b-4d3c-89b6-26602b9b67e2" />

Ahora solo vamos a añadirle la clausula "forward only;" y ya que estamos modificamos los valores de dnssec validation a yes: 

<img width="362" height="126" alt="image" src="https://github.com/user-attachments/assets/c6f9f73e-5909-456e-930a-3175d1285a4f" />

Y con esto ya lo tendríamos. 















