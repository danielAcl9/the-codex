[[PROYECTOS]]

---
### Ideas de mejora
- [ ] Añadirle cantidad de vasos o termos tomados en el día. 
- [ ] Mejorar las visualizaciones, que sea una barra que se vaya llenando

---
Construir una web app simple de tracking de macros para uso personal, que pueda usar desde mi celular.

Contexto:
- Solo para mí, no necesita login ni multi-usuario
- Registro manual de alimentos, sin base de datos externa
- Trackea: calorías, proteína, carbos y grasa por día
- Se publicará en GitHub Pages para acceder desde el celular

Metas diarias hardcodeadas:
- Calorías: 3,500
- Proteína: 155g
- Carbos: 420g
- Grasa: 95g

Stack: HTML, CSS y JavaScript vanilla. Sin frameworks.

Lo importante: 
- Entender qué estoy haciendo y por qué en cada paso.
- Entender las decisiones técnicas, no solo recibir código 
- MVP primero: agregar alimentos manualmente, ver resumen del día con progreso vs metas 
- Después del MVP mejoramos
---
### Flujo de la app

```
Usuario abre la app
       ↓
JS lee la fecha de hoy → busca esa clave en localStorage
       ↓
Renderiza los alimentos del día + calcula totales
       ↓
Usuario llena el formulario y presiona "Agregar"
       ↓
JS crea el objeto, lo guarda en localStorage, re-renderiza
```

