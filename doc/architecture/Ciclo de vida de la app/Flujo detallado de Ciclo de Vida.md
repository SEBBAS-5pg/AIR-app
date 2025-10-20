# Flujo Detallado del Ciclo de Vida del Proyecto 

El proyecto sigue un **modelo de desarrollo Ágil e Iterativo**, con un enfoque en ciclos de retroalimentación cortos y mejora continua, conforme a las fases requeridas:

---

## 1. Análisis y Planificación

Esta fase inicial sienta las bases del proyecto, respondiendo a la pregunta:  
**¿Qué vamos a construir y por qué?**

### 🔹 Descubrimiento & Visión
- Identificación del problema: *exceso de curación en redes, falta de contexto de ubicación*.  
- Definición de la solución: *app de photo-dump geolocalizada*.

### 🔹 Requerimientos (Funcionales/No Funcionales)
- Creación del documento **SRS (IEEE 830)**.  
- Definición de **Historias de Usuario (RF)** y atributos de calidad (**RNF**).

### 🔹 Roadmap & Backlog (Priorización)
- Creación y organización de tareas en el **tablero de GitHub Projects**.  
- Definición de las funcionalidades del **Producto Mínimo Viable (MVP)**.

---

## 2. Diseño UX/UI

Define la experiencia del usuario y la estructura técnica antes de la codificación.

### 🔹 UX/UI (Wireframes, Mockups, Prototipo)
- Creación de la interfaz de usuario en **Figma**.  
- Diseño limpio y centrado en las imágenes (*dumps*).  
- Flujo de cámara rápido y fácil de usar.

### 🔹 Arquitectura & Setup (Repos, CI/CD, Estándares)
- Configuración del entorno de desarrollo (**Ionic/React** y **Firebase**).  
- Definición del **Modelo de Datos NoSQL (MER)**.  
- Establecimiento de la estructura de ramas: `main`, `develop`.

---

## 3. Desarrollo

Fase de codificación, organizada en ciclos de tiempo definidos.

### 🔹 Desarrollo Iterativo (Sprints)
- El equipo trabaja en **ciclos cortos (Sprints)** para construir las Historias de Usuario priorizadas.  
- Uso de la rama `develop` como rama de integración principal.

---

## 4. Pruebas

Verificación continua de la calidad del producto desarrollado.

### 🔹 Testing (Unitario, Integración, Usabilidad, Accesibilidad)

**Unitario:**  
Pruebas al código de React/Ionic (ej. lógica de scroll o servicios de Firebase).

**Integración:**  
Verificación de la comunicación entre frontend y backend (publicar una foto y verla en el feed).

**Usabilidad:**  
Evaluación del flujo del usuario (*¿Es rápido tomar y publicar la foto?*).

### 🔹 Criterios de Aceptación + DoD

- **Punto de control:** Se verifica si la funcionalidad cumple con lo acordado.  
- **Si NO:** Se ajustan errores y se regresa al Desarrollo Iterativo.

---

## 5. Despliegue

Entrega del producto a un entorno de usuario.

### 🔹 Release (Beta → Prod)
- Una vez cumplidos los criterios, el código de `develop` se fusiona con `main`.  
- Se empaqueta y publica (App Store / Google Play).  
- En este contexto universitario, representa la **entrega final del artefacto ejecutable**.

---

## 6. Mantenimiento

Trabajo posterior al lanzamiento para garantizar la salud y evolución del producto.

### 🔹 Observabilidad (Logs, Métricas, Crashlytics)
- Monitoreo del comportamiento en producción usando **Firebase Crashlytics**.  
- Detección de errores, caídas y fallas de rendimiento.

### 🔹 Mantenimiento & Mejora Continua
- Corrección de bugs detectados.  
- Implementación de mejoras o nuevas funcionalidades.  
- Inicia un nuevo ciclo de **Análisis y Planificación** para la versión **2.0**.

---
