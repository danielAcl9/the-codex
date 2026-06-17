[[PROYECTOS]]
[[EDENS ARIA V2]]

---

**Semana 1 — Cerrar ARIA V1**

- Necesario para: tener base documentable antes de empezar V2
- Tareas:
    - [x] Boustrophedon con área predefinida funcionando
    - [x] Mapeo 2D con visualización Python corriendo
	    - [x] Antes de: Cambiar el cable y arreglar por qué no lo reconoce. 
    - [x] Entregable: ARIA patrulla autónomamente una habitación

---

**Semana 2 — Arquitectura y esquemas V2**

- Necesario para: saber exactamente qué comprar, cómo se conecta todo, definir modularidad antes de gastar un peso
- Tareas:
    - [x] Diagrama de bloques del sistema V2 completo
    - [ ] Definir arquitectura modular — qué es intercambiable entre versiones
    - [x] Comprar: Raspberry Pi 4 + MicroSD
    - [ ] Documentación V1: GitHub + README + video V1
    - [ ] A Beginner's Guide to Autonomous Robots — 1 hora, gratis, perfecto para arrancar -> https://learn.nvidia.com/courses/course-detail?course_id=course-v1:DLI+S-OV-35+V1

---

**Semana 3 — Raspberry Pi + ROS + 6 motores sin chasis**

- Necesario para: validar que toda la electrónica funciona antes de imprimir nada físico
- Tareas:
    - [x] Instalar Ubuntu + ROS en Raspberry Pi 4 (Se instala en el RPi, no en mi computador)
    - [ ] Comunicación RPi ↔ Arduino funcionando
    - [ ] Comprar: 4 motores TT + 3x TB6612FNG + encoders IR
    - [ ] Primer nodo ROS controlando los 6 motores sobre mesa
    - [ ] Paper: Introduction + Related Work
    - [ ] **Modern Robotics:** Empezar el curso en paralelo, 1 capítulo por semana con lectura de fondo. https://www.youtube.com/watch?v=jVu-Hijns70&list=PLggLP4f-rq02vX0OQQ5vrCxbJrzamYDfx
    - [ ] Getting Started: Simulating Your First Robot in Isaac Sim — 1.5 horas, gratis -> https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/building-your-first-robot-in-isaac-sim/index.html

---

**Semana 4 — Sensores integrados con ROS sin chasis**

- Necesario para: validar stack electrónico completo antes de diseñar el chasis
- Tareas:
    - [ ] Comprar: 3x VL53L0X + MPU6050
    - [ ] VL53L0X publicando distancias en ROS
    - [ ] MPU6050 publicando inclinación en ROS
    - [ ] Evasión de obstáculos básica con array ToF sobre mesa
    - [ ] Paper: System Architecture + Hardware Design
    - [ ] **Ingesting Robot Assets and Simulating Your Robot in Isaac Sim** — 1 hora, gratis — importas el modelo de ARIA que diseñaste en Fusion -> https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/ingesting-robot-assets-and-simulating-your-robot-in-isaac-sim/index.html

---

**Semana 5 — Diseño CAD con medidas reales**

- Necesario para: diseñar el chasis con dimensiones exactas ya validadas sin sorpresas al imprimir
- Tareas:
    - [ ] Diseño Rocker-Bogie completo en Fusion 360 con medidas reales
    - [ ] Diseño modular — nivel inferior, superior, sistema snap fit
    - [ ] Enviar a imprimir
    - [ ] Paper: Software Design
    - [ ] Esquema de conexiones RPi ↔ Arduino ↔ motores ↔ sensores
    - [ ] Diseñar PBC Personalizada en KiCad
    - [ ] Enviara fabricar (ver si consigo una fábrica local, si no, JLCPCB)
    - [ ] **Developing Robots with SIL in Isaac Sim** — 2 horas, gratis-> https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/developing-robots-with-sil-in-isaac-sim/index.html

---

**Semana 6 — Ensamblaje físico completo**

- Necesario para: tener ARIA V2 físico completo con toda la electrónica validada montada en el chasis
- Tareas:
    - [ ] Recibir impresión y ensamblar chasis Rocker-Bogie
    - [ ] Montar toda la electrónica en el chasis nuevo
    - [ ] Verificar que todo funciona igual que sobre la mesa
    - [ ] Paper: Implementación V1
    - [ ] - **An Introduction to AI-Based Robot Development with Isaac ROS** — 30 min, gratis -> https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-ros/latest/an-introduction-to-ai-based-robot-development-with-isaac-ros/index.html

---

**Semana 7 — Navegación autónoma con encoders**

- Necesario para: que ARIA V2 descubra el área solo sin que tú definas las dimensiones
- Tareas:
    - [ ] Encoders calibrados, odometría real funcionando
    - [ ] Boustrophedon autónomo — ARIA descubre el área solo
    - [ ] Pruebas de navegación en interior
    - [ ] Paper: Implementación V2
    - [ ] - **Leveraging ROS 2 and HIL in Isaac Sim** — 2 horas, gratis -> https://docs.nvidia.com/learning/physical-ai/getting-started-with-isaac-sim/latest/leveraging-ros-2-and-hil-in-isaac-sim/index.html

---

**Semana 8 — Mapeo 3D + energía solar**

- Necesario para: completar las dos funcionalidades clave que diferencian V2 de V1
- Tareas:
    - [ ] Comprar: panel solar + módulo de carga
    - [ ] Fusión encoders + IMU generando mapa 3D con altimetría
    - [ ] Sistema híbrido solar + 18650 funcionando
    - [ ] Paper: Resultados y discusión
    - [ ] - **Develop, Simulate and Deploy Robot Intelligence with General Robotics** — 1 hora, gratis -> https://docs.nvidia.com/learning/physical-ai/going-further-with-robotics/latest/develop-simulate-and-deploy-intelligence-with-general-robotics/index.html

---

**Semana 9 — Prueba de campo exterior**

- Necesario para: validar que ARIA V2 funciona en el entorno real para el que fue diseñado
- Tareas:
    - [ ] Primera prueba en terreno irregular exterior
    - [ ] Ajustes de navegación según resultados reales
    - [ ] Grabación video final V2 en campo
    - [ ] Paper: Conclusiones y trabajo futuro
    - [ ] - **Software-in-the-Loop Testing for Robots** — 2 horas, gratis -> https://docs.nvidia.com/learning/physical-ai/going-further-with-robotics/latest/digital-twin-robotics/index.html

---

**Semana 10 — CERES arranca + portafolio ARIA**

- Necesario para: cerrar ARIA completamente y arrancar CERES con tiempo suficiente
- Tareas:
    - [ ] Definir 4 pilares de CERES con hardware y stack
    - [ ] Investigación FarmBot y referencias académicas
    - [ ] GitHub ARIA pulido — README, código, diagramas, Fritzing
    - [ ] Paper ARIA revisión final formato IEEE

---

**Semana 11 — CERES concepto + Statement of Purpose**

- Necesario para: tener el portafolio narrativo listo antes de contactar profesores
- Tareas:
    - [ ] Diseño estructural básico de CERES en Fusion 360
    - [ ] Lista de componentes y presupuesto CERES
    - [ ] Statement of Purpose primera versión completa
    - [ ] Identificar 3 profesores objetivo en KAIST

---

**Semana 12 — Cierre y aplicación**

- Necesario para: enviar la aplicación con todo el portafolio completo
- Tareas:
    - [ ] Video ARIA V2 editado profesionalmente
    - [ ] Email a profesores KAIST con paper + portafolio
    - [ ] Aplicación KAIST enviada
    - [ ] CERES V1 en progreso como evidencia de continuidad