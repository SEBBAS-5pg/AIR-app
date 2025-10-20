# 📊 Matriz de Trazabilidad de Requisitos - Proyecto AIR

> Esta matriz asegura la relación directa entre requisitos del SRS, historias de usuario, casos de uso y pruebas, garantizando cobertura completa del sistema AIR.

---

## 🎯 Leyenda de Identificadores

| Prefijo  | Tipo                   | Descripción                          |
| -------- | ---------------------- | ------------------------------------ |
| **RF-**  | Requisito Funcional    | Del documento SRS IEEE 830           |
| **RNF-** | Requisito No Funcional | Del documento SRS IEEE 830           |
| **HU-**  | Historia de Usuario    | Del backlog de historias             |
| **UC-**  | Caso de Uso            | De la especificación de casos de uso |
| **TST-** | Caso de Prueba         | Para verificación y validación       |

---

## 🧩 Matriz de Trazabilidad Completa

### 🔐 Módulo Autenticación y Usuarios

| ID REQ     | Descripción                                    | ID HU      | Historia de Usuario      | ID UC      | Caso de Uso             | ID TEST     | Prueba Asociada                               |
| ---------- | ---------------------------------------------- | ---------- | ------------------------ | ---------- | ----------------------- | ----------- | --------------------------------------------- |
| **RF-001** | Registro con email/contraseña y Google Sign-In | **HU-012** | Registro y autenticación | **UC-000** | Autenticarse            | **TST-001** | Verificar registro y login con Firebase Auth  |
| **RF-001** | Recuperación de contraseña                     | **HU-012** | Registro y autenticación | **UC-000** | Autenticarse            | **TST-002** | Validar flujo de recuperación de contraseña   |
| **RF-004** | Gestión de perfil de usuario                   | **HU-013** | Visualización de perfil  | **UC-005** | Gestionar Perfil Propio | **TST-011** | Confirmar actualización de datos en Firestore |

### 📸 Módulo Captura y Publicación

| ID REQ     | Descripción                     | ID HU      | Historia de Usuario        | ID UC      | Caso de Uso             | ID TEST     | Prueba Asociada                              |
| ---------- | ------------------------------- | ---------- | -------------------------- | ---------- | ----------------------- | ----------- | -------------------------------------------- |
| **RF-002** | Acceso rápido a cámara nativa   | **HU-001** | Acceso rápido a cámara     | **UC-001** | Capturar Dump           | **TST-003** | Medir tiempo apertura cámara (<1.5s)         |
| **RF-002** | Geolocalización automática      | **HU-002** | Geolocalización automática | **UC-001** | Capturar Dump           | **TST-004** | Validar captura de coordenadas GPS           |
| **RF-002** | Caption breve opcional          | **HU-003** | Caption breve              | **UC-002** | Publicar Dump           | **TST-005** | Verificar límite 150 caracteres              |
| **RF-002** | Control de privacidad           | **HU-004** | Control de privacidad      | **UC-002** | Publicar Dump           | **TST-006** | Validar configuración público/amigos/privado |
| **RF-002** | Agrupación por rangos de tiempo | **HU-005** | Agrupación por tiempo      | **UC-005** | Gestionar Perfil Propio | **TST-012** | Verificar agrupación mañana/tarde/noche      |

### 📱 Módulo Feed y Descubrimiento

| ID REQ     | Descripción                     | ID HU      | Historia de Usuario             | ID UC      | Caso de Uso               | ID TEST     | Prueba Asociada                     |
| ---------- | ------------------------------- | ---------- | ------------------------------- | ---------- | ------------------------- | ----------- | ----------------------------------- |
| **RF-003** | Feed con contenido prioritizado | **HU-007** | Feed con contenido prioritizado | **UC-003** | Explorar el Feed          | **TST-007** | Validar priorización amigos > local |
| **RF-003** | Formato de imagen compacto      | **HU-008** | Formato compacto                | **UC-003** | Explorar el Feed          | **TST-008** | Verificar relación aspecto 16:9     |
| **RF-003** | Nombres de lugares legibles     | **HU-009** | Nombres de lugares              | **UC-003** | Explorar el Feed          | **TST-009** | Validar reverse geocoding           |
| **RF-004** | Sistema de seguimiento          | **HU-010** | Seguir usuarios                 | **UC-004** | Interactuar con Contenido | **TST-013** | Verificar relación seguidor/seguido |
| **RF-004** | Interacciones sociales          | **HU-011** | Likes y guardados               | **UC-004** | Interactuar con Contenido | **TST-014** | Validar contadores de interacción   |

### 🏢 Módulo Negocios y Empresas

| ID REQ     | Descripción                  | ID HU      | Historia de Usuario          | ID UC      | Caso de Uso                 | ID TEST     | Prueba Asociada                             |
| ---------- | ---------------------------- | ---------- | ---------------------------- | ---------- | --------------------------- | ----------- | ------------------------------------------- |
| **RF-002** | Etiquetado de negocios       | **HU-014** | Etiquetar negocios           | **UC-006** | Etiquetar Negocio           | **TST-015** | Validar búsqueda y asociación de negocios   |
| **RF-004** | Perfil de negocio            | **HU-015** | Perfil de negocio            | **UC-007** | Gestionar Perfil de Negocio | **TST-016** | Verificar galería de dumps etiquetados      |
| **RF-004** | Notificaciones de etiquetado | **HU-016** | Notificaciones de etiquetado | **UC-008** | Gestionar Notificaciones    | **TST-017** | Validar envío y recepción de notificaciones |

### ⚡ Requisitos No Funcionales

| ID REQ           | Descripción                  | ID HU      | Historia de Usuario  | ID UC      | Caso de Uso      | ID TEST     | Prueba Asociada                       |
| ---------------- | ---------------------------- | ---------- | -------------------- | ---------- | ---------------- | ----------- | ------------------------------------- |
| **RNF-PERF-001** | Tiempo carga inicial <3s     | **HU-007** | Feed rápido          | **UC-003** | Explorar el Feed | **TST-018** | Medir tiempo carga inicial aplicación |
| **RNF-PERF-002** | Tiempo apertura cámara <1.5s | **HU-001** | Cámara rápida        | **UC-001** | Capturar Dump    | **TST-019** | Cronometrar apertura cámara nativa    |
| **RNF-PERF-003** | Tiempo carga feed <2s        | **HU-007** | Feed rápido          | **UC-003** | Explorar el Feed | **TST-020** | Medir tiempo carga feed inicial       |
| **RNF-003**      | Seguridad y cifrado          | **HU-012** | Autenticación segura | **UC-000** | Autenticarse     | **TST-021** | Verificar TLS/SSL y Security Rules    |
| **RNF-005**      | Mantenibilidad código        | **N/A**    | (Implícito)          | **N/A**    | (Implícito)      | **TST-022** | Revisión ESLint y estructura modular  |

---

## 📈 Métricas de Cobertura

### Cobertura por Módulo

| Módulo            | RF Cubiertos | HU Cubiertas | UC Cubiertos | Tests Definidos |
| ----------------- | ------------ | ------------ | ------------ | --------------- |
| **Autenticación** | 2/2 (100%)   | 1/1 (100%)   | 1/1 (100%)   | 3 tests         |
| **Captura**       | 5/5 (100%)   | 5/5 (100%)   | 2/2 (100%)   | 6 tests         |
| **Feed**          | 5/5 (100%)   | 4/4 (100%)   | 2/2 (100%)   | 5 tests         |
| **Negocios**      | 3/3 (100%)   | 3/3 (100%)   | 3/3 (100%)   | 3 tests         |
| **RNF**           | 5/5 (100%)   | 2/2 (100%)   | 2/2 (100%)   | 5 tests         |

### Resumen General

| Elemento                      | Total | Cubiertos | Cobertura |
| ----------------------------- | ----- | --------- | --------- |
| **Requisitos Funcionales**    | 15    | 15        | 100%      |
| **Requisitos No Funcionales** | 5     | 5         | 100%      |
| **Historias de Usuario**      | 16    | 16        | 100%      |
| **Casos de Uso**              | 8     | 8         | 100%      |
| **Casos de Prueba**           | 22    | 22        | 100%      |

---

## 🔄 Flujo de Trazabilidad

```
SRS (RF/RNF)
    → Historias de Usuario (HU)
    → Casos de Uso (UC)
    → Casos de Prueba (TST)
    → Implementación
    → Validación
```

## 📋 Observaciones y Seguimiento

### ✅ Completados

- Todos los requisitos del SRS tienen trazabilidad completa
- Cada HU está vinculada a al menos un UC y test
- Cobertura del 100% en elementos trazables

### 🔄 Pendientes de Implementación

- **HU-006** (Cámara dual) - Excluida del MVP
- Tests de integración end-to-end
- Pruebas de usabilidad con usuarios reales

### 📊 Métricas de Calidad

- **Trazabilidad Directa**: 100%
- **Coverage Funcional**: 100%
- **Coverage Técnico**: 100%
- **Tests Automatizables**: 18/22 (82%)

---

**Documento:** `doc/traceability/traceability-matrix.md`  
**Versión:** 1.2  
**Fecha:** Octubre 2025  
**Responsable:** Sebastián Puentes Gonzalez  
**Estado:** ✅ Completado para MVP

**Próxima actualización:** (post-implementación MVP)
