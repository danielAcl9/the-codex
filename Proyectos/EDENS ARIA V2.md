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
