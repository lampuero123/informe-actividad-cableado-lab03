# Laboratorio 04 - Captura de paquetes

## Grupos de 4 integrantes

| Alumno | Tarea realizada | Porcentaje |
|---|---|---|
| Apellidos y Nombres de Integrante 1 | Levantó los contenedores y redactó el README. | 100% |
| Apellidos y Nombres de Integrante 2 | Comunicación simplex. | 100% |
| Apellidos y Nombres de Integrante 3 | Comunicación dúplex. | 100% |
| Apellidos y Nombres de Integrante 4 | Comunicación orientada a conexión. | 100% |

## Creación de los hosts

Usamos dos contenedores con Docker Compose y sacamos sus IPs con `hostname -I`.

```bash
docker compose up -d --build
docker ps
docker exec -it rcd_lab04_container1_escobedo bash
docker exec -it rcd_lab04_container2_escobedo bash
```

| Contenedor | IP |
|---|---|
| container1 (emisor/cliente) | `<IP_C1>` |
| container2 (receptor/servidor) | `<IP_C2>` |

![docker ps](capturas/01_docker_ps.png)

## 1. Comunicación simplex

Usamos UDP con netcat. El container1 solo envía y el container2 solo recibe. La captura se hizo con tcpdump en el container2.

```bash
# container2
tcpdump -i eth0 -nn -w /tmp/simplex.pcap udp port 5000 &
nc -u -l -p 5000

# container1
echo "Mensaje simplex" | nc -u -w1 <IP_C2> 5000
```

![simplex](capturas/02_simplex.png)

**Resultado:** todos los paquetes van de `<IP_C1>` a `<IP_C2>`. No aparece ningún paquete de vuelta, ni respuesta ni confirmación. Por eso es simplex: la información va en un solo sentido.

## 2. Comunicación dúplex o bidireccional

Usamos TCP con netcat. Los dos contenedores escribieron mensajes y ambos los recibieron.

```bash
# container2
tcpdump -i eth0 -nn -w /tmp/duplex.pcap tcp port 6000 &
nc -l -p 6000

# container1
nc <IP_C2> 6000
```

![duplex](capturas/03_duplex.png)

**Resultado:** en la captura hay paquetes con datos (`PSH, ACK`) de `<IP_C1>` a `<IP_C2>` y también de `<IP_C2>` a `<IP_C1>`. Los dos pueden enviar y recibir al mismo tiempo, por eso es dúplex.

## 3. Comunicación orientada a conexión

Usamos TCP y revisamos cómo se establece y cierra la conexión.

```bash
# container2
tcpdump -i eth0 -nn -w /tmp/conexion.pcap tcp port 7000 &
nc -l -p 7000

# container1
nc <IP_C2> 7000
```

![conexion](capturas/04_conexion.png)

**Resultado:** se observan tres etapas:

1. **Establecimiento:** `SYN`, `SYN-ACK` y `ACK` (three-way handshake).
2. **Transferencia:** paquetes con datos y sus `ACK` de confirmación.
3. **Cierre:** `FIN` y `ACK` de ambos lados.

Es orientada a conexión porque antes de enviar datos se establece la conexión y cada envío es confirmado.

## Conclusión

Con tcpdump pudimos diferenciar los tres tipos de comunicación. En simplex el tráfico va en un solo sentido (UDP), en dúplex hay datos en ambos sentidos y en la orientada a conexión se ve el handshake, los ACK y el cierre con FIN (TCP).
