### CASO IA: Búsqueda, Conocimiento y Asimetría

**INTEGRANTES**

Maria Jose Perez Zamora
**OBJETIVO**

En este ejercicio, explorarán los desafíos que presentan los juegos asimétricos para los algoritmos de búsqueda tradicionales. Analizarán las diferencias en el modelado del espacio de soluciones para agentes con objetivos opuestos, el entrenamiento del sistema y su viabilidad.

### PARTE 1: BÚSQUEDA CLÁSICA Y EL DESAFÍO DE BAGH-CHAL

**Escenario:** Imagine que a su equipo de ingeniería se le asigna la tarea de crear un agente de inteligencia artificial capaz de dominar Bagh-Chal. Inicialmente, deben evaluar cómo modelar el entorno asimétrico y evaluar la viabilidad de los métodos de búsqueda tradicionales.

**Actividad:** Su objetivo es definir el problema computacional y los obstáculos iniciales. Discutan y respondan las siguientes cuestiones:

- **Modelado del entorno:** Expliquen qué tipos de problemas se pueden modelar como búsqueda en un espacio de soluciones y cómo se modelan. Además, describan cómo se encontraría la solución computacional para un tablero estructurado 5x5.

_Respuesta:_ Los problemas que se pueden modelar como búsqueda en un espacio de soluciones son aquellos donde existe un estado inicial, un conjunto de acciones posibles, una función de transición y un estado objetivo. Ejemplos: laberintos, puzzles (8-puzzle, Sudoku), planificación de rutas y juegos de tablero. Se modelan como un grafo o árbol donde cada nodo es un estado y cada arista es una acción.

Para Bagh-Chal en un tablero 5×5:
- El estado se representa como una tupla: posición de los 4 tigres, posición de las cabras colocadas, número de cabras en mano, número de cabras capturadas, y de quién es el turno.
- Hay 25 posiciones válidas, conectadas por líneas diagonales y ortogonales.
- La solución se encuentra expandiendo el árbol de juego desde el estado inicial (tigres en esquinas, 0 cabras colocadas) hasta un estado terminal: 5 cabras capturadas (ganan tigres) o los 4 tigres bloqueados (ganan cabras).

- **Evaluación de algoritmos:** Detallen para qué sirven los algoritmos A\* y Minimax. Destaquen qué adaptaciones y consideraciones especiales necesitan implementarse para un juego donde las fuerzas iniciales son desiguales, 4 tigres vs 20 cabras.

_Respuesta:_
- **A\*** es un algoritmo de búsqueda de camino óptimo en grafos. Usa f(n) = g(n) + h(n), donde g(n) es el costo real y h(n) es una heurística admisible. Es ideal para problemas de un solo agente, pero en Bagh-Chal su aplicación es limitada porque hay dos agentes con objetivos opuestos.
- **Minimax** es el algoritmo estándar para juegos adversariales de dos jugadores. Un agente maximiza su ganancia y el otro la minimiza, asumiendo juego óptimo de ambos lados. La poda alfa-beta reduce el árbol explorado.
- **Adaptaciones para la asimetría:**
  - Dos funciones de evaluación separadas, una por bando.
  - Fases diferenciadas: la colocación de cabras no existe en juegos simétricos.
  - Factor de ramificación desigual: los tigres tienen entre 0 y ~8 movimientos, las cabras hasta 21 opciones.

- **La complejidad de la asimetría:** Identifiquen los desafíos particulares de Bagh-Chal para las funciones de evaluación. ¿Cómo logran la victoria Tigres y Cabras?

_Respuesta:_
Las condiciones de victoria son radicalmente distintas:

| Bando  | Condición de victoria                                                 |
| ------ | --------------------------------------------------------------------- |
| Tigres | Capturar **5 cabras** (salto sobre cabra a casilla vacía)             |
| Cabras | **Bloquear los 4 tigres** de forma que ninguno tenga movimiento legal |

- Para los tigres: la heurística debe valorar movilidad, presión sobre cabras y control de zonas centrales.
- Para las cabras: la heurística debe valorar bloqueos cooperativos, densidad alrededor de tigres y protección de cabras vulnerables.
- La función de evaluación debe cambiar según la fase activa.

- **Evaluación de estados:** En arquitecturas de IA modernas, expliquen qué función cumplirían las redes neuronales. Analicen esto partiendo de la disposición inicial del juego, donde los 4 tigres se ubican en las cuatro esquinas del tablero.

_Respuesta:_
En arquitecturas modernas como AlphaZero, las redes neuronales reemplazan funciones heurísticas manuales:
- **Red de valor:** Estima la probabilidad de victoria para el bando activo.
- **Red de política:** Da una distribución de probabilidad sobre los movimientos legales.
- La red aprende patrones como "tigre acorralado" o "formación de bloqueo cabras" a través del entrenamiento, no por reglas explícitas.

- **Estrategia de entrenamiento:** Si se utiliza un enfoque de aprendizaje por refuerzo donde el sistema juega millones de partidas contra sí mismo ¿por qué este método híbrido puede ser superior a la codificación manual de estrategias asimétricas?

_Respuesta:_
El aprendizaje por refuerzo (self-play) es superior a la codificación manual porque:
- Descubre estrategias no humanas.
- Se adapta a la asimetría sin sesgos.
- Es escalable a variantes del juego.
- El self-play fuerza la mejora de ambos bandos simultáneamente.

- **Métricas de progreso:** Durante el entrenamiento autónomo, propongan qué métricas o criterios de evaluación específicos podrían usarse para medir la mejora del bando de las cabras frente al bando de los tigres.

_Respuesta:_
- Tasa de victorias por bando a lo largo del tiempo.
- Cabras capturadas promedio por partida.
- Turnos hasta el fin del juego.
- Frecuencia de bloqueos exitosos.
- Elo relativo entre versiones.
- Entropía de la política.


### PARTE 2: IMPACTO Y TRANSFERENCIA DE SOLUCIONES

**Escenario:** El modelo tiene un rendimiento excepcional y supera por mucho a los jugadores humanos. Ahora, se busca comprender cómo estas metodologías pueden resolver problemas del mundo real.

**ACTIVIDAD:** Reflexionen sobre el ciclo de desarrollo, la inteligencia artificial y su aplicación más allá de los juegos.

- **Ciclo de vida del desarrollo:** Si tuvieran que diseñar este sistema de IA de caza/evasión desde cero, ¿cuáles serían las fases esenciales de desarrollo, desde la recolección inicial de partidas hasta la validación final del agente?
- **Framework universal:** Debatan si es factible diseñar un framework general capaz de dominar cualquier juego de dos jugadores con información perfecta y reglas asimétricas. ¿Qué limitaciones inherentes existirían?
- **Reflexión filosófica:** La IA no "entiende" los conceptos biológicos de un tigre o una cabra, pero juega con una optimización espacial insuperable. ¿Qué nos dice esto sobre la relación entre la competencia técnica y la comprensión real en la inteligencia artificial?

### COMPARAR Y CONTRASTAR

Utilice la siguiente tabla para organizar su respuesta final a manera de comparación.

| **Característica**                         | **Búsqueda en Juegos Simétricos (Ajedrez / Go)** | **Modelado Asimétrico (Bagh-Chal)** |
| ------------------------------------------ | ------------------------------------------------ | ----------------------------------- |
| Diseño de la función heurística/evaluación |                                                  |                                     |
| Condiciones de victoria de los jugadores   |                                                  |                                     |
| Mecánicas y capacidades de movimiento      |                                                  |                                     |
| Complejidad de la fase inicial del juego   |                                                  |                                     |
| Estrategia de entrenamiento por refuerzo   |                                                  |                                     |