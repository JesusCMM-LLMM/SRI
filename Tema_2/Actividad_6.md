# Master DNS
 Partiendo de servidor 1 (192.168.197.99) y servidor 2 (192.168.197.89)

 El servidor 1 será el máster y ahí es donde haremos el gruso de la configuración. Primero, en named.conf.options vamos a modificar la línea de la recursión:

 <img width="402" height="145" alt="image" src="https://github.com/user-attachments/assets/f005a09d-3f75-4232-b4fb-6dd8148f65e8" />

Después vamos a editarr el named.conf.local para indicarle que es el máster de la zona marisma.intranet y de la inversa. Lo dejaremos así:

<img width="806" height="298" alt="image" src="https://github.com/user-attachments/assets/2cf77fac-a8a4-49d1-95db-947050640ffb" />

El siguiente paso es crear el archivo de zona directa. Aquí definiremos los nombres que pide el ejercicio (ns1, ftp1, mail1, www, etc.). Vamos a hacer una copia de la plantilla vacía y la modificaremos:

<img width="860" height="546" alt="image" src="https://github.com/user-attachments/assets/6c87c141-f9f2-4b2f-8d6b-b92f4f1b8662" />

Ahora creremos el archivo de la zona inversa. Lo mismo, copiamos uno vacío y lo editamos:

<img width="843" height="381" alt="image" src="https://github.com/user-attachments/assets/73e5c58a-e477-4600-a45c-6aab73f24f29" />

Vamos a comprobar que la sintaxis de todos nuestros archivos están bien. Usaremos named-checkconf y named-checkzone pasandole el nombre de los archivos recién creados:

<img width="840" height="85" alt="image" src="https://github.com/user-attachments/assets/395f36fb-3c2f-4178-9d22-6e8b22021e02" />

Una vez comprobado que todo está OK, reiniciamos:

<img width="800" height="467" alt="image" src="https://github.com/user-attachments/assets/924f4a67-9679-4e42-b4c4-6992fc3d43bd" />

Ahora nos iremos al segundo servidor, cuyya IP termina en .89. Vamos a configurarlo simplemente editando el resolve.conf, añadiendo el nameserver con la IP del servidor máster y diciendole que busque la zona marisma.intranet:

<img width="313" height="95" alt="image" src="https://github.com/user-attachments/assets/83172931-fecc-4463-995b-e69a7cdf94a0" />

Y ahora hacemos las comprobaciones:

- Probar registro A:

  <img width="473" height="181" alt="image" src="https://github.com/user-attachments/assets/9ca51c8d-0afc-45d0-9fbd-b0a24791ac59" />

- Probar registro NS:

  <img width="685" height="472" alt="image" src="https://github.com/user-attachments/assets/94b1963b-0d40-4fd1-9294-cf470ee281b9" />

- Probar registro MX:

  <img width="738" height="503" alt="image" src="https://github.com/user-attachments/assets/6afd80e4-e7ea-43ae-883d-abcdd9f6ade6" />

- Probar registro SOA:

<img width="1095" height="416" alt="image" src="https://github.com/user-attachments/assets/4d5857bd-f338-40e9-84a0-1655d560526f" />

- Probar resolución inversa:

<img width="732" height="485" alt="image" src="https://github.com/user-attachments/assets/8c1506b6-d9c4-4473-b741-bd9653338009" />

