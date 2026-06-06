**🌿 **Project EDEN — Hoja de Ruta de Robótica Agrícola Autónoma**
*Estado: Investigación activa + prototipo en desarrollo*

---
**Visión**:
Diseñar y construir una suite de robots autónomos para una microsociedad Solarpunk funcional. Máquinas que trabajen con el ambiente, no contra él
- Punto de partida: hardware disponible.
- Destino: robótica agrícola open-source y sostenible.

---

**Robots del Proyecto**
**EDENS ARIA** _(Actual)_ _Autonomous Radar Intelligence Array_
- Hardware: Arduino UNO, servo, HC-SR04, ESP8266
- Función: Escaneo espacial 180°, mapa de distancias en tiempo real
- Stack: Arduino / C++ / Python + matplotlib
- Aprendizaje: Servos, comunicación serial, WiFi, visualización
- Rol en EDEN: Sistema de percepción base para robótica de campo
[[EDENS ARIA]]] 
[[EDENS ARIA]]

**EDENS CERES** _(4 a 6 meses)_ Pórtico CNC agrícola

- Hardware: Raspberry Pi, Arduino, motores NEMA, panel solar
- Función: Siembra, riego, deshierbe mecánico y mantenimiento autónomo de cultivos desde un pórtico con brazo de múltiples grados de libertad
- Referencia: Farmbot.io — open source, consultado por NASA 
- Rol en EDEN: Producción de alimento autónoma y sostenible — ejecuta las acciones físicas sobre el cultivo

**EDENS ATHENA** _(12 meses)_ Monitoreo aéreo y análisis de campo

- Hardware: ROS, RTK-GPS, cámara RGB+IR, frame de dron, controladora de vuelo (Pixhawk o similar)
- Función: Monitoreo aéreo de cultivos, análisis multiespectral de suelo y vegetación, mapeo topográfico desde el aire
- Referencia: Twisted Fields, proyectos agrícolas con drones open sourc
- Rol en EDEN: Inteligencia aérea del ecosistema — visión macro del campo que complementa el reconocimiento en suelo de ARIA y guía las acciones de CERES

**EDENS ATLAS** _(Futuro lejano)_ _Robot de asistencia en campo_
- Hardware: LiDAR, ROS Nav Stack, batería intercambiable
- Función: Sigue al operario, carga herramientas, transporta cosecha
- Rol en EDEN: Extensión física del operario humano

---

**Próximos pasos**
- [ ]  Comprar ESP8266 NodeMCU — ~15-25K COP
- [ ]  Fase 1 ARIA-01: montar servo + sensor
- [ ]  Continuar investigación Solarpunk para el paper
- [ ]  Explorar documentación FarmBot
---

**Preguntas abiertas**
- ¿Qué cultivos serían prioritarios en contexto colombiano?
- ¿Cómo integrar energía solar desde ARIA-01?
- ¿Existe comunidad Solarpunk activa en Colombia?