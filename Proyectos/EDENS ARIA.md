**ARIA — Autonomous Radar Intelligence Array** 
_Proyecto: EDEN — Nivel 1_ _Estado: En construcción_

---
**Qué es?** Robot de percepción espacial. Escanea el entorno en 180° con sensor ultrasónico montado en servomotor y envía el mapa en tiempo real al computador vía WiFi.

---
### Cosas a pensar
- [ ] Como será el diseño final?
	- Se me ocurre tipo tanqueta cortica, sin cara ni pantallas, solo el servo y el reconocimiento.
---

**Lo que ya tengo**
- ✅ Arduino UNO
- ✅ Chasis con 2 ruedas y motores DC
- ✅ Driver de motores L298N
- ✅ Sensor ultrasónico HC-SR04
- ✅ Servomotor
- ✅ Sensor Shield v5.0
- ✅ Porta baterías

---
**Otras cosas para comprar**
- [ ] Alguna clase de soporte para el sensor. 
- [ ] Nuevo set de ruedas
- [ ] Algún tipo de cover hecho en 3d

---

**Fases de construcción**
- **Fase 1 — El radar** _(sin WiFi, con USB)_ Montar el HC-SR04 encima del servomotor, hacer que gire de 0 a 180° y leer distancias en cada ángulo. Visualizar el radar en Python en tiempo real.
	- **ARIA — Sesión Día 1 de Movilidad** _Proyecto: EDEN_
		- Radar Fase 1 completado y funcionando
		- Servo + HC-SR04 escaneando 15°-165°
		- Visualización radar en Python en tiempo real
		- Chasis ensamblado físicamente
		- Arduino + Sensor Shield + L298N + porta baterías montados
		- Conexiones: HC-SR04 a pines 9/10, Servo a pin 6, L298N a pines 2/3/4/7
- **Fase 2 — WiFi** Reemplazar el cable USB por comunicación inalámbrica. El Arduino envía datos por WiFi al computador.
	- **Pendientes:**
		- Cables hembra-hembra más largos
		- Remontar L298N definitivamente por debajo
		- Centrar servo correctamente
		- Conectar motores a OUT1-OUT4
		- Primera prueba de movimiento
- **Fase 3 — Movimiento** Integrar los motores. ARIA se mueve y escanea al mismo tiempo. Evita obstáculos basándose en su propio mapa.
- **Fase 4 — Campo** Prueba en exterior. Terreno irregular, condiciones reales.

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
![[ARIA_Wireframe.png]]![[ARIA_Mech.png]]**Mañana — ARIA + Video**

**1. Review de ARIA — 30 min**

- Estado actual del hardware: qué está conectado y qué no
- Qué funciona: radar Fase 1 ✅
- Qué falta: movimiento autónomo
- Función de ARIA en el ecosistema EDEN documentada

**2. Lista de materiales — 15 min**

- Verificar si hay cable de cobre en casa para soldar
- Anotar todo lo que falta para Fase 2
- Lista lista para comprar el miércoles

**3. Video de introducción de ARIA — 1 hora**

- Mostrar el robot en su estado actual
- Explicar su rol dentro del ecosistema EDEN
- Guión base: "This is where I start"
- Grabar en inglés, sin edición elaborada