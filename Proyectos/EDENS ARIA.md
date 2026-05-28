**ARIA — Autonomous Radar Intelligence Array** 
_Proyecto: EDEN — Nivel 1_ _Estado: En construcción_

---
**Qué es?** ARIA es un rover autónomo de patrullaje continuo. Mapea el terreno agrícola, detecta cambios y obstáculos en tiempo real, y transmite inteligencia espacial al ecosistema EDEN para que los demás robots puedan actuar.

---
### Tareas
**Mañana**
- [ ] Hacer pruebas con las nuevas baterías. 
- [ ] Hacer plan de acción si no sirven.
- [ ] Instalar Onshape
- [ ] Diseñar soporte del servomotor en CAD
- [ ] Antes de diseñar: decidir si el servo necesita girar o puede quedarse fijo

---
**Pendiente / A pensar**
- [ ] Diseño final del chasis — dirección: tanqueta compacta, sin pantallas, solo servo y sensores
- [ ] Migración a energía solar: regulador de carga, batería de litio, panel solar. Pendiente calcular consumo real del sistema para dimensionar todo.
---

**Fases de construcción**
- **Fase 1 — El radar** _(sin WiFi, con USB)_ Montar el HC-SR04 encima del servomotor, hacer que gire de 0 a 180° y leer distancias en cada ángulo. Visualizar el radar en Python en tiempo real.
	- **ARIA — Trabajo realizado
		- Radar Fase 1 completado y funcionando
		- Servo + HC-SR04 escaneando 15°-165°
		- Visualización radar en Python en tiempo real
		- Chasis ensamblado físicamente
		- Arduino + Sensor Shield + L298N + porta baterías montados
		- Conexiones: HC-SR04 a pines 9/10, Servo a pin 6, L298N a pines 2/3/4/7
- **Fase 2 — Conexión básica**
	1. Soldar motores
	2. Conectar motores al L298N
	3. Conectar GND por switch y batería
	4. Primera prueba de movimiento
	5. Reemplazar USB por WiFi
- **Fase 3 — Movimiento inteligente**
	1. Diseño nuevo base chasis en Onshape
	2. Conseguir cables hembra-hembra largos
	3. Integrar motores + radar simultáneamente
	4. Evitación de obstáculos basada en mapa
- **Fase 4 — Campo**
	1. Diseñar chasis completo
	2. Prueba en terreno irregular
---

**Stack**
- Arduino C++ para el hardware
- Python + matplotlib para la visualización

---
![[ARIA_PROTO1.png]]

autonomous agricultural robotics | ARIA robot | real-time radar map | 2WD chassis | ultrasonic sensor scanning

## ARIA Radar Robot

The ARIA Radar Robot is an autonomous agricultural robotics platform featuring a 2WD chassis. It utilizes an ultrasonic sensor, mounted on a pan servo, to scan its surroundings and generate a real-time radar map, controlled by an Arduino UNO.

| Category   | Parts | Cost   |
| ---------- | ----- | ------ |
| Electrical | 8     | $54.50 |
| Mechanical | 7     | $24.66 |
| Total      | 15    | $79.16 |
![[ARIA_Wireframe.png]]![[ARIA_Mech.png]]
