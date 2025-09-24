# Actividad 0.2- UDP y TCP

## Diferencias entre udp y tcp? (min 2:46 y 4:15)

TCP (Transmission Control Protocol) y UDP (User Datagram Protocol) son dos protocolos de la capa de transporte, pero tienen diferencias clave. TCP es un protocolo orientado a la conexión, lo que significa que establece una conexión confiable entre el emisor y el receptor antes de comenzar la transmisión de datos. Garantiza que los datos lleguen completos y en orden, lo cual lo hace más seguro, aunque más lento debido al control de errores y a los mecanismos de verificación. En cambio, UDP es un protocolo no orientado a la conexión, más rápido pero menos confiable, ya que no garantiza la entrega ni el orden de los paquetes.

## ¿Qué aplicaciones usan tcp?  http, smtp, pop, imap, ssh

Aplicaciones como HTTP (protocolo de transferencia de hipertexto), SMTP (protocolo simple de transferencia de correo), POP e IMAP (protocolos para recuperación de correos electrónicos), y SSH (protocolo seguro para acceso remoto).

## ¿Qué aplicaciones usan udp?

Aplicaciones que priorizan la velocidad y toleran cierta pérdida de datos, como las transmisiones de video en vivo, los juegos en línea, DNS (sistema de nombres de dominio) y VoIP (voz sobre IP).

## ¿Qué capa almacena el puerto?

La capa de transporte.

## ¿Qué capa almacena la dirección IP?

La capa de red.

## ¿Qué es three-way handshake?
El "three-way handshake" es un proceso de tres pasos utilizado por TCP para establecer una conexión entre dos dispositivos. Primero, el cliente envía un segmento SYN (synchronize) al servidor. Luego, el servidor responde con un segmento SYN-ACK (synchronize-acknowledge). Finalmente, el cliente envía un ACK (acknowledge) al servidor, completando así el establecimiento de la conexión. Este mecanismo garantiza que ambas partes estén listas para la transmisión de datos y sincronizadas correctamente.