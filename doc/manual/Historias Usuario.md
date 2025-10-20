# AIR - Historias de Usuario (User Stories)

**Proyecto:** AIR (A Image Real) - Red Social de Fotos Espontáneas  
**Versión:** 1.1.2 (Especificación Completa)  
**Fecha:** Noviembre 2023  
**Responsable:** Sebastián Puentes Gonzalez  
**Stack Tecnológico:** Ionic React + Firebase + Capacitor  
**Estado:** En Desarrollo

---

## 📊 Resumen de Historias por Sprint

### Sprint 1: MVP Core (2-3 semanas)
- HU-001, HU-002, HU-003, HU-004, HU-008, HU-012

### Sprint 2: Feed y Perfiles (2-3 semanas)  
- HU-007, HU-009, HU-010, HU-011, HU-013

### Sprint 3: Funcionalidades Avanzadas (2-3 semanas)
- HU-005, HU-006, HU-014, HU-015, HU-016

---

## 🎯 1. Módulo Core: Captura y Publicación (Prioridad Alta)

### HU-001: Acceso Rápido a Cámara
**Como** Usuario estándar  
**Quiero** acceder directamente a la cámara con un botón flotante  
**Para** capturar momentos espontáneos sin demoras

**Criterios de Aceptación:**
- ✅ Botón flotante visible en el feed principal
- ✅ La cámara se abre en menos de 1000ms
- ✅ Interfaz minimalista sin opciones de edición
- ✅ Permisos de cámara manejados automáticamente

**Componentes Ionic:** `IonFab`, `IonFabButton`, `@capacitor/camera`  
**Esfuerzo:** M (Medio)  
**Sprint:** 1

```gherkin
Característica: Acceso Rápido a Cámara
Escenario: Abrir cámara desde feed
  Dado que estoy en el Feed principal
  Cuando presiono el IonFabButton de cámara
  Entonces la cámara nativa debe abrirse usando Capacitor Camera
  Y debo poder tomar una foto inmediatamente

Escenario: Manejo de permisos de cámara
  Dado que es la primera vez que uso la cámara
  Cuando abro la cámara
  Entonces el sistema debe solicitar permisos automáticamente
  Y guiarme a configurar permisos si son denegados
```

---

### HU-002: Geolocalización Automática
**Como** Usuario estándar  
**Quiero** que mis publicaciones incluyan automáticamente la ubicación GPS  
**Para** contextualizar el momento capturado

**Criterios de Aceptación:**
- ✅ Coordenadas GPS capturadas automáticamente al tomar foto
- ✅ Ubicación guardada en Firestore como GeoPoint
- ✅ Fallback cuando GPS no está disponible
- ✅ Permisos de ubicación manejados correctamente

**Componentes Ionic:** `@capacitor/geolocation`, Servicios Firebase  
**Esfuerzo:** M (Medio)  
**Sprint:** 1

```gherkin
Característica: Geolocalización Automática
Escenario: Publicación con ubicación exitosa
  Dado que he tomado una foto con permisos de ubicación activos
  Cuando procedo a publicar
  Entonces las coordenadas GPS deben capturarse automáticamente
  Y el dump debe guardarse con campo 'location' en Firestore

Escenario: Publicación sin ubicación disponible
  Dado que la ubicación GPS no está disponible
  Cuando publico un dump
  Entonces el sistema debe permitir publicar sin ubicación
  Y mostrar indicador de "ubicación no disponible"
```

---

### HU-003: Caption Breve Opcional
**Como** Usuario estándar  
**Quiero** poder agregar un título/comentario breve (máx. 150 caracteres)  
**Para** describir mi momento antes de publicar

**Criterios de Aceptación:**
- ✅ Campo de texto en pantalla de revisión
- ✅ Límite de 150 caracteres con contador visible
- ✅ Publicación permitida sin caption
- ✅ Validación en tiempo real

**Componentes Ionic:** `IonTextarea`, `IonLabel`, `IonNote`  
**Esfuerzo:** S (Small)  
**Sprint:** 1

```gherkin
Característica: Caption Breve Opcional
Escenario: Añadir caption válido
  Dado que estoy en la pantalla de revisión del dump
  Cuando ingreso texto de menos de 150 caracteres
  Entonces el botón de publicar debe estar habilitado
  Y el texto debe guardarse con el dump

Escenario: Caption excede límite
  Dado que ingreso más de 150 caracteres
  Cuando intento escribir más
  Entonces el contador debe mostrarse en rojo
  Y el exceso de texto debe ser truncado automáticamente
```

---

### HU-004: Control de Privacidad
**Como** Usuario estándar  
**Quiero** elegir la visibilidad de mi dump (público/amigos/solo yo)  
**Para** controlar quién puede ver mi contenido

**Criterios de Aceptación:**
- ✅ Selector de privacidad en pantalla de revisión
- ✅ Tres opciones: Público, Amigos, Solo yo
- ✅ Configuración guardada en Firestore
- ✅ Filtrado correcto en feeds según privacidad

**Componentes Ionic:** `IonSegment`, `IonSegmentButton`, `IonLabel`  
**Esfuerzo:** S (Small)  
**Sprint:** 1

```gherkin
Característica: Control de Privacidad
Escenario: Publicación privada
  Dado que selecciono "Solo yo" en privacidad
  Cuando publico el dump
  Entonces el campo 'visibility' debe ser 'private'
  Y el dump solo debe verse en mi perfil

Escenario: Publicación para amigos
  Dado que selecciono "Amigos" en privacidad
  Cuando publico el dump
  Entonces solo usuarios que me siguen deben ver el dump
  Y debe excluirse del feed público
```

---

### HU-005: Agrupación por Rangos de Tiempo
**Como** Usuario estándar  
**Quiero** que mis dumps se agrupen automáticamente por rangos horarios  
**Para** organizar visualmente mis actividades diarias

**Criterios de Aceptación:**
- ✅ Rangos: Mañana (6:00-12:00), Tarde (12:00-18:00), Noche (18:00-6:00)
- ✅ Agrupación automática basada en timestamp
- ✅ Visualización en perfil con headers de rango
- ✅ Cálculo correcto de rangos según timezone

**Componentes Ionic:** `IonListHeader`, `IonGrid`, `IonRow`  
**Esfuerzo:** L (Large)  
**Sprint:** 3

```gherkin
Característica: Agrupación por Rangos de Tiempo
Escenario: Dump en rango mañana
  Dado que publico un dump a las 9:30 AM
  Cuando veo mi perfil
  Entonces el dump debe agruparse bajo "Mañana"
  Y mostrar el rango 6:00 AM - 12:00 PM

Escenario: Dump en rango noche
  Dado que publico un dump a las 8:00 PM
  Cuando veo mi perfil
  Entonces el dump debe agruparse bajo "Noche"
  Y mostrar el rango 6:00 PM - 6:00 AM
```

---

### HU-006: Cámara Dual (Deseable)
**Como** Usuario estándar  
**Quiero** capturar con cámara frontal y trasera simultáneamente  
**Para** mostrar mi reacción y el entorno en una sola toma

**Criterios de Aceptación:**
- ✅ Detección automática de capacidades del dispositivo
- ✅ Vista dividida o Picture-in-Picture
- ✅ Ambas fotos capturadas simultáneamente
- ✅ Ambas imágenes guardadas y asociadas al dump

**Componentes Ionic:** `@capacitor/camera` avanzado, Layout personalizado  
**Esfuerzo:** L (Large)  
**Sprint:** 3

```gherkin
Característica: Cámara Dual
Escenario: Dispositivo compatible con cámara dual
  Dado que mi dispositivo tiene múltiples cámaras
  Cuando activo el modo cámara dual
  Entonces debo ver vistas previas de ambas cámaras
  Y poder capturar ambas fotos con un solo toque

Escenario: Dispositivo no compatible
  Dado que mi dispositivo tiene solo una cámara
  Cuando intento activar cámara dual
  Entonces debe mostrarse un mensaje de no compatibilidad
  Y redirigirme a cámara simple
```

---

## 📱 2. Módulo Feed y Descubrimiento (Prioridad Media)

### HU-007: Feed con Contenido Prioritizado
**Como** Usuario estándar  
**Quiero** ver un feed de scroll infinito que priorice amigos y luego sugerencias locales  
**Para** descubrir contenido relevante de mi círculo y zona

**Criterios de Aceptación:**
- ✅ Primeros 10 dumps de usuarios que sigo
- ✅ Luego dumps populares de mi ubicación
- ✅ Scroll infinito con carga progresiva
- ✅ Pull-to-refresh para actualizar contenido

**Componentes Ionic:** `IonInfiniteScroll`, `IonRefresher`, `IonContent`  
**Esfuerzo:** L (Large)  
**Sprint:** 2

```gherkin
Característica: Feed con Contenido Prioritizado
Escenario: Carga inicial del feed
  Dado que tengo 5 usuarios seguidos
  Cuando abro el feed por primera vez
  Entonces deben mostrarse primero dumps de mis seguidores
  Luego dumps populares de mi ciudad
  Y el tiempo de carga debe ser < 2000ms

Escenario: Scroll infinito
  Dado que he visto los primeros 10 dumps
  Cuando scrolleo hasta el final
  Entonces deben cargarse automáticamente 10 dumps más
  Y mostrar IonSpinner durante la carga
```

---

### HU-008: Formato de Imagen Compacto
**Como** Usuario estándar  
**Quiero** que los dumps en el feed usen formato de imagen compacto (16:9)  
**Para** poder consumir más contenido en pantalla

**Criterios de Aceptación:**
- ✅ Relación de aspecto 16:9 para todas las imágenes
- ✅ Al menos 3-4 dumps visibles en pantalla simultáneamente
- ✅ Scroll vertical suave
- ✅ Images optimizadas para carga rápida

**Componentes Ionic:** `IonCard`, `IonImg`, CSS personalizado  
**Esfuerzo:** S (Small)  
**Sprint:** 1

```gherkin
Característica: Formato de Imagen Compacto
Escenario: Visualización de dump en feed
  Dado que estoy en el feed
  Cuando veo un dump
  Entonces la imagen debe tener relación 16:9
  Y el card no debe exceder el 40% de altura de pantalla
  Y debo ver al menos 3 dumps sin hacer scroll
```

---

### HU-009: Nombres de Lugares Legibles
**Como** Usuario estándar  
**Quiero** ver nombres de lugares legibles en lugar de coordenadas  
**Para** entender fácilmente dónde fue capturado cada momento

**Criterios de Aceptación:**
- ✅ Reverse geocoding de coordenadas a nombres
- ✅ Cache local de nombres de lugares
- ✅ Fallback a dirección aproximada si no hay nombre
- ✅ Actualización en tiempo real si cambia el nombre del lugar

**Componentes Ionic:** Servicios, Google Maps Geocoding API  
**Esfuerzo:** M (Medio)  
**Sprint:** 2

```gherkin
Característica: Nombres de Lugares Legibles
Escenario: Lugar con nombre conocido
  Dado que un dump tiene coordenadas de una cafetería conocida
  Cuando se muestra en el feed
  Entonces debe mostrarse "Cafetería Central" en lugar de coordenadas
  Y debe ser clickeable para ver en mapa

Escenario: Lugar sin nombre específico
  Dado que un dump tiene coordenadas en un parque público
  Cuando se muestra en el feed
  Entonces debe mostrarse "Parque Central" o dirección aproximada
  Y no mostrar coordenadas técnicas
```

---

### HU-010: Sistema de Seguimiento
**Como** Usuario estándar  
**Quiero** poder seguir a otros usuarios  
**Para** priorizar su contenido en mi feed

**Criterios de Aceptación:**
- ✅ Botón "Seguir" en perfiles de usuario
- ✅ Estado persistente (Siguiendo/No siguiendo)
- ✅ Actualización en tiempo real del contador
- ✅ Notificación opcional al usuario seguido

**Componentes Ionic:** `IonButton`, `IonBadge`, Servicios Firebase  
**Esfuerzo:** S (Small)  
**Sprint:** 2

```gherkin
Característica: Sistema de Seguimiento
Escenario: Seguir usuario
  Dado que estoy en el perfil de otro usuario
  Cuando presiono "Seguir"
  Entonces mi ID debe agregarse a sus seguidores
  Y el botón debe cambiar a "Siguiendo"
  Y su contador de seguidores debe incrementarse

Escenario: Dejar de seguir
  Dado que estoy siguiendo a un usuario
  Cuando presiono "Siguiendo"
  Entonces mi ID debe removerse de sus seguidores
  Y el botón debe cambiar a "Seguir"
```

---

### HU-011: Interacciones Sociales
**Como** Usuario estándar  
**Quiero** poder dar "me gusta" y guardar dumps  
**Para** interactuar con contenido que me gusta y acceder luego

**Criterios de Aceptación:**
- ✅ Botón de like con estado visual
- ✅ Contador de likes en tiempo real
- ✅ Funcionalidad de guardar para acceso offline
- ✅ Sección de "guardados" en perfil

**Componentes Ionic:** `IonIcon`, `IonButton`, `IonBadge`  
**Esfuerzo:** S (Small)  
**Sprint:** 2

```gherkin
Característica: Interacciones Sociales
Escenario: Dar like a dump
  Dado que veo un dump en el feed
  Cuando presiono el icono de corazón
  Entonces el contador de likes debe incrementarse
  Y el corazón debe mostrarse en rojo
  Y mi like debe guardarse en Firestore

Escenario: Guardar dump
  Dado que veo un dump que me interesa
  Cuando presiono el icono de guardar
  Entonces el dump debe agregarse a mi lista de guardados
  Y debe estar disponible offline
```

---

## 🔐 3. Módulo Autenticación y Perfil (Prioridad Alta)

### HU-012: Registro y Autenticación
**Como** Usuario nuevo/existente  
**Quiero** registrarme con email/contraseña o Google Sign-In  
**Para** comenzar a usar la aplicación y tener mi perfil

**Criterios de Aceptación:**
- ✅ Formulario de registro con validación
- ✅ Login con Google Sign-In
- ✅ Manejo seguro de credenciales
- ✅ Redirección automática post-login

**Componentes Ionic:** `IonInput`, `IonButton`, `IonAlert`, Firebase Auth  
**Esfuerzo:** M (Medio)  
**Sprint:** 1

```gherkin
Característica: Registro y Autenticación
Escenario: Registro exitoso con email
  Dado que ingreso email y contraseña válidos
  Cuando presiono "Registrarme"
  Entonces debe crearse mi cuenta en Firebase Auth
  Y debe crearse mi perfil en Firestore
  Y debo ser redirigido al feed

Escenario: Login con Google
  Dado que selecciono "Continuar con Google"
  Cuando completo el flujo de OAuth
  Entonces debo autenticarme correctamente
  Y mi perfil debe crearse/recuperarse automáticamente
```

---

### HU-013: Perfil de Usuario
**Como** Usuario estándar  
**Quiero** ver mi perfil con historial de dumps y estadísticas  
**Para** revisar mi actividad y progreso

**Criterios de Aceptación:**
- ✅ Grid de dumps organizados por fecha
- ✅ Estadísticas: total dumps, seguidores, seguidos
- ✅ Navegación entre "Mis Dumps" y "Guardados"
- ✅ Edición básica de perfil (nombre, foto)

**Componentes Ionic:** `IonTabs`, `IonGrid`, `IonChip`, `IonAvatar`  
**Esfuerzo:** M (Medio)  
**Sprint:** 2

```gherkin
Característica: Perfil de Usuario
Escenario: Ver perfil propio
  Dado que navego a mi perfil
  Cuando se carga la página
  Entonces debo ver mi foto y nombre
  Y un grid con todos mis dumps
  Y las estadísticas actualizadas

Escenario: Ver perfil de otro usuario
  Dado que navego al perfil de otro usuario
  Cuando se carga la página
  Entonces debo ver botón "Seguir"
  Y solo sus dumps públicos
  Y no opciones de edición
```

---

## 🏢 4. Módulo Negocios y Economía Orgánica (Prioridad Media/Baja)

### HU-014: Etiquetado de Negocios
**Como** Usuario estándar  
**Quiero** poder etiquetar negocios en mis dumps  
**Para** recomendar lugares de forma orgánica

**Criterios de Aceptación:**
- ✅ Búsqueda de negocios por nombre/categoría
- ✅ Selección desde lista o mapa
- ✅ Tag guardado en metadata del dump
- ✅ Negocio recibe notificación de etiqueta

**Componentes Ionic:** `IonSearchbar`, `IonModal`, `IonList`  
**Esfuerzo:** M (Medio)  
**Sprint:** 3

```gherkin
Característica: Etiquetado de Negocios
Escenario: Etiquetar negocio existente
  Dado que estoy publicando un dump
  Cuando busco "Cafetería Central" y lo selecciono
  Entonces el negocio debe asociarse al dump
  Y mostrarse como tag en la publicación
  Y el negocio debe recibir notificación

Escenario: Negocio no encontrado
  Dado que busco un negocio que no existe
  Cuando no aparece en resultados
  Entonces debo tener opción para sugerir nuevo negocio
  O continuar sin etiquetar
```

---

### HU-015: Perfil de Negocio
**Como** Usuario empresarial  
**Quiero** tener un perfil especial con información de contacto y dumps donde fui etiquetado  
**Para** mostrar mi presencia y engagement

**Criterios de Aceptación:**
- ✅ Perfil diferenciado con logo e información
- ✅ Galería de dumps donde el negocio fue etiquetado
- ✅ Información de contacto y ubicación
- ✅ Estadísticas de engagement

**Componentes Ionic:** `IonCard`, `IonIcon`, Layout empresarial  
**Esfuerzo:** L (Large)  
**Sprint:** 3

```gherkin
Característica: Perfil de Negocio
Escenario: Ver perfil de negocio
  Dado que navego a un perfil de negocio
  Cuando se carga la página
  Entonces debo ver información de contacto
  Y una galería de dumps donde fue etiquetado
  Y botón para seguir/direcciones

Escenario: Negocio sin etiquetas
  Dado que un negocio no ha sido etiquetado
  Cuando veo su perfil
  Entonces debe mostrarse estado "Aún no hay recomendaciones"
  Y llamado a acción para ser el primero
```

---

### HU-016: Notificaciones de Etiquetado
**Como** Usuario empresarial  
**Quiero** recibir notificaciones cuando me etiquetan en dumps  
**Para** conocer las recomendaciones y engagement

**Criterios de Aceptación:**
- ✅ Notificación push cuando son etiquetados
- ✅ Lista de notificaciones en la app
- ✅ Navegación directa al dump etiquetador
- ✅ Configuración de preferencias de notificación

**Componentes Ionic:** `IonBadge`, Firebase Cloud Messaging  
**Esfuerzo:** S (Small)  
**Sprint:** 3

```gherkin
Característica: Notificaciones de Etiquetado
Escenario: Recibir notificación de etiqueta
  Dado que un usuario etiqueta mi negocio
  Cuando se publica el dump
  Entonces debo recibir notificación push
  Y el badge de notificaciones debe incrementarse
  Y al abrirla debo ir directamente al dump

Escenario: Ver historial de notificaciones
  Dado que tengo notificaciones pendientes
  Cuando navego a la sección de notificaciones
  Entonces debo ver lista cronológica
  Y poder marcar como leídas
```

---

## 📋 Definiciones de Esfuerzo

| Esfuerzo | Tiempo Estimado | Complejidad | Ejemplos |
|----------|-----------------|-------------|----------|
| **S (Small)** | 1-2 días | Baja | HU-003, HU-008 |
| **M (Medium)** | 3-5 días | Media | HU-001, HU-002 |
| **L (Large)** | 6-10 días | Alta | HU-005, HU-007 |

---

**Documento:** `doc/backlog/user-stories.md`  
**Última actualización:** octubre 2025  
**Próxima revisión:** ---