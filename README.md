# Informe de Laboratorio 03: Cableado Estructurado

> **Nota:** las marcas **[COMPLETAR]** indican datos que solo tú tienes (nombres, resultados del tester, capturas de red). Búscalas con Ctrl+F antes de entregar.

---

## 1. Portada

| Campo | Información |
|-------|-------------|
| **Curso** | Redes y Comunicación de Datos |
| **Docente** | Richart Escobedo |
| **Laboratorio** | Laboratorio 03: Cableado Estructurado |
| **Grupo / Tema** | **[COMPLETAR]** |
| **Integrantes** | **[COMPLETAR]** |
| **Fecha** | 23 de septiembre de 2026 |

---

## 2. Objetivos

### 2.1 Objetivo general

Implementar y comprobar un enlace básico de red mediante cableado de par trenzado, aplicando procedimientos de cableado estructurado y estándares de terminación RJ-45.

### 2.2 Objetivos específicos

1. Reconocer los componentes de una instalación de cableado estructurado.
2. Identificar los pares y conductores de un cable UTP.
3. Aplicar la distribución de colores T568A y T568B.
4. Elaborar un cable directo y un cable cruzado con conectores RJ-45.
5. Comprobar la continuidad de los conductores con un tester.
6. Detectar y corregir errores de conexión.
7. Realizar la terminación de un cable en un Keystone.
8. Comprobar la conectividad entre equipos.

---

## 3. Materiales y herramientas

### Materiales

| Material | Cantidad |
|----------|:--------:|
| Cable UTP Cat 5e / Cat 6 | 4 m |
| Conectores RJ-45 | 8 |
| Keystone RJ-45 | 1 |
| Cable para terminación del Keystone | 1 m |

### Herramientas

| Herramienta | Uso |
|-------------|-----|
| Crimpadora RJ-45 | Fijar los conectores RJ-45 al cable |
| Ponchadora tipo 110 | Terminar los conductores en el Keystone |
| Pelacables / alicate de corte | Retirar la cubierta y cortar los conductores |
| Tester de cable de red | Comprobar continuidad y orden de los pines |

---

## 4. Fundamento teórico

### 4.1 Cableado estructurado

Es un sistema organizado de cables, conectores, puntos de red, patch panels, patch cords, racks y dispositivos de red. Busca una infraestructura **ordenada, escalable, administrable y fácil de mantener**, independiente de los equipos específicos que se conecten.

### 4.2 Componentes

| Componente | Descripción |
|------------|-------------|
| Cable UTP | Medio físico formado por pares de conductores trenzados |
| RJ-45 | Conector utilizado para terminar el cable |
| Patch cord | Cable flexible para conectar dispositivos |
| Keystone | Módulo donde se termina un cable de red |
| Faceplate | Placa donde se instala el Keystone |
| Patch panel | Elemento donde se organizan las terminaciones del cableado |
| Switch | Interconecta dispositivos dentro de una LAN |
| Tester | Comprueba continuidad y correspondencia de los conductores |

### 4.3 Cable UTP

UTP significa *Unshielded Twisted Pair* (Par Trenzado No Blindado). Contiene cuatro pares:

| Par | Colores |
|:---:|---------|
| 1 | Blanco/Naranja – Naranja |
| 2 | Blanco/Verde – Verde |
| 3 | Blanco/Azul – Azul |
| 4 | Blanco/Marrón – Marrón |

El trenzado reduce las interferencias electromagnéticas, la diafonía y el ruido.

| Categoría | Característica general |
|-----------|------------------------|
| Cat 5e | Ethernet hasta 1 Gb/s en condiciones apropiadas |
| Cat 6 | Mejores características frente a interferencias |
| Cat 6A | Diseñada para 10 Gb/s hasta 100 m en condiciones especificadas |

La velocidad real también depende de la longitud, los componentes, la instalación y los equipos.

### 4.4 Normas T568A y T568B

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

### 4.5 Cable directo y cable cruzado

```text
Directo:   T568B ───────── T568B     (o T568A ───────── T568A)
Cruzado:   T568A ───────── T568B
```

Muchos equipos modernos soportan **Auto-MDI/MDI-X**, por lo que detectan automáticamente el tipo de conexión y el cable directo basta para la mayoría de casos actuales.

---

## 5. Procedimiento

### 5.1 Cable directo (T568B – T568B)

1. Cortar aproximadamente 1 m de cable UTP.
2. Retirar 2 a 3 cm de la cubierta exterior.
3. Separar los pares con cuidado, sin destrenzar más de lo necesario.
4. Ordenar los conductores según T568B: Blanco/Naranja, Naranja, Blanco/Verde, Azul, Blanco/Azul, Verde, Blanco/Marrón, Marrón.
5. Alinear los ocho conductores y verificar de nuevo el orden.
6. Cortar los conductores de forma uniforme.
7. Introducirlos en el RJ-45 hasta el extremo y comprobar que la cubierta entre en la zona de sujeción.
8. Crimpar.
9. Repetir en el otro extremo con T568B.

### 5.2 Cable cruzado (T568A – T568B)

Mismo procedimiento, pero un extremo se termina con T568A y el otro con T568B.

### 5.3 Verificación

1. **Inspección visual:** ocho conductores presentes, orden correcto, conductores hasta el extremo del RJ-45, cubierta sujeta y conector sin daños.
2. **Tester:** se conecta cada extremo al tester y se observa la secuencia de los indicadores. Un cable directo correcto debe mostrar 1→1, 2→2, … 8→8.

### 5.4 Terminación en Keystone

1. Cortar el cable a la longitud necesaria y retirar la cubierta.
2. Identificar los pares y seguir el esquema de colores indicado por el fabricante del Keystone.
3. Colocar cada conductor en su posición y ponchar con la herramienta tipo 110, que también corta los excedentes.
4. Colocar el Keystone en el faceplate.

### 5.5 Punto de red y prueba de conectividad

```text
PC
 │  Patch Cord
Keystone
 │  Cable UTP
Patch Panel
 │  Patch Cord
Switch
```

Comandos usados en Linux para comprobar el enlace:

```bash
ip addr                  # interfaces y dirección IP
ip link                  # estado del enlace
ping <IP_DEL_OTRO_EQUIPO>
```

---

## 6. Resultados

### 6.1 Cable directo

![Figura 1. Cable directo](images/1_directo.png)

*Figura 1. Cable directo.*

En ambos conectores RJ-45 transparentes se aprecia el mismo orden de colores en la misma posición (naranja, azul y verde visibles). Los dos extremos siguen la misma norma (T568B), por lo que el cable es **directo**.

### 6.2 Cable cruzado

![Figura 2. Cable cruzado](images/2_cruzado.png)

*Figura 2. Cable cruzado.*

Al comparar ambos extremos, el orden de los colores es distinto: en uno los hilos verdes quedan arriba y los naranjas abajo, y en el otro ocurre lo contrario. Esto corresponde a un extremo en T568A y el otro en T568B, es decir, un cable **cruzado**. Se intercambian los pines 1 y 2 con los pines 3 y 6.

### 6.3 Keystone

![Figura 4. Keystone](images/4_keystone.png)

*Figura 4. Módulo Keystone RJ-45.*

Se muestra el módulo Keystone RJ-45 (de color azul, marca Dixon) con sus 8 contactos dorados en el puerto frontal, junto a un cable UTP con conector RJ-45. Los conductores se terminan en la parte posterior con la ponchadora tipo 110, siguiendo el esquema de colores del fabricante, y luego el módulo se instala en el faceplate.

### 6.4 Resultado del tester

| Pin | Esperado | Resultado obtenido |
|:---:|:--------:|--------------------|
| 1 | 1 → 1 | **[COMPLETAR]** |
| 2 | 2 → 2 | **[COMPLETAR]** |
| 3 | 3 → 3 | **[COMPLETAR]** |
| 4 | 4 → 4 | **[COMPLETAR]** |
| 5 | 5 → 5 | **[COMPLETAR]** |
| 6 | 6 → 6 | **[COMPLETAR]** |
| 7 | 7 → 7 | **[COMPLETAR]** |
| 8 | 8 → 8 | **[COMPLETAR]** |

**Resultado general del cable directo:** aprobado / rechazado **[COMPLETAR]**

### 6.5 Prueba de conectividad

| Parámetro | Resultado |
|-----------|-----------|
| Equipo 1 | **[COMPLETAR]** |
| Equipo 2 | **[COMPLETAR]** |
| Interfaz de red | **[COMPLETAR]** |
| Dirección IP | **[COMPLETAR]** |
| Máscara | **[COMPLETAR]** |
| Gateway | **[COMPLETAR]** |
| Estado del enlace | **[COMPLETAR]** |
| Resultado del ping | **[COMPLETAR]** |
| Pérdida de paquetes | **[COMPLETAR]** |

---

## 7. Evidencias

| N.º | Evidencia | Estado |
|:---:|-----------|--------|
| 1 | Fotografía de los materiales utilizados | **[COMPLETAR]** |
| 2 | Fotografía del cable UTP antes de la preparación | **[COMPLETAR]** |
| 3 | Fotografía de los conductores ordenados según T568B | **[COMPLETAR]** |
| 4 | Fotografía del conector RJ-45 terminado | Figuras 1 y 2 |
| 5 | Fotografía de la prueba con el tester | **[COMPLETAR]** |
| 6 | Fotografía del punto de red implementado | Figura 4 (Keystone); punto de red completo **[COMPLETAR]** |
| 7 | Captura de `ip addr` | **[COMPLETAR]** |
| 8 | Captura de `ping <IP>` | **[COMPLETAR]** |
| 9 | Fotografía o registro del diagnóstico y corrección de una falla | Figura 3 y sección 8 |

---

## 8. Diagnóstico de fallas

![Figura 3. Cable erróneo](images/3_erroneo.png)

*Figura 3. Cable con falla.*

| Elemento | Resultado |
|----------|-----------|
| **Falla detectada** | Por inspección visual, el cable amarillo no cumple el formato RJ-45 de 8 pines: un extremo tiene un conector más angosto, de aspecto RJ11/RJ12 (telefonía), y el otro extremo tiene el conector deteriorado, con la pestaña de sujeción dañada. **[CONFIRMAR / AJUSTAR]** |
| **Pin afectado** | **[COMPLETAR con lo que indicó el tester]** |
| **Posible causa** | Conector de tipo incorrecto, conector dañado o mal crimpado, cable no diseñado para Ethernet |
| **Solución aplicada** | Cortar los extremos, volver a ponchar con conectores RJ-45 siguiendo T568B y repetir la prueba |
| **Resultado posterior** | **[COMPLETAR]** |

---

## 9. Respuestas a las preguntas

**1. ¿Cuál es la función del cableado estructurado?**
Proveer una infraestructura de red ordenada, escalable, administrable y fácil de mantener, independiente de los equipos y servicios que se conecten.

**2. ¿Cuál es la diferencia entre T568A y T568B?**
Solo cambia el orden de los pares verde y naranja: los pines 1, 2, 3 y 6 se intercambian. Los pines 4, 5, 7 y 8 son iguales en ambas normas.

**3. ¿Qué diferencia existe entre un cable directo y uno cruzado?**
El directo usa la misma norma en ambos extremos (A–A o B–B); el cruzado usa una distinta en cada extremo (A–B), intercambiando los pares de transmisión y recepción.

**4. ¿Por qué es importante mantener el orden de los conductores?**
Porque cada par trenzado debe quedar en los pines que le corresponden. Un orden incorrecto separa los pares, genera diafonía y errores, reduce la velocidad y puede impedir la comunicación.

**5. ¿Qué ocurre si un conductor está abierto?**
No hay continuidad en ese pin: el tester no enciende el indicador correspondiente y el enlace puede fallar o funcionar a menor velocidad.

**6. ¿Qué información proporciona un tester de cableado?**
Continuidad, correspondencia pin a pin entre ambos extremos y detección de conductores abiertos, cortocircuitos o cruzados.

**7. ¿Cuál es la función de un patch panel?**
Organizar y concentrar las terminaciones del cableado horizontal, y permitir conectar cada punto de red al switch mediante patch cords cortos.

**8. ¿Cuál es la diferencia entre un patch cord y un cable de instalación?**
El patch cord es corto, flexible y viene con conectores en ambos extremos para conectar equipos. El cable de instalación es el tendido permanente y se termina en Keystone o patch panel.

**9. ¿Por qué no se debe retirar excesivamente el trenzado de los pares?**
Porque el trenzado protege contra interferencias y diafonía. Destrenzar de más en la terminación degrada la calidad de la señal, especialmente en categorías altas.

**10. ¿Qué factores pueden provocar problemas de conectividad en un cable UTP?**
Mal crimpado, orden incorrecto de colores, conductores abiertos o en corto, conectores dañados o de tipo incorrecto, longitud excesiva, componentes de baja calidad, cable dañado, interferencias y configuración incorrecta de los equipos.

**Pregunta final: ¿Por qué el cableado estructurado es parte fundamental de la infraestructura de red?**
Porque de él depende la calidad, la estabilidad y la escalabilidad de todas las comunicaciones. Un cableado planificado, normalizado, etiquetado y probado facilita el mantenimiento, permite crecer sin rehacer la instalación y evita fallas difíciles de detectar. Un conjunto de cables conectados sin criterio es fuente constante de problemas.

---

## 10. Conclusiones

1. **Conclusión 1:** al comparar los cables de las Figuras 1 y 2 se comprobó que la diferencia entre un cable directo y uno cruzado está únicamente en el orden de los colores en cada extremo (T568B–T568B frente a T568A–T568B), no en el cable en sí.
2. **Conclusión 2:** el cable de la Figura 3 mostró que un cable puede parecer un cable de red y no serlo, o tener conectores dañados. La inspección visual detecta estos errores y el tester confirma el pin o par afectado antes de usar el cable.
3. **Conclusión 3:** la terminación en Keystone (Figura 4) permite pasar de un cable suelto a un punto de red permanente, conectado con patch cords cortos, lo que hace la instalación más ordenada y fácil de mantener.
4. **Conclusión 4:** **[COMPLETAR con una conclusión sobre tus resultados del tester y de la prueba de conectividad]**

---

## 11. Recomendaciones

- Verificar el orden de los colores antes de introducir los conductores en el RJ-45 y antes de crimpar.
- Cortar los conductores de forma uniforme y comprobar que lleguen hasta el extremo del conector.
- Asegurar que la cubierta exterior entre en la zona de sujeción para que el conector no ceda al jalar el cable.
- No destrenzar los pares más de lo necesario.
- Probar siempre el cable con el tester antes de usarlo en un equipo.
- Etiquetar los cables y puntos de red para facilitar el mantenimiento.
- Usar conectores y cable de la categoría adecuada (Cat 5e o superior) y no mezclar conectores de telefonía con conectores de red.
