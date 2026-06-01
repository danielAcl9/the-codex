**ARIA — Autonomous Radar Intelligence Array** 
_Proyecto: EDEN — Nivel 1_ _Estado: En construcción_

---
**Qué es?** ARIA es un rover autónomo de patrullaje continuo. Mapea el terreno agrícola, detecta cambios y obstáculos en tiempo real, y transmite inteligencia espacial al ecosistema EDEN para que los demás robots puedan actuar.

---
### Tareas
- [ ] En Fusión, subir el espacio del switch a un lateral. 
---
**Pendiente / A pensar**
- [ ] Diseño final del chasis — dirección: tanqueta compacta, estilo solarpunk, amigable, curioso, redondo.
- [ ] Debe tener espacio definido para
	- [ ] Arduino, L298N, portabaterías, servo+HC-SR04, switch accesible desde el exterior, paso de cables de motores.
- [ ] Sensor: ¿por fuera como torreta expuesta o empotrado con visera? Si es empotrado, cómo gira sin obstáculos
- [x] Migración de energía: Paso intermedio: Batería litio 18650 x2.
- [ ] Migración a energía solar: regulador de carga, batería de litio, panel solar. Pendiente calcular consumo real del sistema para dimensionar todo.
- [ ] Instalar OnShape si Fusion no convence al acabar los 30 días de prueba premium

---
### Decisiones de diseño
**ARIA V1** - Versión actual
- Rueda loca al frente, motores atrás
- Sensor a 8-10cm del suelo para línea de visión correcta
- Barrido semicircular 180°
- Chasis en dos niveles
	- Inferior: baterías + L298N
	- Superior: Arduino + ESP32
- Baterías 18650 x2 en serie = 7.4V
- Switch empotrado en lateral accesible
- Carcasa sencilla estética Solarpunk
**ARIA V2**
- Modelo con Rocker-Bogie 6 ruedas
- Baúl trasero con apertura para acceso al Arduino
- Integración panel solar.
**ARIA V3**
- Movimiento Oruga
---
# Trabajo Actual ARIA V1
**Fases de construcción**
- **Fase 1 — El radar** (Terminado) ✅
	- Servo + HC-SR04 escaneando 15°-165° con centro calibrado en 64°
	- Visualización radar en Python en tiempo real
	- Chasis ensamblado físicamente
- **Fase 2 — Movimiento básico** (Terminado) ✅
	- Motores soldados y conectados al L298N
	- Diagnóstico completado — Shield dañado, conexiones migradas directo al Arduino
	- Sistema funcionando con baterías 18650 sin USB
	- Velocidad controlada con PWN.
	- Evasión de obstáculos básica funcionando.
- **Fase 3 — Movimiento inteligente** 🟡 En progreso
	- Conexiones limpias sin Shield ✅
	- Evasión de obstáculos autónoma ✅
	- Algoritmo Boustrophedon con área predefinida
	- Mapeo 2D en tiempo real con visualización Python
- **Fase 4 — Documentación y cierre V1**
	- Diagrama de circuito en Fritzing
	- GitHub con README en inglés
	- Video final V1 funcionando
# ARIA V1 TERMINADO
### ARIA V1 — Prototipo funcional

**Entorno:** interior, superficies planas **Objetivo:** demostrar el concepto completo de ARIA funcionando

- Movimiento autónomo con evasión de obstáculos
- Mapeo 2D en tiempo real con visualización
### Criterio de graduación a V2

ARIA mapea autónomamente una habitación completa sin intervención humana.

---

### ARIA V2 — Rover de campo

**Entorno:** terreno irregular, exterior, campo agrícola **Objetivo:** sistema de percepción real para ecosistema EDEN

- Rocker-Bogie 6 ruedas con suspensión pasiva. 
- Sistema híbrido de energía — panel solar + 18650
- Mapeo 3D con altimetría — fusión de encoders + IMU
- Patrullaje autónomo con algoritmo Boustrophedon
- Evasión de obstáculos con array 3x VL53L0X
- Transmisión WiFi al ecosistema EDEN via Raspberry Pi 4
- Estética Solarpunk con personalidad visual
---

**Stack**
- Arduino C++ para el hardware
- Python + matplotlib para la visualización
---
# Ideas para el documento
Título ajustado: _"ARIA: Design and Implementation of an Autonomous Reconnaissance Rover for Agricultural Environment Mapping"_

1. **Abstract** _(escribir al final)_
2. **Introduction**
	- Problema: agricultura necesita automatización accesible, los robots deben apoyar, no reemplazar a nuestros granjeros. 
	- Solución propuesta: rover autónomo de reconocimiento para mapeo de entornos agrícolas
	- Contribución: ARIA como prueba de concepto
	- Mención breve de ecosistema mayor (EDEN) sin desarrollar
	- Estructura del documento
3. **Related Work**
	- FarmBot — pórtico CNC agrícola open source, consultado por NASA
	- Twisted Fields — robótica agrícola de campo
	- Roomba / algoritmos de cobertura — Boustrophedon
	- Rovers NASA — Curiosity como referencia de Rocker-Bogie
	- Sistemas de mapeo con HC-SR04 en robótica educativa vs aplicada
4. **System Architecture** - arquitectura de ARIA en general, no solo V1. La visión de cómo todo se conecta como sistema.
	- Visión general de ARIA — qué es, qué hace
	- Diagrama de bloques del sistema
		![[Pasted image 20260531172729.png]]
	- Decisiones de diseño y justificación de cada componente
		- Por qué elegiste esta arquitectura. Ejemplos:
			- Por qué Arduino y no Raspberry Pi
			- Por qué HC-SR04 y no LiDAR
			- Por qué L298N y no otro driver
		- Stack tecnológico: Arduino / C++ / Python + matplotlib
5. **Hardware Design** - qué hace cada componente en el contexto de ARIA y por qué lo usaste. Luego el diagrama de circuito lo complementa visualmente. Para cada componente: Qué es, qué hace en ARIA, por qué este y no otro. Es selección y justificación de hardware, no diseño desde cero.
	- Arduino UNO — hub de control
	- HC-SR04 + servo SG90 — sistema de radar
	- L298N — driver de motores
	- Motores TT — locomoción
	- Baterías 18650 x2 — sistema de potencia
	- ESP32 — comunicación WiFi
	- Diagrama de circuito (Fritzing)
		- **Diagrama V1** — "Estado inicial del prototipo"
			- Arduino UNO
			- HC-SR04 pines 9/10, Servo pin 6
			- L298N con pines 2/3/4/7
			- Baterías 18650
		- **Diagrama V2** — "Implementación final"
			- Arduino UNO directo sin Shield
			- HC-SR04, Servo, L298N con pines actuales
			- Baterías 18650 x2
			- ESP32
			- Hardware adicional de V2 cuando esté definido
	- **V1: hardware actual con justificación**
	- **V2: hardware propuesto con justificación del upgrade**
6. **Software Design**
	- Diagrama de flujo general
	- Módulo de radar — barrido 180°, calibración centro en 64°
	- Módulo de movimiento — control PWM, compensación de deriva
	- Módulo de evasión de obstáculos — lógica de decisión
	- Algoritmo Boustrophedon — cobertura de área predefinida
	- Visualización en Python + matplotlib
	- Comunicación serial
7. **Implementation**
	- Dos fases reales:
		- V1: prototipo inicial, pruebas en interior
		- V2: Rocker-Bogie, encoders, panel solar, campo real
8. **Results and Discussion**
	- Resultado Fase 1: radar funcional con visualización en tiempo real
	- Resultado Fase 2: movimiento autónomo sin USB con 18650
	- Resultado Fase 3: evasión de obstáculos funcionando
	- Resultado Fase 4: cobertura Boustrophedon en área predefinida
	- Limitaciones: odometría por tiempo sin encoders, deriva acumulada
	- Discusión: qué funcionó, qué se cambiaría
		- **Resultados de ambas versiones**
9. **Conclusions **
	- ARIA como sistema validado, mención de EDEN como siguiente paso
	- Limitaciones documentadas y actuales.
	- Visión del ecosistema EDEN — ARIA como pilar de percepción
10. **References**
	- FarmBot documentation
	- HC-SR04 datasheet
	- L298N datasheet
	- Literatura de algoritmos Boustrophedon
	- Papers de robótica agrícola relevantes