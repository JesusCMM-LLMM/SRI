# ACT 1: INSTALACIÓN DE APACHE EN UBUNTU

Lo primero que hemos hecho en una instalación limpia de Ubuntu 24.04 es actualizar el repositorio apt, mediante sudo apt update & sudo apt upgrade:

<img width="1278" height="867" alt="image" src="https://github.com/user-attachments/assets/362a3c07-7c82-4aea-ab64-83249025c294" />

Lo siguiente es instalar apache como tal:

<img width="724" height="290" alt="image" src="https://github.com/user-attachments/assets/729d2b3e-0128-4062-91db-5f2efd611839" />

Comprobamos que está habilitado accediendo a http://localhost que nos mostrará la página de prueba de apache:

<img width="1281" height="846" alt="image" src="https://github.com/user-attachments/assets/7b48e17f-6b57-46af-910a-6a3261ac7d11" />

Lo siguiente será instalar MySQL, mediante ‘sudo apt install mysql-server’: 

<img width="1039" height="324" alt="image" src="https://github.com/user-attachments/assets/eb812a3e-0e3d-4035-aa0c-9a6ae11f9103" />

Una vez instalado, ejecutaremos una secuencia preestablecida de comandos de seguridad que eliminará algunos ajustes predeterminados poco seguros y se bloqueará el acceso a su sistema de base de datos: 

<img width="987" height="456" alt="image" src="https://github.com/user-attachments/assets/ae55a167-25ee-4ebb-9e84-5b059dff3164" />

Comprobamos que podemos acceder a MySQL: 

<img width="813" height="318" alt="image" src="https://github.com/user-attachments/assets/dae9575a-2fb7-43cc-bf20-4d830de3d671" />

Por último, vamos a instalar PHP: 

<img width="813" height="172" alt="image" src="https://github.com/user-attachments/assets/eb4e18a7-1364-4296-87f5-93b9c86c05c6" />

Comprobamos que está instalado correctamente: 

<img width="703" height="118" alt="image" src="https://github.com/user-attachments/assets/3e72c8fd-7981-4f96-a046-0ce4841123da" />

Pues con esto el LAMP stack ya está completamente configurado. 

El siguiente paso es crear un host virtual para nuestro sitio web. Para ello vamos a crear una estructura de dominio dentro de /var/www/ con el nombre dom_propio. Vamos a aprovechar y cambiarle el propietario a nuestro usuario a la misma vez:

<img width="602" height="114" alt="image" src="https://github.com/user-attachments/assets/c248de1b-4eb8-4986-be11-7403bb1738a7" />

Vamos a crear un nuevo archivo en ‘sites-available’ de Apache usando nano, que servirá como archivo de configuración de nuestro dominio: 

<img width="702" height="290" alt="image" src="https://github.com/user-attachments/assets/3282dac2-93f7-479f-85d1-e0ab62268bc9" />

Ahora habilitamos el nuevo host virtual y reiniciamos apache:

<img width="529" height="113" alt="image" src="https://github.com/user-attachments/assets/9d4902a6-b787-48ac-91f9-38f0dc0b9a39" />

<img width="598" height="114" alt="image" src="https://github.com/user-attachments/assets/9d5c657d-f24a-450b-8bcc-9ac9968b84be" />

Para terminar este paso, vamos a crear un archivo index.html en el directorio de nuestro dominio para que se muestre correctamente: 

<img width="625" height="160" alt="image" src="https://github.com/user-attachments/assets/b38db263-203e-41d3-a008-188608776e0c" />

Y comprobamos que funciona:

<img width="371" height="210" alt="image" src="https://github.com/user-attachments/assets/67d24f22-22c2-4383-ad16-6bee4e1a814b" />

*He quitado el acento del <h1>

Ahora vamos a probar que nuestra nueva página web pueda procesar peticiones PHP. Para ello creamos un nuevo archivo llamado info.php dentro de la carpeta dom_propio con este código:

<img width="604" height="137" alt="image" src="https://github.com/user-attachments/assets/333fa747-3e90-42be-9ad5-694b0e9e9f5d" />

Y la probamos accediendo a http://localhost/info.php desde el navegador:

<img width="1080" height="604" alt="image" src="https://github.com/user-attachments/assets/caae819a-fc64-433a-84c3-d38ee3a49255" />

Una vez comprobado esto, eliminamos el archivo info.php de la carpeta. 

