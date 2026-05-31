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
	- Integrar ESP32 WiFi con 18650
	- Algoritmo Boustrophedon con área predefinida
	- Radar + movimiento integrados con barrido al detenerse
	- Mapeo 2D en tiempo real con visualización Python
- **Fase 4 — Documentación y cierre V1**
	- Pruebas documentadas en entorno controlado
	- Diagrama de circuito en Fritzing
	- GitHub con README en inglés
	- Video final V1 funcionando
# ARIA V1 TERMINADO
### ARIA V1 — Prototipo funcional

**Entorno:** interior, superficies planas **Objetivo:** demostrar el concepto completo de ARIA funcionando

- Movimiento autónomo con evasión de obstáculos
- Mapeo 2D en tiempo real con visualización
- Transmisión WiFi de datos
### Criterio de graduación a V2

ARIA mapea autónomamente una habitación completa sin intervención humana.

---

### ARIA V2 — Rover de campo

**Entorno:** terreno irregular, exterior, campo agrícola **Objetivo:** sistema de percepción real para ecosistema EDEN

- Rocker-Bogie 6 ruedas
- Panel solar integrado
- Mapeo 2D de campo agrícola
- Patrullaje autónomo de área definida
- Transmisión WiFi al ecosistema
---

**Stack**
- Arduino C++ para el hardware
- Python + matplotlib para la visualización
