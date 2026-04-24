[[Proyecto EDEN]]

### Filtro de diseño (todo robot debe cumplirlo)
Open-source · Modular · Fabricable localmente (3D print / CNC básica) · Energía solar · Reparable por no-expertos

---
### Los robots necesarios

| Robot                            | Función                                                   | Stack                                                         | Estado                                                                                                                                                                                                                                            |
| -------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **FarmBot** (pórtico CNC)        | Siembra, riego, deshierbe autónomo en camas               | Raspberry Pi, Arduino, motores NEMA, solar                    | Existe y es open-source. NASA lo consultó para producción de alimento en Marte. [Springer](https://link.springer.com/article/10.1007/s44430-025-00006-0)                                                                                          |
| **Rover agrícola**               | Patrullaje, análisis de suelo, deshierbe mecánico         | ROS, RTK-GPS, cámara RGB+IR, chasis CNC                       | Proyectos como Twisted Fields: fabricado con cortadora plasma, diseñado para operar en lluvia y corrosión. [Medium](https://medium.com/@singularitynetambassadors/unleashing-the-potential-of-open-source-autonomous-farming-rovers-9a5988003aa6) |
| **Brazo de cosecha suave**       | Cosecha de frutos sin daño                                | Soft robotics (silicona fundida), visión local en Jetson Nano | Prototipos funcionales, aún en maduración                                                                                                                                                                                                         |
| **Robot de tuberías**            | Inspección de red hídrica e hidropónica                   | Impresión TPU, sensores pH/EC, cámara endoscópica             | Investigación activa                                                                                                                                                                                                                              |
| **Brazo de taller**              | Soldar, fresar, reparar otros robots                      | AR2/AR3 open-source, servos, GRBL/ROS                         | Construible hoy por ~$500 USD                                                                                                                                                                                                                     |
| **Impresora 3D + recicladora**   | Producir piezas de reemplazo con plástico local           | ProtoCycler+ open-source, Arduino                             | Existe y funcional                                                                                                                                                                                                                                |
| **Robot de asistencia en campo** | Carga herramientas, sigue al operario, transporta cosecha | LiDAR, ROS Nav Stack, batería intercambiable                  | Componentes maduros, integración DIY posible                                                                                                                                                                                                      |

---
### Orden de adopción lógico
**Impresora 3D → FarmBot → Rover → todo lo demás.** Sin la impresora, cualquier robot roto es chatarra permanente.
### Punto central
El stack completo existe hoy en forma open-source. El problema no es tecnológico — es documentación, comunidad y voluntad de construirlo. **ROS** es el sistema nervioso común de todo el ecosistema.
**Conexión clave con el paper:** estos robots no reemplazan roles humanos, los liberan de carga física. Eso es exactamente la propuesta de valor de la micro-sociedad solarpunk.