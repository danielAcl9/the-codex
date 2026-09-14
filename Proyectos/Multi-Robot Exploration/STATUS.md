# Project Status

## Current Phase
Problem-discovery / Research-definition

## This Week
- [ ] Literature review: "multi-robot exploration reinforcement learning" (2021-2025)
	- [ ] Lun-Mar: Cerrar literatura _(problema que resuelve, limitaciones de su approach, qué deja abierto. No revisar todo sino lo que llame la atención. No avanzar a research question hasta tener todos anotados.)_
	- [ ] Mar-Mié: Síntesis y gap-finding _(Con todas las notas juntas, buscar patrones: ¿qué limitación se repite entre papers? ¿qué combinación de restricciones (comunicación limitada + batería + fallas de robot) nadie ha atacado bien?)_
	- [ ] Mié-Jue: Formular research question _(Redactar la pregunta específica en 1-2 frases, más una hipótesis comprobable. Debe ser lo suficientemente concreta para diseñar un experimento, no un tema general. Revisarla contra el filtro: ¿esto se puede responder con el hardware y tiempo que tengo?)_
	- [ ] Jue-Vie: Arrancar Phase 0 de simulación _(Solo una vez la research question esté escrita: montar el esqueleto del entorno de simulación en Python puro: mapa simple, 1-2 agentes, loop básico de exploración. No metas RL todavía, solo que el mundo y los robots existan y se muevan.)_
	- [ ] Fin de semana: Buffer + revisión _(Usar el tiempo extra de fin de semana para lo que se atrasó entre semana, o, empezar a bocetar qué política de exploración simple (baseline, tipo frontier-based) que se usará como punto de comparación antes de meter aprendizaje.)_
- [ ] Literature review: "cooperative exploration unknown environment neural network" (2022-2025)

## Bloqueos actuales
- Pregunta de investigación exacta no definida, depende de la literatura

## Last Session
- 13 September 2026
- Redefinición completa del proyecto
- Descartado ARIA como proyecto principal agrícola
- Nuevo eje: autonomous multi-robot exploration + learning-based coordination
- Documento central del proyecto redactado

## Decisions Made
- El proyecto es una plataforma de exploración multi-robot
- El hardware existente (RPi, Arduino, motores, encoders, MPU6050) sigue siendo válido
- Simulación primero, hardware después
- Pregunta de investigación: encontrarla en la literatura, no inventarla

## Open Questions
- Exact research question and scientific gap
- Exact neural architecture
- Exact learning paradigm
- Exact number of robots
- Exact sensors beyond current hardware
- Exact application domain
- Exact experimental environment
