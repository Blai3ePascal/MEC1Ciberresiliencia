# Resiliencia Protocol – Guardián de Activos

![MIT License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 🇪🇸 Sección en español

### 1. Descripción del código

#### 1.1. Estructura general

El archivo implementa una **single page application (SPA)** desarrollada en **HTML5** y **JavaScript** que utiliza un elemento `<canvas>` de **HTML** para representar un juego tipo **tower defense** orientado a la **ciberresiliencia**.

La lógica principal se encapsula en una función de tipo **IIFE**, que inicializa el **game state**, configura la **interfaz de usuario (UI)**, genera la topología de la red, crea las rondas de ataque (**rounds**) y ejecuta continuamente el bucle de animación sobre el `canvas`.

El aspecto visual se define mediante **CSS**, utilizando **variables de tema (theme variables)** para ofrecer distintos estilos (por ejemplo, temas oscuros o de alto contraste) que el usuario puede cambiar desde la propia interfaz.

#### 1.2. Interfaz de usuario

El diseño se organiza en varias zonas principales:

- **Top bar**  
  En la barra superior se muestran:
  - El título del ejercicio (por ejemplo, “Resiliencia Protocol”).
  - La **round** actual y el número total de rondas.
  - Los recursos de la partida (créditos disponibles e integridad global del sistema).
  - Las métricas del modelo **ACIDA**:
    - Autenticación  
    - Confidencialidad  
    - Integridad  
    - Disponibilidad  
    - Trazabilidad / Accountability  

- **Threat intelligence panel**  
  Panel lateral que muestra, para la ronda actual:
  - Tipos de ataques previstos: **DDoS**, **APT**, **ransomware**.
  - Nivel aproximado de cada amenaza, que crece con las rondas.

- **Panel de log**  
  Área donde se van registrando, en tiempo real, los eventos relevantes del sistema:
  - Despliegue de defensas (por ejemplo, colocación de un **firewall**).
  - Inicio y fin de cada **wave**.
  - Éxitos o fracasos de las defensas.
  - Daño sufrido por los activos.

- **Zona de juego (canvas)**  
  El `canvas` representa una **topología de red** formada por:
  - Un **Core Router** central.
  - Varios **switches** de distribución.
  - Varios **endpoints** que representan:
    - Activos de **infraestructura** (por ejemplo, “Srv 1”, “Router”, “Switch”).
    - Activos de **información** (por ejemplo, “Datos 1”, “Base de Datos”, “Patentes”).
  Sobre esta topología se colocan las defensas y se visualiza el movimiento de los ataques.

- **Barra de controles en fase de planificación (planning phase)**  
  Durante la fase de planificación, aparece una barra de controles que permite:
  - Seleccionar y desplegar defensas:
    - **Firewall**
    - **Identity and Access Management (IAM)**
    - Acciones de **cifrado / encryption** sobre activos de información
    - Activación de **backup**
  - Iniciar la **wave** de ataques de la ronda.

- **Modales (ventanas emergentes)**  
  El código incluye varios **modals**:
  - Tutorial inicial: describe el contexto del ejercicio, las amenazas y las defensas disponibles.
  - Fase de clasificación de activos: el alumnado debe clasificar distintos activos como “Infraestructura” o “Información”.
  - Informe de fin de ronda: muestra estadísticas y un análisis cualitativo de la resiliencia alcanzada.
  - Confirmación de reinicio de la simulación.

- **Controles de navegación del mapa**  
  Se habilita:
  - **Zoom** con botones y rueda de ratón.
  - **Scroll** y **drag** para desplazarse sobre el mapa cuando la topología se hace más compleja.

#### 1.3. Lógica de juego y estado

El núcleo de la simulación se organiza en torno a un objeto de **game state** que almacena:

- Número de **round** actual.
- Recursos (créditos).
- Nivel de integridad global.
- Estado de las métricas **ACIDA**.
- Listados de activos, defensas desplegadas, ataques activos y estadísticas por ronda.
- Un identificador de operación (**operationId**) que permite etiquetar la sesión.

La generación de cada ronda realiza:

1. Construcción de la **topología de red**:
   - Creación del **Core Router**.
   - Creación de varios **switches** de distribución.
   - Creación de **nodos (nodes)** finales de tipo infraestructura o información.
2. Distribución pseudoaleatoria de los nodos, evitando solapes.
3. Asignación de rutas de ataque desde los bordes del mapa hacia los activos objetivos.

El juego avanza pasando por varios estados:

1. Inicio y tutorial.
2. **Planning phase** (fase de planificación).
3. **Wave** (ola de ataques).
4. Informe de fin de ronda.
5. Fin de juego (**game over**) por:
   - Compromiso del sistema (integridad o métricas ACIDA en valores críticos).
   - Alcance de la ronda máxima predefinida.

#### 1.4. Ataques y defensas

Los principales tipos de ataque son:

- **DDoS**  
  Ataque distribuido orientado a saturar activos de **infraestructura**, reduciendo principalmente la **Disponibilidad** y la integridad global del sistema.

- **APT (Advanced Persistent Threat)**  
  Atacante sofisticado que busca comprometer activos de **información** durante varias rondas, afectando a la **Confidencialidad** y la **Autenticación** de los datos.

- **Ransomware**  
  Tipo de **malware** que cifra o bloquea activos de información, afectando a la **Integridad** y la **Disponibilidad**, especialmente si no existe un **backup** eficaz.

Las defensas disponibles incluyen:

- **Firewall**  
  Se despliega sobre el mapa y actúa de forma automática sobre ataques, con especial eficacia frente a **DDoS**.

- **Identity and Access Management (IAM)**  
  Control avanzado de identidades y accesos, especialmente eficaz frente a **APT** y **ransomware**, protegiendo la **Autenticación** y parte de la **Confidencialidad**.

- **Cifrado / encryption de activos de información**  
  Acción que marca un activo de tipo información como cifrado, disminuyendo o anulando el impacto de **APT** y **ransomware** sobre ese activo.

- **Backup**  
  Mecanismo que permite reducir el impacto final de un cifrado exitoso (por ejemplo, por ransomware), facilitando la recuperación de la operación y mejorando la **ciberresiliencia** del sistema.

### 2. Uso de la mecánica en el aula

1. **Carga inicial y tutorial**  
   Al abrir la página, el alumnado visualiza un **modal** con el contexto del ejercicio, los tipos de ataques y las defensas disponibles. Esta fase permite introducir de forma guiada los conceptos de **ACIDA**, **activo**, **infraestructura**, **información** y **ciberresiliencia**.

2. **Clasificación de activos**  
   Antes de la primera ronda, se muestra una pantalla de clasificación donde se deben etiquetar varios activos (por ejemplo, “Servidor Web”, “Base de Datos”, “Router”, “Patentes”, “Switch”) como:
   - Infraestructura  
   - Información  
   Una clasificación correcta puede asociarse a una recompensa en créditos; una clasificación incorrecta se refleja en el **panel de log** y sirve como punto de discusión en clase.

3. **Fase de planificación (planning phase)**  
   En cada **round**:
   - El alumnado consulta el **threat intelligence panel** para conocer los tipos de ataques esperados y su nivel.
   - Se decide la colocación de defensas sobre la topología (por ejemplo, un **firewall** cerca de un **Core Router** o de un **switch** crítico).
   - Se selecciona qué activos de información conviene cifrar y cuándo invertir en **backup**.
   - Se gestiona el presupuesto de créditos disponible, priorizando entre nuevas defensas y mejoras.

4. **Ejecución de la wave**  
   Al iniciar la **wave**, los ataques entran en el mapa y avanzan hacia sus objetivos:
   - Las defensas actúan de forma automática según su rango y tipo.
   - El **panel de log** recoge los eventos relevantes.
   - Las métricas **ACIDA** y la integridad global se actualizan en función del daño producido o mitigado.

5. **Fin de ronda e informe**  
   Al finalizar cada **wave**, un **modal** de informe de fin de ronda presenta:
   - Estadísticas (activos intactos, ataques bloqueados, defensas desplegadas).
   - Comentarios cualitativos que ayudan a interpretar la calidad de la defensa.
   - En algunos casos, la posibilidad de generar un **PDF** resumen de la ronda o de toda la operación.

6. **Progresión y fin de partida**  
   El alumnado avanza por varias rondas con amenazas crecientes. El final puede ser:
   - **game over** por fallo de ciberresiliencia (por ejemplo, integridad global en cero).
   - Alcance de la ronda máxima, interpretado como logro de un nivel alto de **ciberresiliencia**.

7. **Cheat code para uso docente**  
   El código incluye un **cheat code** (secuencia de teclas) que permite al profesorado simular rápidamente todas las rondas y generar un **PDF** final con capturas (**snapshots**) de la topología y un resumen estadístico. Es útil para disponer de un ejemplo completo sin jugar toda la partida en directo.

### 3. Objetivos didácticos

La mecánica está diseñada para trabajar, entre otros, los siguientes objetivos:

1. **Comprender la noción de ciberresiliencia**  
   El alumnado observa que no se trata sólo de evitar incidentes, sino de mantener la continuidad de servicio a pesar de sufrir ataques.

2. **Clasificar activos y entender su valor**  
   Distinguir entre activos de **infraestructura** y activos de **información**, identificando los riesgos asociados a cada categoría.

3. **Relacionar ataques con impactos en ACIDA**  
   - **DDoS** se asocia principalmente a la **Disponibilidad**.  
   - **APT** combina **Confidencialidad**, **Autenticación** y **Trazabilidad**.  
   - **Ransomware** se centra en **Integridad** y **Disponibilidad**, especialmente si no hay **backup**.

4. **Aplicar defensa en profundidad**  
   El alumnado aprende a combinar:
   - **firewall**
   - **IAM**
   - **cifrado / encryption**
   - **backup**  
   para mitigar de forma conjunta ataques complejos.

5. **Gestionar recursos limitados**  
   La asignación de créditos obliga a priorizar, por ejemplo, entre proteger todos los activos de información o reforzar la infraestructura crítica.

6. **Analizar resultados y extraer lecciones**  
   Mediante los informes de ronda y el informe final en **PDF**, se puede realizar un análisis posterior al incidente (**post-incident review**) que muestre qué decisiones han sido efectivas y cuáles no.

### 4. Resolución paso a paso (guía docente)

A continuación se describe un posible recorrido óptimo para utilizar en la corrección o para orientarse en la dinamización de la actividad.

#### 4.1. Clasificación de activos

Propuesta de clasificación:

- Servidor Web → Infraestructura  
- Base de Datos → Información  
- Router → Infraestructura  
- Patentes → Información  
- Switch → Infraestructura  

Es recomendable comentar en clase las consecuencias de clasificar erróneamente, por ejemplo, considerar la Base de Datos como infraestructura y minimizar la protección de sus datos.

#### 4.2. Rondas iniciales

En las primeras **rounds** predominan los ataques de tipo **DDoS**:

- Desplegar uno o dos **firewalls** en posiciones estratégicas, cerca del **Core Router** o de los **switches** que concentran más tráfico.
- Mantener cierta reserva de créditos para futuras rondas, evitando sobreespecializarse sólo en la **Disponibilidad**.

#### 4.3. Aparición de ransomware

En **rounds** intermedias comienzan a aparecer ataques de **ransomware**:

- Iniciar una política sistemática de **cifrado / encryption** sobre:
  - la Base de Datos,
  - activos “Datos n”,
  - activos que representen propiedad intelectual (por ejemplo, Patentes).
- Introducir el concepto de **backup** periódico y mostrar cómo la existencia de copias de seguridad modifica el impacto de un incidente de **ransomware**.

#### 4.4. Aparición de APT

Cuando el **threat intelligence panel** indica presencia de **APT**:

- Priorizar el despliegue de **Identity and Access Management (IAM)** alrededor de los activos de información más críticos.
- Explicar que muchas intrusiones se basan en credenciales comprometidas, ausencia de doble factor o fallos en la gestión de privilegios.
- Relacionar el efecto de **APT** con las métricas de **Confidencialidad**, **Autenticación** y **Trazabilidad**.

#### 4.5. Estrategia avanzada y análisis

En rondas avanzadas:

- Utilizar el **zoom**, el **scroll** y el **drag** para identificar “cuellos de botella” de la red donde un número reducido de defensas protege un gran número de rutas.
- Consolidar una estrategia de **defensa en profundidad**, donde un fallo concreto (por ejemplo, un **firewall**) no implique el colapso de la defensa global.
- Tras cada ronda, emplear el informe para realizar un mini **post-mortem**:
  - ¿Qué ataques han tenido éxito?
  - ¿Dónde faltaban defensas?
  - ¿Qué papel ha jugado el **backup**?

#### 4.6. Uso del informe final

Mediante el **cheat code** o tras completar todas las **rounds**, es posible generar un informe en **PDF** a partir de **jsPDF**:

- El informe incluye un **Executive summary**, un **threat analysis** y **snapshots** de la topología por ronda.
- Puede utilizarse como base para un ejercicio escrito adicional, un debate o una comparación entre grupos.

---

## 🇬🇧 English section

### 1. Code description

#### 1.1. General structure

The file implements a **single page application (SPA)** using **HTML5** and **JavaScript**. Rendering is done through an HTML `<canvas>`, where a **tower defense** style serious game focused on **cyber-resilience** is displayed.

The main logic is wrapped in an **IIFE**, which initialises the **game state**, sets up the **user interface (UI)**, generates the network topology, configures attack **rounds** and continuously runs the animation loop over the canvas.

Visual styling is handled via **CSS** with **theme variables**, allowing the user to switch between different visual themes directly from the interface.

#### 1.2. User interface

The UI is structured into several key areas:

- **Top bar**  
  Shows:
  - The exercise title (for example, “Resiliencia Protocol”).
  - Current **round** and total number of rounds.
  - Resources (available credits and global system integrity).
  - The **ACIDA** metrics:
    - Authentication  
    - Confidentiality  
    - Integrity  
    - Availability  
    - Traceability / Accountability  

- **Threat intelligence panel**  
  Indicates, for the current round:
  - Expected threats (**DDoS**, **APT**, **ransomware**).
  - Their approximate level, which scales with game progression.

- **Log panel**  
  Displays a real-time **log** of important events:
  - Deployment of defensive elements (for example, a **firewall**).
  - Start and end of each **wave**.
  - Successful and failed defences.
  - Damage inflicted on assets.

- **Game area (canvas)**  
  The `canvas` shows a network **topology** composed of:
  - A central **Core Router**.
  - Several distribution **switches**.
  - Multiple **endpoints** representing:
    - **Infrastructure** assets (for example, “Srv 1”, “Router”, “Switch”).
    - **Information** assets (for example, “Datos 1”, “Database”, “Patents”).

- **Controls during planning phase**  
  In the **planning phase**, a control bar allows the player to:
  - Place defensive elements:
    - **Firewall**
    - **Identity and Access Management (IAM)**
    - **Encryption** actions for information assets
    - **Backup** activation
  - Start the attack **wave**.

- **Modals**  
  Several **modals** support the learning flow:
  - Initial tutorial.
  - Asset classification step (Infrastructure vs Information).
  - End-of-round report.
  - Reset confirmation.

- **Map navigation**  
  The player can use:
  - **Zoom** (buttons and mouse wheel).
  - **Scroll** and **drag** to navigate the map.

#### 1.3. Game logic and state

The **game state** object stores:

- Current **round**.
- Credits and global integrity.
- **ACIDA** metrics.
- Lists of assets, deployed defences, active attacks and per-round statistics.
- An **operationId** to identify the session.

Each round includes:

1. Building the network topology:
   - Creating the **Core Router** and distribution **switches**.
   - Generating **nodes** (infrastructure or information endpoints).
2. Avoiding overlaps and assigning attack paths.
3. Spawning attacks from the map edges towards target assets.

The game moves through:

1. Initialisation and tutorial.
2. **Planning phase**.
3. Attack **wave**.
4. End-of-round report.
5. **Game over**, either due to failure (critical integrity or ACIDA values) or successful completion of all rounds.

#### 1.4. Attacks and defences

Main attack types:

- **DDoS** – impacts **infrastructure**, especially **Availability** and global integrity.  
- **APT (Advanced Persistent Threat)** – targets **information** assets over multiple rounds, affecting **Confidentiality**, **Authentication** and **Traceability**.  
- **Ransomware** – a type of **malware** encrypting information assets, damaging **Integrity** and **Availability**, especially without an effective **backup** strategy.

Defensive mechanisms:

- **Firewall** – network-level control, particularly effective against **DDoS**.  
- **Identity and Access Management (IAM)** – protects identities and access control, mitigating **APT** and **ransomware**.  
- **Encryption** of information assets – prevents or limits the impact of **APT** and **ransomware** on specific assets.  
- **Backup** – ensures data and service recovery, reinforcing overall **cyber-resilience**.

### 2. How to use the exercise with students

1. **Initial load and tutorial**  
   When the page is loaded, a tutorial **modal** presents the scenario, threats and available defences.

2. **Asset classification**  
   Students classify several items (for example “Web Server”, “Database”, “Router”, “Patents”, “Switch”) as:
   - Infrastructure  
   - Information  
   Their choices can be linked to rewards or penalties in credits and provide a starting point for discussion.

3. **Planning phase**  
   For each **round**:
   - Students read the **threat intelligence panel** to understand expected threats and levels.
   - They decide where to place **firewalls**, **IAM**, where to apply **encryption**, and when to invest in **backup**.
   - They manage limited credits and must prioritise.

4. **Running the wave**  
   When the **wave** starts:
   - Attacks traverse the network towards their targets.
   - Defences fire automatically according to their type and range.
   - The **log** records key outcomes and the **ACIDA** metrics update.

5. **End-of-round report**  
   A **modal** shows:
   - Quantitative results (blocked attacks, damaged assets).
   - Qualitative comments that can be used to structure a group debriefing.
   - Options to export a **PDF** report using **jsPDF**.

6. **Progression and game over**  
   As rounds progress, threats intensify and the topology grows more complex. The simulation ends with:
   - **Game over** due to insufficient resilience.
   - Successful completion of all rounds, interpreted as achieving a high level of **cyber-resilience**.

7. **Cheat code for instructors**  
   A **cheat code** can simulate all rounds and directly produce a final **PDF** report with **snapshots** of each round, useful for demonstration or for preparing materials in advance.

### 3. Educational goals

The exercise supports the following goals:

- Understand **cyber-resilience** as continuity of service under attack.  
- Correctly classify **assets** into **infrastructure** and **information**.  
- Relate threats (**DDoS**, **APT**, **ransomware**) to their impact on **ACIDA** metrics.  
- Design **defence in depth** strategies combining **firewall**, **IAM**, **encryption** and **backup**.  
- Practise decision-making under resource constraints (limited credits).  
- Conduct a structured **post-incident review** based on the exported **PDF** report (**Executive summary**, **threat analysis**, diagrams and **snapshots**).

---

## Glosario de términos / Glossary of terms

> Todos los términos técnicos o en inglés utilizados en el documento se definen a continuación.

- **HTML**: Lenguaje de marcas utilizado para estructurar el contenido de páginas web.  
- **HTML5**: Versión moderna de HTML que introduce nuevas etiquetas, APIs y capacidades multimedia.  
- **single page application (SPA)**: Aplicación web que carga una sola página HTML y actualiza dinámicamente su contenido sin volver a cargar la página completa.  
- **JavaScript**: Lenguaje de programación principal del navegador que permite añadir interacción y lógica a páginas web.  
- **CSS**: Lenguaje de hojas de estilo usado para definir la presentación visual (colores, fuentes, distribución) de una página web.  
- **canvas**: Elemento de HTML que proporciona una superficie de dibujo bidimensional manipulable desde JavaScript.  
- **Resiliencia Protocol**: Nombre del escenario o juego serio centrado en la idea de ciberresiliencia.  
- **Asset Guardian**: Nombre alternativo o descriptivo del rol del jugador como “guardián” de los activos.  
- **IIFE (Immediately Invoked Function Expression)**: Patrón de JavaScript en el que una función se define y se ejecuta inmediatamente para encapsular variables y evitar contaminaciones del ámbito global.  
- **theme variable / variable de tema**: Variable utilizada en CSS para definir colores, tamaños u otros atributos que se pueden cambiar dinámicamente para alterar el tema visual.  
- **interfaz de usuario (UI)**: Conjunto de elementos visuales e interactivos a través de los cuales la persona usuaria interactúa con la aplicación.  
- **top bar**: Barra superior de la interfaz que suele mostrar título, estado y controles principales.  
- **threat intelligence panel**: Panel que muestra información sobre las amenazas presentes o esperadas en cada ronda.  
- **log / panel de log**: Registro secuencial de eventos y acciones que han ocurrido durante la ejecución del sistema.  
- **modal**: Ventana emergente superpuesta sobre la interfaz principal, que requiere interacción antes de continuar.  
- **zoom**: Acción de acercar o alejar la vista sobre el mapa o la interfaz.  
- **scroll**: Desplazamiento vertical u horizontal del contenido más allá de la parte visible en pantalla.  
- **drag**: Acción de “arrastrar” elementos o la vista manteniendo pulsado el botón del ratón mientras se mueve.  
- **snapshot**: Captura puntual del estado visual (por ejemplo, una imagen del `canvas` en un momento concreto).  
- **game state**: Conjunto de variables que representan el estado actual de la partida (ronda, recursos, defensas, etc.).  
- **round**: Unidad discreta de tiempo o etapa del juego en la que se planifica y ejecuta una ola de ataques.  
- **wave**: Oleada de ataques que se lanzan durante una ronda concreta.  
- **planning phase**: Fase previa al ataque en la que se toman decisiones de configuración y despliegue de defensas.  
- **game over**: Estado final de la partida cuando se cumple una condición de derrota o finalización.  
- **operationId**: Identificador único que etiqueta una ejecución o sesión concreta del juego.  
- **activo**: Cualquier recurso con valor para la organización (equipos, aplicaciones, datos, patentes, etc.).  
- **infraestructura**: Conjunto de elementos físicos o lógicos que soportan los servicios (routers, switches, servidores).  
- **activo de información**: Activo cuya principal relevancia es el contenido de datos que almacena o procesa (bases de datos, ficheros, registros de clientes, propiedad intelectual).  
- **router**: Dispositivo de red que dirige el tráfico entre distintas redes o segmentos.  
- **switch**: Dispositivo de red que conecta múltiples equipos en una misma red local y reenvía tramas según direcciones físicas.  
- **endpoint**: Nodo final de una red donde reside un activo (por ejemplo, servidor, estación de trabajo o dispositivo final).  
- **topología de red / network topology**: Forma en que los nodos de una red se conectan entre sí (estructura y relaciones).  
- **nodo (node)**: Punto de la red que puede enviar, recibir o reenviar información (router, switch, servidor, etc.).  
- **ciberresiliencia / cyber-resilience**: Capacidad de una organización o sistema para mantener o recuperar rápidamente sus funciones críticas ante incidentes de ciberseguridad.  
- **ACIDA**: Modelo de cinco atributos de seguridad: Autenticación, Confidencialidad, Integridad, Disponibilidad y Trazabilidad/Accountability.  
- **Autenticación (Authentication)**: Proceso mediante el cual un sistema verifica la identidad de una persona, dispositivo o proceso.  
- **Confidencialidad (Confidentiality)**: Propiedad que garantiza que la información sólo es accesible a personas o sistemas autorizados.  
- **Integridad (Integrity)**: Propiedad que asegura que la información no ha sido alterada de forma no autorizada o accidental.  
- **Disponibilidad (Availability)**: Capacidad de un sistema o servicio para estar accesible y operativo cuando se necesita.  
- **Trazabilidad (Traceability)**: Capacidad de un sistema para registrar y reconstruir acciones, eventos y cambios realizados sobre los activos.  
- **Accountability**: Responsabilidad asociada a cada acción registrada, de forma que se pueda atribuir a una identidad concreta.  
- **DDoS (Distributed Denial of Service)**: Ataque distribuido que busca saturar recursos (ancho de banda, CPU, memoria) para dejar un servicio inaccesible.  
- **APT (Advanced Persistent Threat)**: Amenaza avanzada y persistente, normalmente llevada a cabo por un actor sofisticado que mantiene una presencia prolongada en la red objetivo.  
- **ransomware**: Tipo de malware que cifra o bloquea datos y exige un pago (rescate) para recuperarlos.  
- **malware**: Software malicioso diseñado para dañar sistemas, robar información o realizar actividades no autorizadas.  
- **firewall**: Dispositivo o software que controla y filtra el tráfico de red según un conjunto de reglas de seguridad.  
- **Identity and Access Management (IAM)**: Conjunto de políticas, procesos y tecnologías para gestionar identidades digitales y sus permisos de acceso.  
- **cifrado / encryption**: Proceso de transformar información legible en un formato ilegible para protegerla frente a accesos no autorizados.  
- **backup**: Copia de datos o sistemas que permite restaurarlos después de una pérdida o incidente.  
- **defensa en profundidad / defence in depth**: Estrategia de seguridad que consiste en aplicar múltiples capas de controles para que el fallo de una sola capa no comprometa la protección global.  
- **post-mortem**: Análisis estructurado que se realiza después de un incidente para entender causas y proponer mejoras.  
- **post-incident review**: Revisión formal posterior a un incidente de seguridad para evaluar la respuesta, el impacto y las medidas correctivas.  
- **Executive summary**: Resumen ejecutivo de alto nivel dirigido a responsables de decisión, con los puntos clave de un informe más extenso.  
- **threat analysis**: Análisis sistemático de las amenazas que afectan a un sistema, su probabilidad y su impacto.  
- **crown jewel data**: Datos especialmente valiosos o críticos para la organización, cuya pérdida o filtración tendría un impacto muy elevado.  
- **localStorage**: Mecanismo de almacenamiento clave-valor del navegador que permite guardar datos de forma persistente en el dispositivo del usuario.  
- **jsPDF**: Librería de JavaScript para generar documentos **PDF** desde el navegador.  
- **PDF (Portable Document Format)**: Formato de documento que conserva el diseño original y se puede visualizar en múltiples plataformas.  
- **MIT License**: Licencia de software permisiva que permite reutilizar, modificar y distribuir el código, siempre que se mantenga el aviso de copyright y la licencia.
