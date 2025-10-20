# 📦 Backlog Inicial APP v0.1

**Versión:** 0.1  
**Fecha:** 20/10/2025  
**Proyecto:** APP (nombre temporal: Momentum)  
**Equipo:** Sebastián Puentes Gonzalez

---

## 🔖 Estructura de columnas en GitHub Projects
- **Backlog:** tareas identificadas pero sin iniciar.  
- **En progreso:** tareas activas.  
- **En revisión:** tareas terminadas, pendientes de validación.  
- **Finalizado:** tareas completadas y validadas.  

---

## 🧩 Épica 1: Onboarding y Autenticación

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 1.1 | Diseñar flujo de registro y login (usuarios y empresas) | Alta | Backlog | Equipo | Mockups UX/UI | Basado en SRS y HU-01 |
| 1.2 | Crear pantallas de registro/login en prototipo (Figma) | Media | Backlog | Integrante 1 | 1.1 | Referencia al caso de uso CU-01 |
| 1.3 | Documentar endpoints para autenticación (backend) | Alta | Backlog | Integrante 2 | 1.1 | JWT o Firebase Auth (decidir) |

---

## 📸 Épica 2: Captura y Publicación Rápida

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 2.1 | Diseñar flujo de captura instantánea (cam front/back) | Alta | Backlog | Equipo | SRS | Inspirado en “BeReal” pero libre |
| 2.2 | Definir estructura de datos para publicación | Alta | Backlog | Integrante 2 | 2.1 | Tabla: Post, Usuario, Ubicación |
| 2.3 | Crear mockup de pantalla de captura y publicación | Media | Backlog | Integrante 1 | 2.1 | Enlace con UX/UI |

---

## 🧭 Épica 3: Exploración de contenido y lugares

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 3.1 | Diseñar pantalla principal (scroll dinámico) | Alta | Backlog | Integrante 1 | Mockups | Priorizar contenido visual |
| 3.2 | Investigar API de Google Maps o Places | Media | Backlog | Integrante 2 | 3.1 | Para geolocalización de publicaciones |
| 3.3 | Prototipar vista de recomendación de lugares | Media | Backlog | Integrante 1 | 3.2 | Integrar con datos falsos inicialmente |

---

## 👤 Épica 4: Perfil de Usuario / Empresa

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 4.1 | Diseñar perfil básico de usuario | Media | Backlog | Integrante 1 | HU-04 | Mostrar dump diarios agrupados |
| 4.2 | Diseñar perfil empresarial con catálogo | Alta | Backlog | Integrante 2 | HU-05 | Mostrar publicaciones etiquetadas |
| 4.3 | Definir roles en base de datos (user / business) | Alta | Backlog | Integrante 2 | 4.2 | Herencia de roles (seguridad) |

---

## 🧠 Épica 5: Infraestructura y Base de Datos

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 5.1 | Definir modelo de datos inicial (MER) | Alta | Backlog | Equipo | Casos de uso | Evaluar NoSQL vs SQL |
| 5.2 | Crear script inicial en `/data-base/schema.sql` | Media | Backlog | Integrante 2 | 5.1 | Usar UUIDs y auditoría |
| 5.3 | Documentar sincronización local-remota | Media | Backlog | Equipo | 5.2 | Política cache-then-network |

---

## 🎨 Épica 6: UI/UX y Prototipos

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 6.1 | Crear wireframes iniciales (Figma) | Alta | Backlog | Integrante 1 | HU-01, HU-02 | Colores neutros y foco en imagen |
| 6.2 | Diseñar logo temporal y esquema de color | Baja | Backlog | Integrante 1 | 6.1 | Placeholder por ahora |
| 6.3 | Documentar guía de diseño en `/doc/architecture/ui_guidelines.md` | Media | Backlog | Integrante 1 | 6.1 | Referencia para desarrollo posterior |

---

## 🧪 Épica 7: Pruebas y Despliegue

| ID | Tarea | Prioridad | Estado | Responsable | Dependencias | Notas |
|----|--------|------------|---------|--------------|---------------|-------|
| 7.1 | Crear plan de pruebas funcionales (Postman) | Media | Backlog | Integrante 2 | SRS | Reutilizar estructura de API |
| 7.2 | Configurar entorno QA en rama `/qa` | Alta | Backlog | Equipo | Repositorio | Validación de features |
| 7.3 | Documentar proceso de despliegue local | Media | Backlog | Integrante 2 | 7.2 | Docker + Expo CLI (según framework) |

---

## 🧭 Versión del Backlog
**v0.1 – 20/10/2025**  
- Se crea backlog base para iniciar el tablero GitHub Projects.  
- Pendiente: estimación de tiempos y prioridad final.
