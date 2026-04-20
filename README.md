### CASO IA: Búsqueda, Conocimiento y Asimetría

**INTEGRANTES**

- Maria Jose Perez Zamora
**OBJETIVO**

En este ejercicio, explorarán los desafíos que presentan los juegos asimétricos para los algoritmos de búsqueda tradicionales. Analizarán las diferencias en el modelado del espacio de soluciones para agentes con objetivos opuestos, el entrenamiento del sistema y su viabilidad.

### PARTE 1: BÚSQUEDA CLÁSICA Y EL DESAFÍO DE BAGH-CHAL

**Escenario:** Imagine que a su equipo de ingeniería se le asigna la tarea de crear un agente de inteligencia artificial capaz de dominar Bagh-Chal. Inicialmente, deben evaluar cómo modelar el entorno asimétrico y evaluar la viabilidad de los métodos de búsqueda tradicionales.

**Actividad:** Su objetivo es definir el problema computacional y los obstáculos iniciales. Discutan y respondan las siguientes cuestiones:

- **Modelado del entorno:** Expliquen qué tipos de problemas se pueden modelar como búsqueda en un espacio de soluciones y cómo se modelan. Además, describan cómo se encontraría la solución computacional para un tablero estructurado 5x5.

**Respuesta:**
Se pueden modelar como búsqueda en un espacio de soluciones aquellos problemas donde existe un conjunto finito (o acotado) de estados y acciones, como juegos de tablero, laberintos, rutas, planificación de tareas, etc. El modelado consiste en definir:
- El estado inicial (por ejemplo, la disposición de piezas en el tablero).
- El conjunto de acciones legales desde cada estado (movimientos permitidos para cada jugador).
- Las reglas de transición (cómo cambia el estado tras cada acción).
- Las condiciones de objetivo o victoria.
En Bagh-Chal, el tablero 5x5 se representa como una matriz, donde cada celda puede estar vacía, tener un tigre o una cabra. La solución computacional implica generar el árbol de estados posibles desde la disposición inicial, considerando las reglas asimétricas: primero se colocan cabras, luego se mueven, y los tigres pueden capturar. El espacio de búsqueda es muy grande, por lo que se usan algoritmos para explorar solo las ramas más prometedoras.

- **Evaluación de algoritmos:** Detallen para qué sirven los algoritmos A\* y Minimax. Destaquen qué adaptaciones y consideraciones especiales necesitan implementarse para un juego donde las fuerzas iniciales son desiguales, 4 tigres vs 20 cabras.

**Respuesta:**
A* es un algoritmo de búsqueda informada que encuentra caminos óptimos en grafos, combinando el costo real y una heurística para estimar el costo restante. Es útil en problemas de rutas o laberintos, pero en juegos de adversarios se prefiere Minimax.
Minimax explora el árbol de juego asumiendo que ambos jugadores juegan óptimamente, maximizando la ganancia propia y minimizando la del rival. En Bagh-Chal, la asimetría exige adaptar Minimax:
- Los tigres tienen como objetivo capturar cabras, mientras que las cabras buscan bloquear a los tigres.
- Las funciones de evaluación deben ser diferentes para cada bando: para tigres, priorizar movilidad y capturas; para cabras, maximizar cobertura y minimizar pérdidas.
- Se deben considerar fases distintas: colocación de cabras, movimiento de cabras, movimiento y captura de tigres.
Además, se pueden usar variantes como Alpha-Beta pruning para reducir el número de estados evaluados.


- **La complejidad de la asimetría:** Identifiquen los desafíos particulares de Bagh-Chal para las funciones de evaluación. ¿Cómo logran la victoria Tigres y Cabras?

**Respuesta:**
La asimetría de Bagh-Chal implica que los bandos tienen objetivos y capacidades muy diferentes:
- Los tigres ganan si capturan suficientes cabras para evitar ser bloqueados (generalmente, si quedan menos de 5 cabras en el tablero, los tigres no pueden ser bloqueados).
- Las cabras ganan si logran inmovilizar a todos los tigres, bloqueando sus movimientos.
Esto genera desafíos para las funciones de evaluación:
- Para los tigres, la función debe valorar la movilidad, la cantidad de cabras capturadas y las oportunidades de captura.
- Para las cabras, la función debe valorar la cobertura del tablero, la minimización de bajas y la capacidad de formar bloqueos.
Además, la asimetría hace que el balance del juego sea delicado y que las estrategias óptimas sean muy diferentes para cada bando.

- **Evaluación de estados:** En arquitecturas de IA modernas, expliquen qué función cumplirían las redes neuronales. Analicen esto partiendo de la disposición inicial del juego, donde los 4 tigres se ubican en las cuatro esquinas del tablero.

**Respuesta:**
En arquitecturas modernas de IA, las redes neuronales profundas pueden aprender funciones de evaluación complejas a partir de grandes cantidades de datos de partidas. En Bagh-Chal, una red puede recibir como entrada la representación del tablero (por ejemplo, una matriz codificada) y predecir la probabilidad de victoria para cada bando o el valor del estado.
Desde la disposición inicial (tigres en las esquinas), la red puede aprender patrones como:
- Qué posiciones de cabras tienden a bloquear a los tigres.
- Qué configuraciones permiten capturas múltiples.
- Cómo evolucionan las fases del juego.
Esto permite superar las limitaciones de heurísticas manuales y adaptarse a la complejidad asimétrica del juego, aprendiendo estrategias que pueden ser incluso superiores a las humanas.


- **Estrategia de entrenamiento:** Si se utiliza un enfoque de aprendizaje por refuerzo donde el sistema juega millones de partidas contra sí mismo ¿por qué este método híbrido puede ser superior a la codificación manual de estrategias asimétricas?

**Respuesta:**
El aprendizaje por refuerzo (RL) permite que el agente explore el espacio de estrategias jugando contra sí mismo millones de veces, ajustando sus políticas en función de la retroalimentación (recompensas por ganar, empatar o perder). Este método es superior a la codificación manual porque:
- Descubre tácticas y patrones que los humanos pueden pasar por alto.
- Se adapta dinámicamente a la asimetría y a los cambios en el entorno.
- Permite optimizar estrategias para ambos bandos, incluso en situaciones poco frecuentes.
El RL puede combinarse con redes neuronales (Deep RL) para aprender funciones de evaluación y políticas directamente desde la experiencia, logrando un rendimiento superior y menos sesgado que las estrategias programadas manualmente.

- **Métricas de progreso:** Durante el entrenamiento autónomo, propongan qué métricas o criterios de evaluación específicos podrían usarse para medir la mejora del bando de las cabras frente al bando de los tigres.

**Respuesta:**
Algunas métricas útiles para evaluar el progreso durante el entrenamiento autónomo son:
- Tasa de victorias de las cabras y de los tigres.
- Promedio de cabras capturadas antes de que los tigres sean bloqueados.
- Número de partidas empatadas o sin resolución.
- Tiempo promedio (en turnos) para lograr la victoria de cada bando.
- Diversidad y robustez de las estrategias aprendidas (por ejemplo, cuántas formas distintas de bloqueo o captura se emplean).
Estas métricas permiten identificar si el agente mejora, si aprende nuevas tácticas y si el juego se mantiene balanceado entre ambos bandos.


### PARTE 2: IMPACTO Y TRANSFERENCIA DE SOLUCIONES

**Escenario:** El modelo tiene un rendimiento excepcional y supera por mucho a los jugadores humanos. Ahora, se busca comprender cómo estas metodologías pueden resolver problemas del mundo real.

**ACTIVIDAD:** Reflexionen sobre el ciclo de desarrollo, la inteligencia artificial y su aplicación más allá de los juegos.

- **Ciclo de vida del desarrollo:** Si tuvieran que diseñar este sistema de IA de caza/evasión desde cero, ¿cuáles serían las fases esenciales de desarrollo, desde la recolección inicial de partidas hasta la validación final del agente?

**Respuesta:**
1. Definición del problema y objetivos: Especificar claramente las reglas, condiciones de victoria y métricas de éxito.
2. Recolección y análisis de datos: Obtener partidas históricas, simuladas o generadas artificialmente para analizar patrones y estrategias.
3. Modelado del entorno: Representar el tablero, los agentes y las reglas en una estructura computacional.
4. Selección de algoritmos: Elegir técnicas de búsqueda, aprendizaje por refuerzo y/o redes neuronales según la complejidad y los objetivos.
5. Entrenamiento del agente: Simular millones de partidas para que el agente aprenda estrategias óptimas, ajustando hiperparámetros y funciones de recompensa.
6. Evaluación y validación: Medir el desempeño del agente contra jugadores humanos y otros agentes, usando métricas objetivas y pruebas de robustez.
7. Iteración y mejora: Refinar el modelo y el entrenamiento según los resultados, corrigiendo debilidades y optimizando el rendimiento.
8. Despliegue y monitoreo: Implementar el agente en un entorno real o de competencia, monitoreando su desempeño y adaptándolo si es necesario.
- **Framework universal:** Debatan si es factible diseñar un framework general capaz de dominar cualquier juego de dos jugadores con información perfecta y reglas asimétricas. ¿Qué limitaciones inherentes existirían?

**Respuesta:**
Es posible diseñar frameworks generales para juegos de dos jugadores con información perfecta (como ajedrez, Go, Bagh-Chal), pero existen limitaciones:
- La explosión combinatoria del espacio de estados puede hacer inviable la búsqueda exhaustiva en juegos muy complejos.
- Las reglas asimétricas requieren que el framework sea flexible para modelar objetivos, acciones y evaluaciones distintas para cada bando.
- Algunos juegos pueden tener elementos de azar, información oculta o reglas cambiantes, lo que complica la generalización.
- La eficiencia y el rendimiento pueden verse afectados si el framework es demasiado genérico y no aprovecha particularidades del juego.
En resumen, aunque es factible crear frameworks universales para juegos de información perfecta y reglas claras, siempre habrá desafíos de escalabilidad, personalización y eficiencia.
- **Reflexión filosófica:** La IA no "entiende" los conceptos biológicos de un tigre o una cabra, pero juega con una optimización espacial insuperable. ¿Qué nos dice esto sobre la relación entre la competencia técnica y la comprensión real en la inteligencia artificial?

**Respuesta:**
La IA puede alcanzar un nivel de competencia técnica sobresaliente en tareas específicas sin comprender el significado profundo o biológico de los elementos involucrados. Esto evidencia que la optimización matemática y la búsqueda de patrones pueden superar la comprensión conceptual o semántica. La IA "juega" a ganar, no a entender. Esto plantea preguntas sobre los límites de la inteligencia artificial: puede ser experta en resolver problemas, pero carece de conciencia, intuición o comprensión real del contexto, actuando solo sobre representaciones abstractas y reglas formales.

### COMPARAR Y CONTRASTAR

Utilice la siguiente tabla para organizar su respuesta final a manera de comparación.

| **Característica**                         | **Búsqueda en Juegos Simétricos (Ajedrez / Go)** | **Modelado Asimétrico (Bagh-Chal)** |
| ------------------------------------------ | ------------------------------------------------ | ----------------------------------- |
| Diseño de la función heurística/evaluación | Suele ser única para ambos jugadores, basada en material, control de centro, movilidad, etc. | Debe ser diferente para cada bando: para tigres, movilidad y capturas; para cabras, cobertura y bloqueo. |
| Condiciones de victoria de los jugadores   | Normalmente ambos jugadores tienen condiciones simétricas (dar mate, rodear al rey, capturar todas las piezas). | Los tigres ganan capturando cabras; las cabras ganan bloqueando a los tigres. Condiciones y caminos a la victoria distintos. |
| Mecánicas y capacidades de movimiento      | Ambos jugadores tienen piezas con movimientos equivalentes o similares. | Los tigres pueden moverse y capturar; las cabras solo se colocan o mueven, pero no capturan. |
| Complejidad de la fase inicial del juego   | Generalmente ambos jugadores parten de posiciones equivalentes y con información completa. | El juego tiene fases diferenciadas: primero se colocan cabras, luego se mueven; los tigres siempre están en las esquinas al inicio. |
| Estrategia de entrenamiento por refuerzo   | El agente puede aprender estrategias generales válidas para ambos bandos. | El agente debe aprender estrategias especializadas y asimétricas para cada bando, adaptándose a objetivos y capacidades distintas. |

### Bibliografía

GitHub Copilot. (2026). Asistente de programación con IA (versión GPT-4.1) [Herramienta de software]. Microsoft. https://github.com/features/copilot
