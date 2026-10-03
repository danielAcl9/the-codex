# Research

## Working Project Statement
I am developing a multi-robot autonomous exploration system in which ground robots collaboratively explore unknown environments, share partial information, and make autonomous decisions about where to explore next. The project investigates whether learning-based coordination can improve exploration efficiency and robustness under ==realistic constraints such as limited communication, battery resources, partial observability, and robot failures.==

## Core Question
How can a group of autonomous robots collaboratively explore an unknown environment and decide what to do next using incomplete information?

==⚠️ This question is not yet fully specified. The exact contribution must be found through literature review.==

### Direction: Coordination under constraints
Robust coordination under realistic constraints, using central perception as a base for colective desition. 

*¿Puede un swarm de robots aprender políticas de coordinación que mantengan eficiencia de exploración cuando la comunicación es intermitente/limitada y algún robot puede fallar, y en qué medida una representación de percepción compartida (vs. independiente) mejora esa robustez?*

**A arreglar:**
1. Son 2 preguntas en una. (Lo mejor sería que lo primero fuera la pregunta, y lo segundo una ablación.)
2. El conflicto: un mapa compartido solo se actualiza cuando los robots se comunican. Si la comunicación se cae, cada robot queda con un mapa desactualizado y la "percepción compartida" deja de ser compartida.
	1. Eso puede ser mi contribución: ¿Cuánto sirve la percepción compartida cuando se degrada, y cuándo es peor que la independiente? Pero se tendría que ponerlo explícito en la pregunta, no dejarlo implícito.
3. Alcance experimental
	- Simulación: escala (decenas de robots), entrenamiento y evaluación principal.
	- Hardware: 3 a 5 rovers reales (número a fijar según presupuesto) para validar transferencia sim-to-real.
	- Qué valida el hardware: que la política se transfiere y que la degradación por comunicación limitada se parece a la de la simulación.
	- Qué NO se afirma con hardware: conclusiones de escala. Eso sale solo de la simulación.
4. Baselines: *punto de referencia para saber si la política aprendida aporta frente a lo que ya existe.*
	- Candidatos sin aprendizaje: exploración por fronteras, asignación por subasta.
	- Pregunta de evaluación: ¿le gana a los baselines, y en qué condiciones? (comunicación limitada, fallos, comunicación perfecta).
	- Reportar dónde pierde también: es un hallazgo, no un fracaso.
	- Pendiente: ver qué baselines se repiten en los papers del área (anotar 2 o 3) y definir los míos.

#### Investigación Pendiente
- [ ] ==Comunicación Limitada/intermitente en exploración multi-robot==
	- Papers que traten específicamente "limited communication", "intermittent connectivity" o "communication-aware exploration" en multi-robot systems. **Pregunta clave: Como otros han modelado esa restricción y que tan resuelto está.**
- [ ] ==Tolerancia a fallas / robustez ante pérdida de robots==
	- "Robot failure", "fault-tolerant multi robot" o "robustness to agent loss" en RL / MARL. **Pregunta clave: Confirmar si es un gap real o si hay trabajo consolidado. **
- [ ] Representación de percepción compartida (GNN) aplicada a coordinación no solo a exploración.
	- Profundizar en papers de Graph Neural Networks para exploración. Buscando específicamente si GNN se ha usado para resolver el problema de comunicación limitada / fallas.
- [ ] Métricas de evaluación pra robustez de exploración.
	- Que métrics usa la literatura para medir "robustez" o "eficiencia bajo restricción" (no solo tiempo de cobertura) . E
## Research Philosophy
- Problem
- Research Question
- Hypothesis
- System
- Experiment
- Results
- Iteration

NOT: Technology → find a reason to use it.

## Key Concepts

**Active exploration**
Robots ask: "Where would obtaining more information be most valuable?"
Prioritize areas where uncertainty is high or information gain is high.

**Robot failure as research variable**
Failure is a feature, not a bug. The system should detect and adapt.
Questions: Can robots redistribute? How much performance is lost? Does decentralized coordination improve resilience?

**Communication constraints**
Not assuming perfect communication.
Question: How much communication does the system actually need?

## Evaluation Metrics (tentative)
- % environment explored
- Exploration time
- Coverage rate
- Distance traveled / energy consumed
- Redundant exploration
- Map accuracy
- Task allocation efficiency
- Performance after robot failures
- Performance under communication loss
- Generalization to unseen environments

## Baselines to Compare Against
- Random exploration
- Greedy exploration
- Frontier-based exploration
- Classical task allocation
- Auction-based coordination
- Centralized planning
- Decentralized heuristics
