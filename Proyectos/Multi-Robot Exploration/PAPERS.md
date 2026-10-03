# Literature

## Search Queries (Active)
- "multi-robot exploration reinforcement learning" — Google Scholar 2021-2025
- "cooperative exploration unknown environment neural network" — Google Scholar 2022-2025

## Reading Template
Para cada paper:
- **Title:**  
- **Authors:**  
- **Year:**  
- **Problem solved:**  
- **Method:**  
- **Key results:**  
- **Limitations:**  
- **Open questions / gaps:**  
- **Relevance to this project:**

---

## Papers Read
- [ ] (TODO) - [Multi-Agent Deep Reinforcement Learning for Multi-Robot Applications: A Survey](https://www.mdpi.com/1424-8220/23/7/3625)
	- [ ] Presenta varios algoritmos, ideas de problemas que se han hecho ya, revisando que son y determinando si son válidos para lo que yo quiero hacer
- [ ] (TODO) - [Deep Reinforcement Learning for Decentralized Multi-Robot Exploration With Macro Actions](https://ieeexplore.ieee.org/abstract/document/9963690)
- [ ] (TODO) - [MARVEL: Multi-Agent Reinforcement Learning for Constrained Field-of-View Multi-Robot Exploration in Large-Scale Environments](https://ieeexplore.ieee.org/abstract/document/11127700)

## Gaps Found
*(vacío — se llena con la literatura)*

## Key Venues to Follow
- ICRA (International Conference on Robotics and Automation)
- IROS (International Conference on Intelligent Robots and Systems)
- CoRL (Conference on Robot Learning)
- RAL (IEEE Robotics and Automation Letters)
- AAMAS (Autonomous Agents and Multi-Agent Systems)

# Paper 1 — Orr & Dutta, "Multi-Agent Deep Reinforcement Learning for Multi-robot Applications: A Survey"

**Rol en el proyecto:** punto de entrada general al campo. No es un paper de investigación original, es un survey. Sirve para orientar vocabulario y mapear qué está resuelto vs. qué sigue abierto, no como fuente primaria para citar hallazgos específicos de un solo experimento.
**Relevancia filtrada a Dirección B+C** (coordinación bajo restricciones realistas + percepción compartida como base de decisión colectiva).

---
## Problema que resuelve (el survey, en general)

Mapea el estado del arte de cómo múltiples robots usan deep reinforcement learning para aprender políticas conjuntas o individuales, cubriendo desde los fundamentos (MDP, Q-learning) hasta extensiones multi-agente (MADDPG, MAPPO) y aplicaciones (coverage, exploración, navegación, construcción, etc).
## Lo relevante para mi dirección

### Coordinación bajo restricciones (Dirección B)

- La exploración multi-robot es distinta del problema clásico de Coverage Path Planning (CPP): en exploración puede existir la restricción de **mantener conectividad inalámbrica** con robots de rango de comunicación limitado. El survey la menciona como una diferencia clave frente a CPP, pero no la desarrolla a fondo — **gap a confirmar con literatura adicional**.
- La complejidad de los enfoques multi-agente **crece exponencialmente con el número de robots**, lo cual limita la escalabilidad de los métodos conjuntos (joint-policy). Esto es relevante como restricción de diseño: cualquier sistema que proponga debe considerar este techo de escalabilidad.
- El survey **no trata a fondo la tolerancia a fallas de robot** (un robot que se cae o deja de responder). Es una ausencia notable — posible indicio de gap real, pendiente de confirmar con búsqueda dirigida.
- **Value Function Factorization**: técnica para descomponer la contribución individual de cada robot a una recompensa conjunta, sin tener que modelar el espacio de estados/acciones combinado completo (que se vuelve inmanejable). Relevante si mi sistema necesita evaluar "qué tan bien está coordinando cada robot" sin centralizar todo el cómputo.

### Percepción compartida y decisión colectiva (Dirección C)
- **Graph Neural Networks (GNN) para exploración multi-robot**: representan el espacio a explorar como un grafo y lo recorren de forma "coarse-to-fine" (primero una pasada gruesa, luego refinamiento por zonas/"hops"). Es el enfoque que más se alinea con una decisión colectiva basada en percepción compartida, en lugar de percepción puramente individual. **Candidato fuerte como mecanismo central del proyecto** — pendiente profundizar si ya se ha combinado con restricciones de comunicación o fallas (subtema 3 de la semana).
- **Arquitectura divide-and-conquer**: separar un módulo de "sensado ambiental" (percepción) de un módulo de "política" (decisión), ambos entrenables. Relevante como patrón de arquitectura general, no necesariamente ligado a GNN.
- **Approach CNN + PPO descentralizado para collision avoidance**: los robots comparten los parámetros de una misma red, que mapea directamente de LiDAR a comandos de control, tratando el entorno sensado como una "imagen" de la que el CNN extrae características. Marcado como un approach replicable para mi propio sistema — es un patrón técnico concreto y relativamente simple de implementar que resuelve percepción→acción en un solo robot y escala por compartir pesos, no por centralizar decisión.

### Descartado como núcleo de investigación (Dirección A)
- El esquema **independiente** (cada robot corre su propio RL, ignora a los demás, sin mecanismo de coordinación) está resuelto y es, según el propio survey, la opción de implementación _más simple_ disponible. No es un gap — es la base sobre la que se construyen los enfoques cooperativos. Útil como posible **baseline de comparación** para mi sistema, no como pregunta de investigación.

## Lo que deja abierto (para mi research question)
1. Conectividad de comunicación limitada en exploración — mencionado pero no resuelto en profundidad aquí.
2. Tolerancia a fallas de robot — prácticamente ausente en este survey.
3. Si el enfoque GNN de exploración "coarse-to-fine" se ha combinado alguna vez con las dos restricciones anteriores, o si solo se ha probado en condiciones ideales de comunicación/sin fallas.

## Técnico — no relevante a la research question, solo a implementación futura
(Guardado por referencia, no determina la pregunta de investigación)

- Familias de algoritmo: DQN, Double DQN (DDQN), DDPG, PPO (clip/penalty), TRPO, A3C
- Extensiones multi-agente: MADDPG (actor descentralizado, crítico centralizado), MAPPO (centralized training, decentralized execution)
- Common experience memory como técnica para DQN multi-agente independiente
- Voronoi partitioning para asignación de zonas entre robots
- Validación experimental de otro trabajo citado: Gazebo + 3x TurtleBot3 Waffle Pi, usando Prioritised Experience Replay con demostraciones humanas

## Nota de validación
- Corregido typo de transcripción: "O-learning" → **Q-learning** (consistente con el resto del documento, que usa Q-learning/Q-values repetidamente).
- Terminología general (MDP, Bellman, DQN, DDPG, MADDPG, PPO, MAPPO) es estándar en la literatura de MARL — sin inconsistencias detectadas.
- Como es un survey, cualquier afirmación específica de "estado del arte" aquí debería eventualmente rastrearse a su paper original antes de citarla en la propuesta final — el survey es buen mapa, no fuente primaria.