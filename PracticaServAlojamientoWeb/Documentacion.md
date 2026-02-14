# Práctica 2º Trimestre - Servidor de Alojamiento Web

## 0. Punto de partida.

En este primer apartado vamos a crear la máquina virtual y darle una IP estática para facilitarnos la vida más adelante. Nos vamos a nuestro Proxmox y creamos una MV con Ubuntu Server 24.04 LTS:

<img width="719" height="541" alt="image" src="https://github.com/user-attachments/assets/63ba6f82-ec1f-4fbd-af81-a34c41f6e6ec" />

<img width="884" height="392" alt="image" src="https://github.com/user-attachments/assets/341ba216-3cca-4db8-b457-e91c6df37562" />

Una vez hecho esto, vamos a instalar el sistema operativo, parándonos en dos puntos clave: 

<img width="1215" height="299" alt="image" src="https://github.com/user-attachments/assets/72567571-f121-4fa9-ac75-300bbcae942c" />

El primero es en la configuración de red, donde vamos a aprovechar para ponerle una ip estática. Vamos a Edit IPv4: 

<img width="660" height="256" alt="image" src="https://github.com/user-attachments/assets/78f4773c-8805-40d9-b9dd-b4a92ab88203" />

Y lo vamos a configurar de la siguiente manera:

<img width="667" height="430" alt="image" src="https://github.com/user-attachments/assets/55d52c06-6e99-4f5e-b281-1176f52db4e0" />

- La subnet es la subred de nuestro nodo en proxmox (la he visto en la interfaz del router virtual, cogiendo solo los tres primeros octetos)
- La Address va a ser nuestra IP, yo he elegido la 192.168.193.110
- Y el gateway (puerta de enlace) es la IP del router, para tener salida a internet.

<img width="1178" height="270" alt="image" src="https://github.com/user-attachments/assets/d268eacd-06b2-45de-a578-c0082a6909bd" />

