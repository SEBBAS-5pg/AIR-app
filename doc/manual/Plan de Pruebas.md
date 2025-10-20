# Momentum - Plan de Pruebas

## 📋 Información General

- **Proyecto**: Momentum (Red Social de Fotos Espontáneas Geolocalizadas)
- **Versión**: 1.0 (Plan de Pruebas Detallado)
- **Fecha**: 20 de Octubre de 2025
- **Responsable**: Documentador Líder / Equipo QA

## 🎯 Introducción y Alcance

### 1.1. Objetivo del Plan

Asegurar que el Producto Mínimo Viable (MVP) de Momentum cumple con los 16 Requerimientos Funcionales (HU), los 8 Casos de Uso (UC) y los 6 Requerimientos No Funcionales (RNF) especificados en la documentación del proyecto.

### 1.2. Alcance

El enfoque es la prueba de caja negra (funcionalidad de usuario) y la verificación del backend (seguridad y rendimiento). Las pruebas se realizarán a nivel de Sistema, Integración y Rendimiento.

## 🚀 Estrategia de Pruebas

### 2.1. Metodología

Las pruebas se ejecutan de manera Iterativa dentro de los Sprints. La priorización sigue la matriz de riesgos:

- **Crítico**: Publicación, Seguridad, Autenticación
- **Alta**: Feed, Carga, Interacciones Sociales
- **Media**: Gestión de Perfil, Notificaciones Secundarias

### 2.2. Criterios de Finalización (Exit Criteria)

- Ejecución del 100% de los Casos de Prueba Críticos y Altos
- Tasa de Éxito ≥ 95% en los Casos de Prueba Críticos
- Cumplimiento del 100% de los RNF (RNF-001 al RNF-006)
- No hay bugs de prioridad Alta o Crítica en el Backlog

## ⚙️ Entorno y Herramientas

| Componente | Configuración | Justificación |
|------------|---------------|---------------|
| **Front-end** | Android 12+ (Emulador) / iOS 16+ (Simulator) | Cubrir los SO móviles dominantes |
| **Simulación de Red** | Simulación de red 3G/4G | Pruebas de Rendimiento (RNF-001) |
| **Herramientas QA** | Consola de Firebase (Logs, Auth, Rules) | Verificación de seguridad y datos del backend |

## 🧪 Tipos de Pruebas

| Tipo de Prueba | Objetivo de Verificación | Requisitos Clave |
|----------------|--------------------------|------------------|
| **Funcional (Sistema)** | La aplicación se comporta como lo dictan las HU y UC | Todas las HU (HU-001 a HU-016) |
| **No Funcional: Rendimiento** | Carga rápida de la interfaz y recursos | RNF-001, RNF-002 |
| **No Funcional: Seguridad** | Verificación de reglas de acceso de Firebase y protección de datos | RNF-003, RNF-004 |
| **No Funcional: Usabilidad** | Flujo intuitivo, cumplimiento de touch targets y accesibilidad (UX) | RNF-006 |
| **Integración** | Verificación de la comunicación entre React (Front-end) y Firebase (Back-end) | UC-002, UC-004 |

## 📊 Casos de Prueba Detallados (Trazabilidad)

Se listan los casos de prueba esenciales, trazando directamente a los requerimientos:

### Módulo A: Autenticación y Perfil (UC-000, UC-005)

| CP ID | Requisito Trazado | Descripción del Caso de Prueba | Resultado Esperado | Prioridad |
|-------|-------------------|--------------------------------|-------------------|-----------|
| **CP-A01** | HU-012 | Registrarse con datos válidos | El usuario es creado en Firebase Auth y Firestore; es redirigido al Feed | Crítica |
| **CP-A02** | RNF-003 | Intentar leer data de un usuario sin estar autenticado | Error 403 (Permiso Denegado) en Firebase (Seguridad) | Crítica |
| **CP-A03** | UC-005 | Verificar historial de dumps en el perfil | Los dumps se cargan y se agrupan correctamente por fecha y hora (según HU-013) | Media |

### Módulo B: Captura y Publicación (UC-001, UC-002, UC-006)

| CP ID | Requisito Trazado | Descripción del Caso de Prueba | Resultado Esperado | Prioridad |
|-------|-------------------|--------------------------------|-------------------|-----------|
| **CP-B01** | HU-001, RNF-002 | Pulsar el botón de cámara y medir el tiempo de acceso | La cámara abre en menos de 500ms (RNF-002) | Crítica |
| **CP-B02** | HU-002, HU-004 | Tomar foto, publicar y verificar el GeoPoint y el rango de tiempo | El documento de Firestore contiene geoPoint y el timeRange calculado es preciso | Crítica |
| **CP-B03** | HU-006 | Tomar un dump con la cámara dual activada | Una sola publicación aparece en el Feed, con la imagen compuesta correctamente | Alta |
| **CP-B04** | UC-006 | Etiquetar un Negocio y Publicar | El campo businessId en el documento de Firestore contiene el ID correcto del Negocio | Alta |

### Módulo C: Feed y Social (UC-003, UC-004, UC-007, UC-008)

| CP ID | Requisito Trazado | Descripción del Caso de Prueba | Resultado Esperado | Prioridad |
|-------|-------------------|--------------------------------|-------------------|-----------|
| **CP-C01** | RNF-001, UC-003 | Medir la carga inicial del Feed en un entorno 3G simulado | La carga inicial del Feed se completa en menos de 2.5 segundos (RNF-001) | Crítica |
| **CP-C02** | HU-007, HU-008 | Verificar la prioridad de posts en el Feed | Los posts de seguidores deben aparecer antes que los posts locales | Alta |
| **CP-C03** | HU-011 | Dar "Me Gusta" a un post y recargar la aplicación | El contador de likes se incrementa y el estado del botón se persiste | Alta |
| **CP-C04** | HU-015, UC-007 | Ver el perfil de un Negocio etiquetado | Se muestra la información del negocio Y la galería dinámica de dumps de la comunidad | Media |
| **CP-C05** | HU-016, UC-008 | Verificar notificación del Negocio tras ser etiquetado | El Usuario Empresarial recibe una notificación push (o interna) con el mensaje correcto | Media |

### Módulo D: Usabilidad (RNF-006)

| CP ID | Requisito Trazado | Descripción del Caso de Prueba | Resultado Esperado | Prioridad |
|-------|-------------------|--------------------------------|-------------------|-----------|
| **CP-D01** | RNF-006 | Inspeccionar el tamaño del botón de Cámara y Me Gusta | El área de toque (touch target) debe ser igual o superior a 44x44 dp | Media |
| **CP-D02** | HU-009 | Pulsar la etiqueta de ubicación en un dump | Se abre una vista de mapa o se copia la dirección al portapapeles | Media |

## ✅ Resumen de Pruebas

El cumplimiento de este plan garantiza la estabilidad de la aplicación y la satisfacción del cliente al verificar que el producto cumple con los requisitos definidos en la fase de análisis.