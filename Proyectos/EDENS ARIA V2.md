1. Diseño
- Chasis Rocker-Bogie de 6 ruedas — inspirado en rovers NASA
- Estética Solarpunk — formas orgánicas, amigables, no intimidantes
- Arquitectura modular — piezas intercambiables entre versiones
- Baúl trasero accesible para mantenimiento
- Integración de panel solar desde el diseño, no como parche
- Modelado en Fusion 360, impresión 3D en PLA
- Pantalla OLED o LEDs expresivos — interfaz visual de personalidad, no funcional

---
2. Mecánica
- 6 motores TT — los dos intermedios con Encoders integrados.
- Suspensión Rocker-Bogie pasiva — adaptación a terreno irregular
- Servo SG90 — movimiento de "cabeza" para expresión visual, coherente con estética Solarpunk amigable

---

3. Electrónica

- Raspberry Pi 4 — cerebro principal, lógica pesada, ROS
- Arduino UNO — control de hardware en tiempo real
- Protocolo de comunicación Raspberry Pi ↔ Arduino (I2C o Serial)
- 3x TB6612FNG — driver para 6 motores con PWM preciso
- 3x VL53L0X — sensores ToF, cobertura frontal, izquierda y derecha
- IMU MPU6050 — medición de inclinación y orientación para altimetría
- Sistema híbrido de energía: panel solar + 18650 x2 + módulo de carga

---

4. Programación

- ROS (Robot Operating System) como framework principal
- Odometría precisa con encoders — distancia y posición real
- Algoritmo Boustrophedon autónomo — descubre el área solo
- Mapeo 3D con altimetría — fusión de odometría + IMU
- Evasión de obstáculos mejorada
- Transmisión de datos WiFi al ecosistema EDEN via Raspberry Pi 4
- Stack: ROS / Python / C++ / Arduino
---
## Lista de compras ARIA V2

**Cerebro:**
- Raspberry Pi 4 (2GB) → ~350.000 COP

**Motores y drivers:**
- 4 motores TT adicionales → ~40.000 COP
- 2 encoders ópticos IR (ruedas intermedias) → ~16.000 COP
- 3x TB6612FNG → ~42.000 COP

**Sensores:**
- 3x VL53L0X → ~45.000 COP
- IMU MPU6050 → ~8.000 COP

**Energía:**
- Panel solar 6V 500mA+ → ~35.000 COP
- Módulo de carga solar → ~20.000 COP
- MicroSD 32GB clase 10 → ~30.000 COP

**Diseño y estructura:**
- Impresión 3D chasis Rocker-Bogie → ~120.000 COP
- Pantalla OLED pequeña → ~15.000 COP

**Miscelánea:**
- Cables, tornillos, standoffs → ~25.000 COP

**Total estimado: ~746.000 COP**