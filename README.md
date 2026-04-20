### CASO IA: Búsqueda, Conocimiento y Asimetría

**INTEGRANTES**

Maria Jose Perez Zamora
**OBJETIVO**

En este ejercicio, explorarán los desafíos que presentan los juegos asimétricos para los algoritmos de búsqueda tradicionales. Analizarán las diferencias en el modelado del espacio de soluciones para agentes con objetivos opuestos, el entrenamiento del sistema y su viabilidad.

### PARTE 1: BÚSQUEDA CLÁSICA Y EL DESAFÍO DE BAGH-CHAL

**Escenario:** Imagine que a su equipo de ingeniería se le asigna la tarea de crear un agente de inteligencia artificial capaz de dominar Bagh-Chal. Inicialmente, deben evaluar cómo modelar el entorno asimétrico y evaluar la viabilidad de los métodos de búsqueda tradicionales.

**Actividad:** Su objetivo es definir el problema computacional y los obstáculos iniciales. Discutan y respondan las siguientes cuestiones:

- **Modelado del entorno:** Expliquen qué tipos de problemas se pueden modelar como búsqueda en un espacio de soluciones y cómo se modelan. Además, describan cómo se encontraría la solución computacional para un tablero estructurado 5x5.

- **Evaluación de algoritmos:** Detallen para qué sirven los algoritmos A\* y Minimax. Destaquen qué adaptaciones y consideraciones especiales necesitan implementarse para un juego donde las fuerzas iniciales son desiguales, 4 tigres vs 20 cabras.


- **La complejidad de la asimetría:** Identifiquen los desafíos particulares de Bagh-Chal para las funciones de evaluación. ¿Cómo logran la victoria Tigres y Cabras?

- **Evaluación de estados:** En arquitecturas de IA modernas, expliquen qué función cumplirían las redes neuronales. Analicen esto partiendo de la disposición inicial del juego, donde los 4 tigres se ubican en las cuatro esquinas del tablero.


- **Estrategia de entrenamiento:** Si se utiliza un enfoque de aprendizaje por refuerzo donde el sistema juega millones de partidas contra sí mismo ¿por qué este método híbrido puede ser superior a la codificación manual de estrategias asimétricas?

- **Métricas de progreso:** Durante el entrenamiento autónomo, propongan qué métricas o criterios de evaluación específicos podrían usarse para medir la mejora del bando de las cabras frente al bando de los tigres.


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
