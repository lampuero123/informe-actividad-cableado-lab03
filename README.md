# Laboratorio 03: Cableado Estructurado

## 1. Portada

- **Curso:** Redes y Comunicación de Datos
- **Docente:** Richart Escobedo
- **Laboratorio:** Laboratorio 03 – Cableado Estructurado
- **Grupo:** [COMPLETAR]
- **Integrantes:**       -Tiago Pilco Cerdan 
                         -Santiago Echegaray Cárcamo 
                         -Valentino Pinto Herrera
                         -Luis Ampuero Gonzales
- **Fecha:** 23 de septiembre de 2026

---

## 2. Objetivos

**Objetivo general**

Armar y comprobar un enlace de red con cable de par trenzado, aplicando procedimientos de cableado.

**Objetivos específicos**

- Reconocer los componentes que se usan en una instalación de cableado estructurado.
- Comprobar la continuidad de los conductores con un tester.
- Detectar y corregir errores de conexión.
- Terminar un cable en un Keystone.
- Verificar la conectividad entre equipos.

---

## 3. Materiales y herramientas

**Materiales**

- 4 m de cable UTP Cat 5e / Cat 6
- 8 conectores RJ-45
- 1 Keystone RJ-45
- 1 m de cable para la terminación del Keystone

**Herramientas**

- Crimpadora RJ-45
- Ponchadora tipo 110
- Pelacables y alicate de corte
- Tester de cable de red

---

## 4. Fundamento teórico

Cableado estructurado es un sistema organizado de cables, conectores, puntos de red, etc. Lo que buscamos es que la infraestructura esté ordenada, que pueda crecer, y tambien que se pueda administrar y sea fácil de mantener.

**Componentes que vimos en el laboratorio:**

- **Cable UTP:** es el medio físico, formado por pares de conductores trenzados.
- **RJ-45:** es el conector con el que se termina el cable.
- **Patch cord:** es un cable flexible para conectar los dispositivos.
- **Keystone:** es un módulo donde se termina un cable de red.
- **Faceplate:** es la placa donde se instala el Keystone.
- **Patch panel:** es donde se organizan las terminaciones del cableado.
- **Switch:** es el que interconecta los dispositivos de una LAN.
- **Tester:** es el que comprueba la continuidad y que los conductores lleguen al pin correcto.

**Cable UTP.** Trae cuatro pares: blanco/naranja–naranja, blanco/verde–verde, blanco/azul–azul y blanco/marrón–marrón. Los pares van trenzados.

**Normas T568A y T568B.** Definen el orden de los ocho conductores dentro del RJ-45:

| Pin | T568A | T568B |
|:---:|-------|-------|
| 1 | Blanco/Verde | Blanco/Naranja |
| 2 | Verde | Naranja |
| 3 | Blanco/Naranja | Blanco/Verde |
| 4 | Azul | Azul |
| 5 | Blanco/Azul | Blanco/Azul |
| 6 | Naranja | Verde |
| 7 | Blanco/Marrón | Blanco/Marrón |
| 8 | Marrón | Marrón |

**Cable directo y cable cruzado.** El directo usa la misma norma en los dos extremos T568B–T568B o T568A–T568A. El cruzado usa una norma distinta en cada extremo (T568A–T568B).

---

## 5. Procedimiento

**Cable directo (T568B en ambos extremos)**

1. Cortamos unos 1 m de cable UTP.
2. Quitamos entre 2 y 3 cm de la cubierta exterior.
3. Separamos los pares con cuidado, sin destrenzar más de lo necesario.
4. Ordenamos los ocho conductores según T568B: blanco/naranja, naranja, blanco/verde, azul, blanco/azul, verde, blanco/marrón, marrón.
5. Los alineamos y revisamos el orden otra vez antes de seguir.
6. Cortamos las puntas para que todos quedaran parejos.
7. Los metimos en el RJ-45 hasta el fondo, comprobando que la cubierta entrara en la zona de sujeción.
8. Crimpamos el conector.
9. Repetimos todo en el otro extremo, también con T568B.

**Cable cruzado**

Es el mismo procedimiento, pero un extremo se arma con T568A y el otro con T568B.

**Verificación**

Primero revisamos a simple vista: los ocho conductores presentes, el orden de los colores, que llegaran hasta la punta del conector y que la cubierta estuviera sujeta. Después conectamos cada extremo al tester y observamos la secuencia de luces. En un cable directo bien hecho debe verse 1→1, 2→2, hasta 8→8.

**Terminación en Keystone**

1. Cortamos el cable a la longitud necesaria y quitamos la cubierta.
2. Identificamos los pares y seguimos el esquema de colores que indica el fabricante del Keystone.
3. Colocamos cada conductor en su posición y lo ponchamos con la herramienta tipo 110, que también corta los sobrantes.
4. Instalamos el Keystone en el faceplate.

**Punto de red y prueba de conectividad**

El punto de red se arma así: PC → patch cord → Keystone → cable UTP → patch panel → patch cord → switch. Para comprobar que funcionaba usamos estos comandos en Linux:

```bash
ip addr                       # interfaces y dirección IP
ip link                       # estado del enlace
ping <IP_DEL_OTRO_EQUIPO>     # conectividad con otro equipo
```

---

## 6. Resultados

### Cable directo

![Figura 1. Cable directo](images/1_directo.png)

En la foto se ve que los dos conectores tienen los colores en el mismo orden y en la misma posición (naranja, azul y verde). Como ambos extremos siguen la misma norma, es un cable directo.

### Cable cruzado

![Figura 2. Cable cruzado](images/2_cruzado.png)

Aquí el orden de los colores cambia de un extremo al otro: en uno los hilos verdes quedan arriba y los naranjas abajo, y en el otro pasa al revés. Eso es lo que pasa cuando un extremo está en T568A y el otro en T568B, y es lo que hace que sea un cable cruzado (se intercambian los pines 1 y 2 con los pines 3 y 6).

### Keystone

![Figura 4. Keystone](images/4_keystone.png)

Es un módulo Keystone RJ-45 azul, de la marca Dixon, con sus 8 contactos dorados en el puerto frontal. Los conductores se ponchan en la parte de atrás siguiendo los colores del fabricante, y después el módulo se encaja en el faceplate.

### Prueba con el tester

| Pin | Esperado | Resultado |
|:---:|:--------:|-----------|
| 1 | 1 → 1 | [COMPLETAR] |
| 2 | 2 → 2 | [COMPLETAR] |
| 3 | 3 → 3 | [COMPLETAR] |
| 4 | 4 → 4 | [COMPLETAR] |
| 5 | 5 → 5 | [COMPLETAR] |
| 6 | 6 → 6 | [COMPLETAR] |
| 7 | 7 → 7 | [COMPLETAR] |
| 8 | 8 → 8 | [COMPLETAR] |

Resultado general: cable aprobado / rechazado [COMPLETAR]

### Prueba de conectividad

| Parámetro | Resultado |
|-----------|-----------|
| Equipo 1 | [COMPLETAR] |
| Equipo 2 | [COMPLETAR] |
| Interfaz de red | [COMPLETAR] |
| Dirección IP | [COMPLETAR] |
| Máscara | [COMPLETAR] |
| Gateway | [COMPLETAR] |
| Estado del enlace | [COMPLETAR] |
| Resultado del ping | [COMPLETAR] |
| Pérdida de paquetes | [COMPLETAR] |

---

## 7. Evidencias

- **Evidencia 1:** materiales utilizados. [COMPLETAR]
- **Evidencia 2:** cable UTP antes de prepararlo. [COMPLETAR]
- **Evidencia 3:** conductores ordenados según T568B. [COMPLETAR]
- **Evidencia 4:** conector RJ-45 terminado. Ver Figuras 1 y 2.
- **Evidencia 5:** prueba con el tester. [COMPLETAR]
- **Evidencia 6:** punto de red implementado. Ver Figura 4 (Keystone). [COMPLETAR foto del punto de red completo]
- **Evidencia 7:** captura de `ip addr`. [COMPLETAR]
- **Evidencia 8:** captura de `ping <IP>`. [COMPLETAR]
- **Evidencia 9:** diagnóstico y corrección de una falla. Ver Figura 3 y el apartado 8.

---

## 8. Diagnóstico de fallas

![Figura 3. Cable con falla](images/3_erroneo.png)

| Elemento | Resultado |
|----------|-----------|
| Falla detectada | A simple vista, este cable amarillo no es un cable Ethernet válido: un extremo tiene un conector más angosto, parecido a un RJ11/RJ12 de teléfono, y el otro tiene el conector deteriorado, con la pestaña de sujeción dañada. [CONFIRMAR] |
| Pin afectado | [COMPLETAR según el tester] |
| Posible causa | Conector de tipo equivocado, conector dañado o mal crimpado, o un cable que no es para red. |
| Solución aplicada | Cortar los extremos, volver a poner conectores RJ-45 con T568B y probar otra vez. |
| Resultado posterior | [COMPLETAR] |

---

## 9. Respuestas a las preguntas

**1. ¿Cuál es la función del cableado estructurado?**
Darle a la red una base ordenada, que pueda crecer y que sea fácil de administrar y mantener, sin depender de los equipos que se conecten.

**2. ¿Cuál es la diferencia entre T568A y T568B?**
Solo cambia la posición de los pares verde y naranja: los pines 1, 2, 3 y 6 se intercambian. Los pines 4, 5, 7 y 8 son iguales en las dos normas.

**3. ¿Qué diferencia existe entre un cable directo y uno cruzado?**
El directo usa la misma norma en los dos extremos. El cruzado usa una distinta en cada extremo, con lo que se intercambian los pares de transmisión y recepción.

**4. ¿Por qué es importante mantener el orden de los conductores?**
Porque cada par tiene que quedar en los pines que le corresponden. Si el orden está mal, se separan los pares, aparece diafonía, baja la velocidad y hasta puede no haber comunicación.

**5. ¿Qué ocurre si un conductor está abierto?**
Ese pin no tiene continuidad, así que en el tester no se enciende su luz. El enlace puede fallar o funcionar más lento.

**6. ¿Qué información proporciona un tester de cableado?**
Muestra si hay continuidad y si cada pin de un extremo llega al pin correcto del otro. Así se detectan conductores abiertos, en corto o cruzados.

**7. ¿Cuál es la función de un patch panel?**
Ordenar y concentrar las terminaciones del cableado, y permitir conectar cada punto de red al switch con patch cords cortos.

**8. ¿Cuál es la diferencia entre un patch cord y un cable de instalación?**
El patch cord es corto y flexible, y ya trae su conector en cada extremo para conectar equipos. El cable de instalación es el que se tiende de forma permanente y se termina en un Keystone o en el patch panel.

**9. ¿Por qué no se debe retirar excesivamente el trenzado de los pares?**
Porque el trenzado es lo que protege la señal de interferencias y diafonía. Si se destrenza de más, esa protección se pierde y el cable rinde peor.

**10. ¿Qué factores pueden provocar problemas de conectividad en un cable UTP?**
Un mal crimpado, el orden de colores equivocado, conductores abiertos o en corto, conectores dañados o de otro tipo, una longitud excesiva, componentes de mala calidad, cable dañado, interferencias o una mala configuración de los equipos.

**Pregunta final: ¿por qué el cableado estructurado es parte fundamental de la infraestructura de una red?**
Porque de él depende que la red funcione bien y siga funcionando cuando crezca. Un cableado planificado, con normas, etiquetado y probado, es fácil de mantener y evita fallas difíciles de encontrar. Un montón de cables conectados sin criterio, en cambio, da problemas todo el tiempo.

---

## 10. Conclusiones

1. Comparando las Figuras 1 y 2 vimos que lo único que distingue a un cable directo de uno cruzado es el orden de los colores en cada extremo. El cable es el mismo; lo que cambia es cómo se arma.
2. El cable de la Figura 3 nos mostró que un cable puede parecer de red y no serlo, o tener el conector dañado. Por eso conviene revisarlo a simple vista y luego comprobarlo con el tester antes de usarlo.
3. Al terminar el cable en el Keystone (Figura 4) vimos cómo se pasa de un cable suelto a un punto de red fijo, que se conecta con patch cords cortos. Eso deja la instalación más ordenada y más fácil de mantener.

---

## 11. Recomendaciones

- Revisar el orden de los colores antes de meter los conductores en el RJ-45 y otra vez antes de crimpar.
- Cortar los conductores parejos y comprobar que lleguen hasta el fondo del conector.
- Asegurarse de que la cubierta quede dentro de la zona de sujeción, para que el conector no se suelte al jalar el cable.
- No destrenzar los pares más de lo necesario.
- Probar siempre el cable con el tester antes de usarlo.
- Etiquetar los cables y los puntos de red.
- No mezclar conectores de teléfono con conectores de red.
