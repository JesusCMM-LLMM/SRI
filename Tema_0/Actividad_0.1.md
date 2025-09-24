# Actividad 0.1- HTTP Introduction

## ¿Quién, dónde y cuándo se crea el primer servidor web?

El primer servidor web fue creado por Tim Berners Lee en el CERn, en 1990.

## ¿Qué pila de protocolos usa http?
	
La pila de protocolos de HTTP, permite la comunicación en red. Digamos que es el “camino” que debe recorrer una petición HTTP pasando por las capas del modelo TCP/IP. 

## ¿Componentes de una URL?
	
Las partes más esenciales de una URL (Uniform Resource Locator) son:
    1. Protocolo / esquema: por ejemplo http, https (el mecanismo de transferencia)
    2. Host / dominio: por ejemplo www.ejemplo.com
    3. Puerto (opcional, si no es el estándar): por ejemplo :80, :443
    4. Ruta (path): indica la ubicación del recurso en el servidor, por ejemplo /carpeta/pagina.html
    5. Consulta / query string (opcional): parte después de ?, para parámetros, ej: ?id=123&orden=asc
    6. Fragmento (opcional): después de #, para referirse a una sección dentro del recurso, ej: #seccion2

## ¿Pasos en la recuperación de una página web mediante HTTP?
	
Aquí un flujo típico de lo que sucede cuando un navegador recupera una página:
    1. Usuario o navegador introduce una URL / hace clic en enlace.
    2. Se resuelve el nombre de dominio (DNS lookup): el navegador pregunta qué dirección IP corresponde al dominio.
    3. Se establece una conexión TCP al servidor web (en el puerto apropiado, por ejemplo 80 para HTTP o 443 para HTTPS).
    4. Se envía la petición HTTP al servidor, p.ej. un mensaje GET /ruta HTTP/1.1 con encabezados.
    5. El servidor procesa la petición: determina qué recurso corresponde, puede implicar lectura de archivos estáticos o ejecutar código (en el caso dinámico), etc.
    6. Se construye la respuesta HTTP: línea de estado, encabezados (headers), tipo de contenido, longitud, etc., y finalmente el cuerpo (body) con el recurso (HTML, imagen, etc.).
    7. La respuesta viaja de vuelta al cliente, por la conexión TCP.
    8. El navegador interpreta la respuesta: si es HTML, lo renderiza; si incluye referencias a recursos secundarios (CSS, JS, imágenes), hace peticiones adicionales para esos.
    9. Una vez terminado todo, opcionalmente se cierra la conexión TCP, o se mantiene abierta si se usa HTTP persistente.

## Diferencia entre páginas dinámicas y estáticas
	
    • Páginas estáticas: el contenido que el servidor entrega es siempre el mismo para esa URL, porque el archivo ya existe en disco (HTML, imágenes, CSS). No cambia según el usuario, o si cambia, el webmaster lo edita.
    • Páginas dinámicas: el contenido se genera bajo demanda cuando llega la petición. Puede depender de datos en una base de datos, de la sesión del usuario, de parámetros, etc. Por ejemplo, un foro, un blog con comentarios, una tienda online.

## Request. Métodos principales
	
    • GET: solicitar un recurso, no debe tener efectos secundarios (idealmente).
    • HEAD: como GET pero sólo obtiene los encabezados, no el cuerpo del recurso.
    • POST: enviar datos al servidor (por ejemplo, enviar formulario), puede producir efectos secundarios.
    • PUT: reemplazar completamente un recurso existente o crearlo si no existe.
    • DELETE: eliminar un recurso.
    • También: OPTIONS, PATCH, TRACE, CONNECT dependiendo del uso.


## Response. Códigos
	
Listado de códigos: 

    • 1xx	-> Informativos – la petición se recibió, pero el servidor sigue procesando
    • 2xx	-> Éxito – la petición fue atendida correctamente
    • 3xx	-> Redirecciones – el cliente debe hacer algo adicional para completar la petición (seguir locaciones, etc.)
    • 4xx	-> Errores del cliente – la petición fue mala o no tiene permisos, etc.
    • 5xx	-> Errores del servidor – la petición estaba bien formada, pero el servidor falló al procesarla


## Content type. Tipos principales

El Content‑Type es un encabezado 
de la respuesta HTTP que indica qué tipo de contenido se está enviando (tipo mime). Algunos de los más comunes:
    • text/html → páginas HTML
    • text/plain → texto plano
    • text/css → hojas de estilo CSS
    • application/javascript o text/javascript → scripts JS
    • application/json → datos en formato JSON
    • image/jpeg, image/png, image/gif → imágenes
    • application/xml → XML (aunque cada vez menos usado excepto APIs antiguas)




