# Simulacro_Redes2

Link repo: https://github.com/Dinastino/Simulacro_Redes2.git

## Pregunta 1: Cálculo de Ruta Más Corta
**a)**  Explica brevemente el funcionamiento del Algoritmo de Dijkstra para encontrar la ruta más corta entre dos nodos en un grafo ponderado.

- 

**b)**  Describe el método de Enrutamiento por Inundación (Flooding) y discute sus ventajas y desventajas comparándolo con Dijkstra.

- El enrutamiento por inundación es un método en el que cada nodo recibe un paquete y lo reenvía a todos sus vecinos (excepto al que se lo envió). El paquete sigue propagándose hasta que llega al destino o hasta que se agota un campo como el TTL (Time to Live).

--- 
## Pregunta 2: Cálculo de Direcciones de Broadcast y Subredes
**a)** Para la subred 172.29.152.0 con máscara 255.255.248.0, determina la dirección de broadcast. Explica el proceso de conversión de la máscara a binario y cómo se obtiene el resultado.
- Para la subred 172.29.152.0 la mascara 255.255.248.0 significa que la traducción a binario seria 11111111.11111111.11111000.00000000 lo que deja una mascara de /21, 19 bits para la red y 13 bits para direccionamiento es decir que los primeros 21 bits son estaticos para la red. Dado que los ultimos tres bits del trecer octeto son parte del rango de hosts se cuentan es decir el rango de broadcast qque es el ultimo son 1 seria la 111.11111111 que seria la 172.29.152 + 4 + 2 + 1.255 => ***172.29.159.255 que es la dirección del broadcast***.

$$\text{Bits de red: }11111111.11111111.11111-\text{Bits de hosts: }111.11111111$$
$$\text{Dirección de broadcast: }172.29.159.255$$


**b)** Dado el bloque 172.18.26.0/23, calcula la dirección de broadcast y justifica el proceso.

- Dado el bloque 172.18.26.0 con mascara de red /23 -> 11111111.11111111.11111110.0000000. sacando que tienes 9 bits para el rango de hosts, para sacar el broadcast se saca la dirección de host final que en este caso si le sumas el bit restante a tercer octeto y llenas el cuarto daría 172.18.27.255/23 como direccion de broadcast.

$$\text{Bits de red: }11111111.11111111.1111111-\text{Bits de hosts: }1.11111111$$
$$\text{Dirección de broadcast: }172.18.27.255$$


---
## Pregunta 3: Última Dirección Válida y Rango de Hosts
**a)** Con la subred 172.30.67.192 y máscara 255.255.255.192, determina cuál es la última dirección de host válida (excluyendo la dirección de broadcast).
- Con mascara de red 255.255.255.192 se quedan 6 bits para host es decir los ultimos seis bits del ultimo octeto. Para calcularlo rapidamente cojes el 255 que es el rango de direcciones maximas del cuarto octeto, los ocho bits, y le restas la mascara de red, los dos bits de mascara,:
$$255 - 192 = 63$$

Se quita el ultimo bit dado que es el del broad cast y le sumas 62 al 192 = ***172.20.67.254***

**b)** Para el host 172.22.53.199 con máscara 255.255.252.0, determina el rango de direcciones válidas (primera y última dirección de host) de la subred.

---
## Pregunta 4: Capacidad y Segmentación de Subredes

**a)** Calcula el número de equipos (hosts) que pueden conectarse en la red 172.26.0.0 con máscara 255.255.255.192.
- En una red 172.26.0.0 con mascara /26 aunque haya dos posiciones vacias no se pueden utilizar dada la mascara de red. Se utilizan los ultimos 6 bits lo que daria una dirección final de 172.26.0.62.  

**b)** Dado el host 172.18.171.190/23, identifica a qué subred pertenece, explicando cómo se determina el bloque correspondiente.

- Dado el host 172.18.171.190/23. El prefijo /23 indica que los primeros 23 bits son de red, dejando 9 bits para host. Esto significa que la subred agrupa dos bloques contiguos de direcciones de clase C (cada uno de 256 direcciones). Para determinar a qué bloque pertenece el host, observamos el tercer octeto (171). Como el bloque /23 cubre de 2 en 2 en el tercer octeto (porque 256 - 254 = 2), buscamos el múltiplo de 2 más cercano hacia abajo: 170. Por lo tanto, el host 172.18.171.190 pertenece a la subred 172.18.170.0/23,  hasta 172.18.171.255.

---

## Pregunta 5: Número de Subredes Necesarias
Explica cómo se determina el número de subredes disponibles utilizando la fórmula:

$$\text{Nº de subredes} = 2^s$$

Donde s es el número de bits prestados al identificador de subred. Aplica este concepto a un escenario en el que se requieren al menos 4 subredes para segmentar una red.

- Para determinar el número de subredes disponibles al dividir una red, se utiliza la fórmula $( 2^s \)$, donde **s** representa la cantidad de **bits prestados** del campo de host para ser usados como identificador de subred. Al tomar bits originalmente destinados a los hosts y usarlos para crear más redes, se generan múltiples subredes dentro de la red original. Por ejemplo, si se necesitan al menos **4 subredes**, se debe buscar el valor mínimo de **s** tal que $( 2^s \geq 4 \)$; en este caso, $( s = 2 \)$, porque $( 2^2 = 4 \)$. Esto significa que debemos prestar 2 bits del campo de host. Aplicado a una red como 192.168.1.0/24, al usar una nueva máscara /26 (es decir, 2 bits adicionales para red), obtenemos 4 subredes posibles, cada una con 64 direcciones (62 válidas para hosts).


## Pregunta 6: Comparación entre TCP y UDP
**a)** Compara TCP y UDP en términos de:

1. Necesidad de establecer conexión
2. Fiabilidad y control de errores
3. Control de flujo y congestión
3. Velocidad de transmisión
    - **b)** Menciona dos ejemplos de aplicaciones en las que se prefiera usar UDP y justifica la elección.


-  1. Necesidad de establecer conexion
    - En TCP se necesita establecer una conexion previa, un tubo/pipe entre los dos ordenadores, un *three way handshake* entre las dos maquinas.
    - En UDP dado que es un protocolo no orientado a conexión no se necesitaria establecer esa conexión previa y se podría empezar mandando datos desde un principio
-  2. Fiabilidad y control de errores
    - En cuando a fiabilidad y control de errores TCP es un protoclo que se asegura no solo que se envien todos los paquetes sino que también requiere un confirmacion de envio por parte del receptor para poder parar el proceso y asegurarse de que todos los paquetes han llegado a su destino. En cambio UDP solo envia, no espera confirmacion y tampoco se asegura de que lleguen todos, dado a esto es posible que se pierdan paquetes UDP por el camino.
-  3. Control de flujo y congestión
    - TCP implementa varios mecanismos de control de flujo para asegurar que el emisor no envíe datos más rápido de lo que el receptor puede procesar como ventana deslizante, ACKS y el control de flujo basado en ventana cero. Porotro lado UDP no controla el flujo de información.
-  4. Velocidad de transmisión
    - TCP es un protocolo mas lento dado que empieza con un saludo a tres bandas, necesita confiramciones y controla el flujo para no abrumar al receptor, por eso es mas adecuado para datos criticos. UDP es un protocolo mucho mas rápido dado que solo se ocupa de enviar no confirma la llegada ni controla el fluja para evitar sobrecargas pero esto significa que existe el riesgo de perdida de datos.ç
    - **b)** Menciona dos ejemplos de aplicaciones en las que se prefiera usar UDP y justifica la elección.
      - Aplicaciones de straming por ejemplo porque se prioriza la velocidad y se puede permitir una ligera perdida que no afecta a la calidad en total
      - Videojuegos en linea que necesitan conectividad en todo momento/latencia minima y para los que tcp con su confirmacion constante no serviria.
     
  

