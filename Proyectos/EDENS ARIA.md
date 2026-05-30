**ARIA — Autonomous Radar Intelligence Array** 
_Proyecto: EDEN — Nivel 1_ _Estado: En construcción_

---
**Qué es?** ARIA es un rover autónomo de patrullaje continuo. Mapea el terreno agrícola, detecta cambios y obstáculos en tiempo real, y transmite inteligencia espacial al ecosistema EDEN para que los demás robots puedan actuar.

---
### Tareas


**Recurso recomendado:** YouTube — GreatScott! o Andreas Spiess para electrónica práctica orientada a proyectos reales.
---
**Pendiente / A pensar**
- [ ] Diseño final del chasis — dirección: tanqueta compacta, estilo solarpunk, amigable, curioso, redondo.
- [ ] Debe tener espacio definido para
	- [ ] Arduino+Shield, L298N, portabaterías, servo+HC-SR04, switch accesible desde el exterior, paso de cables de motores.
- [ ] Sensor: ¿por fuera como torreta expuesta o empotrado con visera? Si es empotrado, cómo gira sin obstáculos
- [ ] Migración de energía: Paso intermedio: Batería litio 18650 x2.
- [ ] Migración a energía solar: regulador de carga, batería de litio, panel solar. Pendiente calcular consumo real del sistema para dimensionar todo.
- [ ] Instalar OnShape si Fusion no convence al acabar los 30 días de prueba premium

---
### Decisiones de diseño
**ParaV1**
- Rueda loca al frente, motores atrás
- Sensor a 8-10cm del suelo para línea de visión correcta
- Barrido semicircular 180° — no fijo al frente
- Chasis en dos niveles si es necesario
- Baterías 18650 x2 en serie = 7.4V
- Switch empotrado en lateral accesible
**Para V2**
- Baúl trasero con apertura para acceso al Arduino
- Estética Solarpunk — formas orgánicas, redondeadas, amigables
**Llantas y movimiento**
- ARIA V2 → Rocker-Bogie 6 ruedas
- ARIA V3 → orugas
##### Pendiente hardware

- Conseguir pilas AA alcalinas nuevas para prueba inmediata
- Planear compra baterías 18650 x2 + porta baterías en serie + cargador
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
	- Soldar motores
	- Conectar motores al L298N
	- Conectar GND por switch y batería
	- Pendientes:
		1. Primera prueba de movimiento
		2. Reemplazar USB por WiFi
- **Fase 3 — Movimiento inteligente**
	1. Diseño nuevo base chasis en Onshape
		1. Considerando posibles 4 ruedas
	2. Conseguir cables hembra-hembra largos
		1. Implementar 4 ruedas en vez de 2
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
