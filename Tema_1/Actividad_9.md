# Ejercicios adicionales de autenticación básica

## 1. Crea cinco usuarios: usuario1, usuario2, usuario3, usuario4, usuario5.

<img width="528" height="142" alt="image" src="https://github.com/user-attachments/assets/dd84ecd7-7596-4d7b-a5fd-34946288ed0b" />

<img width="474" height="111" alt="image" src="https://github.com/user-attachments/assets/ba60ee90-2fc2-47b2-8ca6-7b4184c28a3d" />

Y hacemos lo mismo hasta el usuario5.

<img width="541" height="171" alt="image" src="https://github.com/user-attachments/assets/9e6147a4-a9f8-4885-b01a-1cb5d30522bf" />


## 2. Crea dos grupos de usuarios, el primero formado por usuario1 y usuario2; y el segundo por el resto de usuarios.

<img width="325" height="56" alt="image" src="https://github.com/user-attachments/assets/e9521343-8a46-4e12-b065-a972f626d26e" />

<img width="533" height="95" alt="image" src="https://github.com/user-attachments/assets/eac87e3b-4c64-458b-a1de-5645926e1783" />


## 3. Crea un directorio llamado privado1 que permita el acceso a todos los usuarios.

<img width="420" height="115" alt="image" src="https://github.com/user-attachments/assets/585bdf4e-8a9e-4e9d-b714-024e1df82b5e" />

Ahora, en /etc/apache2/apache2.conf vamos a poner lo siguiente:

<img width="452" height="154" alt="image" src="https://github.com/user-attachments/assets/bed0bd23-a94e-4f18-b400-bd02940c4831" />

Lo comprobamos:

<img width="510" height="147" alt="image" src="https://github.com/user-attachments/assets/0a17ef28-45a7-47f5-a7d9-4622ae60f998" />


## 4. Crea un directorio llamado privado2 que permita el acceso sólo a los usuarios del grupo1.

Ahora, en /etc/apache2/apache2.conf vamos a poner lo siguiente:

<img width="454" height="172" alt="image" src="https://github.com/user-attachments/assets/3da797b6-3447-41ae-b9c1-e405e148af31" />

Podemos comprobar desde el navegador que solo si eres usuario1 o usuario2 puedes acceder:

<img width="875" height="428" alt="image" src="https://github.com/user-attachments/assets/9c300cda-2cd2-4a88-8003-75d7fc2c49c3" />

Si ponemos a algun usuario del grupo2: 

<img width="967" height="306" alt="image" src="https://github.com/user-attachments/assets/8da849f3-3712-4cf5-bec5-ae4ffe789e1f" />


## 5. Esta parte es teórica, solo tenemos que mirar esa documentación.

## 6. En el directorio privado2 haz que sólo sea accesible desde el localhost, y estudia cómo se comporta la autorización si ponemos: satisfy any, satisfy all

Primero de todo, activamos el módulo:

<img width="674" height="70" alt="image" src="https://github.com/user-attachments/assets/6dde48b3-d14b-4425-b776-980071cbf155" />

La primera, con Satisfy All nos dice que debemos cumplir todas las condiciones (entrar desde localhost y que usuario y contraseña sean reconocidos)

<img width="372" height="268" alt="image" src="https://github.com/user-attachments/assets/5240c034-db88-446d-9298-961b577fdf91" />

Y en el segundo caso, con Satisfy Any, solo tiene que cumplirse uno:

<img width="391" height="270" alt="image" src="https://github.com/user-attachments/assets/5d73f876-9eba-4825-a211-20428db7647a" />
