# Laboratorio 04 – Captura de paquetes: comunicación simplex, dúplex y orientada a conexión

## Grupos de 4 integrantes: (Indicar las tareas que realizó cada integrante)

| Alumno | Tarea realizada | Porcentaje |
|---|---|---|
| Apellidos y Nombres de Integrante 1 (responsable del grupo) | Levantó el entorno con Docker Compose y redactó el README. | 100% |
| Apellidos y Nombres de Integrante 2 | Ejecutó y capturó la comunicación simplex. | 100% |
| Apellidos y Nombres de Integrante 3 | Ejecutó y capturó la comunicación dúplex. | 100% |
| Apellidos y Nombres de Integrante 4 | Ejecutó y capturó la comunicación orientada a conexión. | 100% |

---

## Actividades previas

### 1. Construir la imagen y crear los contenedores

Desde la carpeta donde están `Dockerfile` y `docker-compose.yml`:

```bash
docker compose up -d --build
```

Verificar que los contenedores estén corriendo:

```bash
docker ps
```

> 📸 **Captura 1:** salida de `docker ps` con los dos contenedores activos.
> `![docker ps](capturas/01_docker_ps.png)`

Ingresar a cada contenedor (usar una terminal por cada uno):

```bash
docker exec -it rcd_lab04_container1_escobedo bash
```

```bash
docker exec -it rcd_lab04_container2_escobedo bash
```

Para eliminar los contenedores y la red creada por Compose:

```bash
docker compose down
```

### 2. Obtener las direcciones IP de los contenedores

Dentro de cada contenedor:

```bash
hostname -I
# o bien
ip -4 addr show eth0
```

| Host | Contenedor | IP |
|---|---|---|
| Emisor / Cliente | `rcd_lab04_container1_escobedo` | `<IP_C1>` (ej. 172.18.0.2) |
| Receptor / Servidor | `rcd_lab04_container2_escobedo` | `<IP_C2>` (ej. 172.18.0.3) |

> 📸 **Captura 2:** salida de `hostname -I` en ambos contenedores.

### 3. Herramientas necesarias

Si la imagen no las trae instaladas, ejecutar en **ambos** contenedores:

```bash
apt update && apt install -y tcpdump netcat-openbsd iputils-ping
```

> Para abrir el `.pcap` en Wireshark se puede copiar al host con:
> `docker cp rcd_lab04_container2_escobedo:/tmp/simplex.pcap .`

---

## Tarea: Actividades a desarrollar en laboratorio

Se usaron **dos hosts** (container1 y container2) conectados por la red virtual creada por Docker Compose, y se capturó el tráfico con `tcpdump` en el contenedor receptor.

---

## 1. Comunicación simplex

**Concepto:** la información viaja en **un solo sentido**: un host solo transmite y el otro solo recibe (por ejemplo, radio o TV). Para simularlo se usa **UDP**, sin respuesta del receptor.

**Terminal A – container2 (receptor + captura):**

```bash
# Iniciar la captura
tcpdump -i eth0 -n -nn -w /tmp/simplex.pcap udp port 5000 &

# Escuchar en UDP 5000 (solo recibe)
nc -u -l -p 5000
```

**Terminal B – container1 (emisor):**

```bash
echo "Mensaje simplex 1" | nc -u -w1 <IP_C2> 5000
echo "Mensaje simplex 2" | nc -u -w1 <IP_C2> 5000
echo "Mensaje simplex 3" | nc -u -w1 <IP_C2> 5000
```

**Detener y ver la captura (container2):**

```bash
kill %1
tcpdump -n -r /tmp/simplex.pcap
```

**Salida esperada (ejemplo):**

```
10:15:01.120 IP 172.18.0.2.41234 > 172.18.0.3.5000: UDP, length 18
10:15:03.455 IP 172.18.0.2.52310 > 172.18.0.3.5000: UDP, length 18
10:15:05.871 IP 172.18.0.2.38977 > 172.18.0.3.5000: UDP, length 18
```

> 📸 **Captura 3:** mensajes enviados desde container1 y recibidos en container2.
> 📸 **Captura 4:** salida de `tcpdump -r simplex.pcap` (o Wireshark).

**Análisis:**
- Todos los paquetes van en la misma dirección: `<IP_C1> → <IP_C2>`.
- No hay paquetes de respuesta de `<IP_C2>` hacia `<IP_C1>` (ni confirmaciones ni datos).
- UDP no establece conexión ni confirma la recepción, por lo que se comporta como un canal simplex.

---

## 2. Comunicación dúplex o bidireccional

**Concepto:** ambos hosts pueden **enviar y recibir**. Es *half-duplex* si lo hacen alternadamente (walkie-talkie) y *full-duplex* si pueden hacerlo al mismo tiempo (teléfono). Con `netcat` sobre TCP ambos extremos escriben y leen simultáneamente, es decir, full-duplex.

**Terminal A – container2 (servidor + captura):**

```bash
tcpdump -i eth0 -n -nn -w /tmp/duplex.pcap tcp port 6000 &
nc -l -p 6000
```

**Terminal B – container1 (cliente):**

```bash
nc <IP_C2> 6000
```

Una vez conectados, **escribir mensajes en ambas terminales**:

```
[container1] Hola desde container1
[container2] Hola container1, te recibo
[container1] ¿Puedes escuchar mis mensajes?
[container2] Sí, la comunicación es bidireccional
```

Finalizar con `Ctrl + C` y luego:

```bash
kill %1
tcpdump -n -r /tmp/duplex.pcap
```

**Salida esperada (ejemplo):**

```
IP 172.18.0.2.50122 > 172.18.0.3.6000: Flags [P.], length 21
IP 172.18.0.3.6000 > 172.18.0.2.50122: Flags [.],  ack 22
IP 172.18.0.3.6000 > 172.18.0.2.50122: Flags [P.], length 27
IP 172.18.0.2.50122 > 172.18.0.3.6000: Flags [.],  ack 28
```

> 📸 **Captura 5:** chat entre ambos contenedores.
> 📸 **Captura 6:** paquetes en ambas direcciones (`tcpdump` o Wireshark).

**Análisis:**
- Hay paquetes con datos (`P` = PSH) en **ambos sentidos**: `C1 → C2` y `C2 → C1`.
- Cualquiera de los extremos puede transmitir en cualquier momento sin esperar turno, por lo tanto es una comunicación **dúplex (full-duplex)**.

---

## 3. Comunicación orientada a conexión

**Concepto:** antes de transmitir datos se establece una conexión (**three-way handshake** de TCP), se garantiza la entrega con confirmaciones (ACK) y al final se cierra la conexión ordenadamente.

**Terminal A – container2 (servidor + captura):**

```bash
tcpdump -i eth0 -n -nn -S -w /tmp/conexion.pcap tcp port 7000 &
nc -l -p 7000
```

**Terminal B – container1 (cliente):**

```bash
nc <IP_C2> 7000
# escribir: "Prueba orientada a conexion" y presionar Enter
# cerrar con Ctrl + C
```

**Ver la captura:**

```bash
kill %1
tcpdump -n -r /tmp/conexion.pcap
```

**Salida esperada (ejemplo):**

```
IP 172.18.0.2.44210 > 172.18.0.3.7000: Flags [S],  seq 1000          <- 1) SYN
IP 172.18.0.3.7000 > 172.18.0.2.44210: Flags [S.], seq 5000, ack 1001 <- 2) SYN-ACK
IP 172.18.0.2.44210 > 172.18.0.3.7000: Flags [.],  ack 5001          <- 3) ACK
IP 172.18.0.2.44210 > 172.18.0.3.7000: Flags [P.], length 28          <- Datos
IP 172.18.0.3.7000 > 172.18.0.2.44210: Flags [.],  ack 1029          <- ACK de datos
IP 172.18.0.2.44210 > 172.18.0.3.7000: Flags [F.], seq 1029          <- FIN
IP 172.18.0.3.7000 > 172.18.0.2.44210: Flags [F.], seq 5001          <- FIN
IP 172.18.0.2.44210 > 172.18.0.3.7000: Flags [.],  ack 1030          <- ACK final
```

> 📸 **Captura 7:** cliente y servidor durante la conexión.
> 📸 **Captura 8:** handshake `SYN → SYN-ACK → ACK` y cierre `FIN` en Wireshark.

**Análisis de las fases:**

| Fase | Paquetes | Descripción |
|---|---|---|
| Establecimiento | `SYN`, `SYN-ACK`, `ACK` | Saludo en tres vías; ambos acuerdan números de secuencia. |
| Transferencia | `PSH-ACK`, `ACK` | Cada segmento de datos es confirmado por el receptor. |
| Cierre | `FIN`, `ACK`, `FIN`, `ACK` | Cada lado cierra su extremo de la conexión. |

---

## Cuadro comparativo

| Característica | Simplex | Dúplex | Orientada a conexión |
|---|---|---|---|
| Protocolo usado | UDP | TCP | TCP |
| Sentido de la comunicación | Un solo sentido | Ambos sentidos | Ambos sentidos |
| Handshake previo | No | Sí | Sí |
| Confirmaciones (ACK) | No | Sí | Sí |
| Paquetes de respuesta | Ninguno | Sí | Sí |
| Ejemplo real | Radio, TV | Chat, llamada | HTTP, SSH, FTP |

> Nota: TCP es orientado a conexión y por naturaleza full-duplex. En el punto 2 se destaca el intercambio simultáneo de datos en ambas direcciones y en el punto 3 el establecimiento y cierre de la conexión.

---

## Conclusiones

1. La comunicación **simplex** se evidenció con UDP: los paquetes solo circulan del emisor al receptor, sin respuesta ni confirmación.
2. La comunicación **dúplex** se evidenció con una sesión TCP donde ambos hosts enviaron datos, y en la captura se observan paquetes con datos en ambas direcciones.
3. La comunicación **orientada a conexión** se comprobó al observar el *three-way handshake*, las confirmaciones ACK y el cierre con FIN.
4. `tcpdump` y Wireshark permiten distinguir claramente el tipo de comunicación analizando la dirección de los paquetes, las banderas TCP y el protocolo de transporte.
5. Docker Compose facilita reproducir un entorno de red aislado para realizar estas pruebas de manera rápida y repetible.

---

## Estructura del repositorio

```
.
├── Dockerfile
├── docker-compose.yml
├── README.md
└── capturas/
    ├── 01_docker_ps.png
    ├── ...
    └── simplex.pcap / duplex.pcap / conexion.pcap
```
