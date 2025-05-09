# Simulacro_Redes2

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

