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


