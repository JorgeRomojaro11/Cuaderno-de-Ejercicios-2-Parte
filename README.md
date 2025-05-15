# Cuaderno-de-Ejercicios-2-Parte

https://github.com/JorgeRomojaro11/Cuaderno-de-Ejercicios-2-Parte.git


1. Explicar sobre el siguiente grafo de red los conceptos de circuito virtual entre el nodo 10 y el 6, y datagrama entre el nodo 3 y el 6. Asumir arcos bidireccionales.
Circuito Virtual (CV) entre nodo 10 y 6:

Se establece una ruta fija antes de transmitir los datos, por ejemplo: 10 → 5 → 7 → 6.

Cada nodo intermedio configura su tabla con una entrada de circuito virtual.

Todos los paquetes siguen esa misma ruta.

La red mantiene el estado de la conexión.

Datagrama entre nodo 3 y 6:

No hay ruta establecida previamente.

Cada paquete puede seguir una ruta diferente.

Por ejemplo:

Paquete 1: 3 → 10 → 5 → 7 → 6

Paquete 2: 3 → 8 → 10 → 5 → 6

Los nodos no guardan estado.

Se usa el mejor esfuerzo (best-effort).



2. Partiendo de la anterior red, generar las tablas de cada uno de los nodos de un circuito virtual entre los nodos 3 y 4. Tener en cuenta que los CV creados del anterior ejercicio siguen presentes. Asumir arcos bidireccionales.
Ruta sugerida del circuito virtual: 3 → 10 → 5 → 7 → 4

Tablas de encaminamiento para el nuevo circuito virtual (CV-2):

Nodo 3:

Entrada: -

Salida: CV-2 hacia 10

Nodo 10:

Entrada: CV-2

Salida: CV-2 hacia 5

Nodo 5:

Entrada: CV-2

Salida: CV-2 hacia 7

Nodo 7:

Entrada: CV-2

Salida: CV-2 hacia 4

Nodo 4:

Entrada: CV-2

Salida: -

Nota: el CV anterior (entre 10 y 6) sigue activo.



3. Aplicar los algoritmos indicados en los siguientes grafos, tomando como partida el nodo 5. Indicar iteración a iteración lo que ocurre. Asumir arcos bidireccionales.
a) Algoritmo de Dijkstra:

Paso 0:

Nodo origen: 5. Coste = 0.

Nodos vecinos: 4, 6, 7, 10 (con coste correspondiente)

Tabla inicializada.

Iteración 1:

Elegir nodo con menor coste: 6.

Actualizar costes de sus vecinos si se mejora el camino.

Iteración 2:

Elegir siguiente nodo con menor coste: 4.

Continuar hasta alcanzar todos los nodos.

Se construye una tabla de costes mínimos desde el nodo 5.

b) Algoritmo de inundación hasta el nodo 6. Contar el total de paquetes generados.

Iteración 1:

Nodo 5 envía a: 4, 6, 7, 10 → 4 paquetes

Iteración 2:

Nodo 4 reenvía a 1 y 7

Nodo 7 reenvía a 2 y 6 (si no recibido)

Nodo 10 reenvía a 3 y 8

En este caso, el nodo 6 es alcanzado en la primera iteración, así que como mínimo se generan 4 paquetes.



4. Diseñar las tablas de rutado jerárquico de la siguiente red:
Dividir la red en regiones jerárquicas, por ejemplo:

Nivel 0: routers locales

Nivel 1: routers interregionales

Nivel 2: router principal

Cada router mantiene:

Rutas locales directas

Ruta por defecto hacia su "padre" jerárquico

Ejemplo:
Router R1

Destino: T1 → Directo
Destino: T2 → Directo
Destino: T3 → R2
Destino: T4 → R5

Reducción del tamaño de las tablas debido a agregación por región.



5. En un sistema con las siguientes características, indicar las máscaras utilizadas, la primera y última dirección de los equipos, y los elementos/dispositivos necesarios:
7900 profesionales con datos sensibles.

54 subredes para sensorización (100 sensores por subred).

1290 tomas Ethernet.

75000 clientes externos que deberán tener acceso a Internet por wifi.

Switches de máximo 24 bocas.

Cálculos:

7900 profesionales → /19 (8192 IPs)

Primera IP: X.X.X.1

Última IP: X.X.X.8190

Switches: ceil(7900 / 24) = 330 switches

54 subredes × 100 sensores → usar /25 (128 IPs por subred)

1290 tomas Ethernet → /21 (2048 IPs)

75000 clientes WiFi → /15 (131072 IPs)

Dispositivos requeridos: switches, routers intermedios, gateways, servidores DHCP.



6. Calcular la eficiencia en un sistema basado en UDP/IP desde un mensaje de la capa de aplicación de 1000000 bytes, sabiendo que la longitud máxima del campo de datos es:
UDP: 65527 bytes. Cabecera de 8 bytes.

IP: 65535 bytes. Cabecera de 4 bytes.

Ethernet: 1500 bytes. Cabecera de 8 bytes.

Paquetes necesarios:
1000000 / 65527 ≈ 16

Tamaño total transmitido por paquete:
65527 + 8 + 4 + 8 = 65547 bytes

Eficiencia:
E = 1000000 / (16 × 65547) ≈ 0.9538 → 95.38%



7. Con los datos del ejercicio anterior, calcular la eficiencia de un sistema RTP/UDP, con cabecera RTP de 12 bytes y 65535 bytes de datos.
Tamaño total por paquete:
65535 (datos) + 12 (RTP) + 8 (UDP) + 4 (IP) + 8 (Ethernet) = 65567 bytes

Eficiencia:
E = 65535 / 65567 ≈ 0.9995 → 99.95%



8. Realizar el pseudocódigo de un cliente y servidor UDP/TCP que devuelva la hora de una región determinada.
Cliente UDP:

Crear socket UDP

Enviar mensaje “HORA” al servidor

Esperar respuesta

Imprimir hora

Servidor UDP:

Crear socket y hacer bind

Escuchar mensajes

Si mensaje es “HORA”, responder con la hora actual

Repetir indefinidamente



9. Indicar el procedimiento a seguir mediante el protocolo DNS para obtener la dirección IP de la siguiente URL: iuj.ac.jp
El cliente envía solicitud DNS al servidor local.

Si el servidor local no tiene la IP en caché:

Consulta al servidor raíz DNS.

El servidor raíz responde con IP del servidor .jp.

El servidor .jp responde con IP de ac.jp.

El servidor ac.jp responde con IP de iuj.ac.jp.

La respuesta se almacena en caché y se devuelve al cliente.



10. Indicar el intercambio de mensajes completo que se produce desde que se introduce la URL www.twitch.tv hasta que empieza a visualizarse una transmisión en directo.
El usuario introduce la URL.

El navegador realiza una consulta DNS.

Se obtiene la IP del servidor de Twitch.

Se establece una conexión TCP al puerto 443 (HTTPS).

Se realiza la negociación TLS (cifrado seguro).

El navegador envía una petición HTTP GET.

El servidor responde con la página HTML.

El navegador descarga recursos (JS, CSS, media).

El usuario selecciona una transmisión.

Se inicia la descarga por streaming (HLS/WebRTC).

El reproductor comienza a mostrar la transmisión en tiempo real.

