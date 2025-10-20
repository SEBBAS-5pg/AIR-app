# ESPECIFICACIÓN COMPLETA DE CASOS DE USO (UC)

**Proyecto:** AIR (A Image Real) - Red Social de Fotos Espontáneas  
**Versión:** 1.1.2 (Especificación Completa)  
**Fecha:** Octubre 2025  
**Responsable:** Sebastián Puentes Gonzalez  
**Stack:** Ionic React + Capacitor + Firebase

---

## UC-000: Autenticarse

**UC ID:** UC-000  
**Nombre:** Autenticarse (Registro e Inicio de Sesión)  
**Objetivo:** Permitir al actor acceder al sistema de forma segura mediante credenciales (HU-012, RNF-003).  
**Actor Principal:** Usuario Estándar, Usuario Empresarial  
**Precondición:** El actor no está autenticado.  

**Flujo Principal:**
1. El actor ingresa a la aplicación y es redirigido a la AuthPage
2. El actor selecciona "Registrarse" o "Iniciar Sesión"
3. El actor ingresa email y contraseña válidos
4. El sistema valida las credenciales contra Firebase Auth
5. Si es registro, crea el perfil de usuario en Firestore
6. El sistema redirige al actor al Feed principal (UC-003)

**Flujo Alternativo (A1 - Registro con Google):**
- El actor selecciona "Continuar con Google"
- Completa el flujo OAuth2 con Google Sign-In
- El sistema crea automáticamente el perfil asociado
- Redirección al Feed principal

**Flujo Alternativo (A2 - Recuperación de Contraseña):**
- El actor selecciona "¿Olvidaste tu contraseña?"
- Ingresa su email registrado
- El sistema envía email de recuperación via Firebase Auth
- El actor sigue el enlace para restablecer contraseña

**Flujo de Excepción (E1 - Credenciales Inválidas):**
- El sistema muestra mensaje "Credenciales incorrectas" usando IonAlert
- Permite reintentar o recuperar contraseña

**Flujo de Excepción (E2 - Email Ya Registrado):**
- Durante registro, si el email existe, muestra "Este email ya está registrado"
- Sugiere iniciar sesión o recuperar contraseña

**Postcondición:**  
El actor está autenticado en el sistema con sesión persistente y tiene acceso a las funcionalidades principales.

---

## UC-001: Capturar Dump (Instantáneo)

**UC ID:** UC-001  
**Nombre:** Capturar Dump (Instantáneo)  
**Objetivo:** Abrir la cámara nativa del dispositivo de forma inmediata para tomar una foto sin filtros (HU-001, RNF-002).  
**Actor Principal:** Usuario Estándar  
**Precondición:** El actor está autenticado y en el Feed principal.

**Flujo Principal:**
1. El actor pulsa el IonFabButton de cámara en el Feed
2. El sistema navega a CameraPage y solicita permisos de cámara
3. El sistema accede a la cámara nativa via @capacitor/camera en menos de 1.5 segundos
4. El actor compone la foto y pulsa el botón de captura
5. El sistema toma la foto con calidad media (80%)
6. El sistema obtiene la ubicación actual via @capacitor/geolocation
7. El sistema navega a PostReviewPage con la foto y metadatos

**Flujo Alternativo (A1 - Cámara desde Perfil):**
- El actor accede a la cámara desde la pestaña de perfil
- Mismo flujo principal pero redirección post-captura al perfil

**Flujo de Excepción (E1 - Permisos Denegados):**
- El sistema muestra IonAlert explicando la necesidad de permisos
- Ofrece opción para ir a configuración del dispositivo
- Redirige al Feed si el usuario cancela

**Flujo de Excepción (E2 - GPS No Disponible):**
- El sistema captura la foto sin ubicación
- Muestra indicador "Ubicación no disponible" en revisión
- Permite al usuario ingresar ubicación manualmente

**Postcondición:**  
Una imagen capturada con metadatos básicos lista para revisión y publicación.

---

## UC-002: Publicar Dump

**UC ID:** UC-002  
**Nombre:** Publicar Dump (Incluyendo GeoPoint y Metadatos)  
**Objetivo:** Almacenar la foto y sus metadatos asociados en el backend (HU-002, HU-003, HU-004, HU-005).  
**Actor Principal:** Usuario Estándar  
**Precondición:** El actor ha capturado una foto (UC-001) y está en PostReviewPage.

**Flujo Principal:**
1. El sistema muestra la foto capturada con metadatos pre-cargados
2. El actor añade caption (opcional, máximo 150 caracteres) - HU-003
3. El actor selecciona privacidad usando IonSegment (Público/Amigos/Solo yo) - HU-004, HU-005
4. El actor opcionalmente etiqueta negocio usando UC-006
5. El actor pulsa "Publicar"
6. El sistema sube la imagen a Firebase Storage
7. El sistema crea documento en Firestore con todos los metadatos
8. El sistema muestra IonToast de confirmación
9. El sistema redirige al Feed principal

**Flujo Alternativo (A1 - Publicación Rápida):**
- El actor omite todos los pasos opcionales y publica directamente
- El sistema usa configuración por defecto (público, sin caption)

**Flujo Alternativo (A2 - Guardar como Borrador):**
- El actor selecciona "Guardar borrador"
- El sistema guarda localmente usando Ionic Storage
- Puede recuperarse desde la sección de borradores del perfil

**Flujo de Excepción (E1 - Error de Subida):**
- El sistema detecta fallo en upload a Storage
- Muestra opción para reintentar o guardar localmente
- Programa reintento automático cuando haya conexión

**Flujo de Excepción (E2 - Caption Muy Largo):**
- El sistema valida longitud en tiempo real
- Muestra contador en rojo y deshabilita botón de publicar
- Previene envío hasta que esté dentro del límite

**Postcondición:**  
La publicación existe en Firestore y Storage, accesible según configuración de privacidad.

---

## UC-003: Explorar el Feed

**UC ID:** UC-003  
**Nombre:** Explorar el Feed (Descubrimiento y Consumo)  
**Objetivo:** Mostrar contenido relevante y local de forma priorizada (HU-007, HU-008, HU-009, RNF-001).  
**Actor Principal:** Usuario Estándar, Usuario Empresarial  
**Precondición:** El actor está autenticado.

**Flujo Principal:**
1. El actor accede al FeedPage
2. El sistema carga contenido inicial (amigos > local) en menos de 2 segundos
3. El sistema muestra DumpCards con formato 16:9 optimizado - HU-008
4. Cada card muestra nombre de lugar legible en lugar de coordenadas - HU-009
5. El actor hace scroll vertical
6. Al acercarse al final, IonInfiniteScroll carga más contenido
7. El actor puede interactuar con contenido (UC-004) o ver perfiles

**Flujo Alternativo (A1 - Pull to Refresh):**
- El actor hace pull-down en la lista
- IonRefresher ejecuta nueva consulta a Firestore
- Muestra contenido más reciente

**Flujo Alternativo (A2 - Filtro por Ubicación):**
- El actor usa filtro de ubicación para ver contenido de zona específica
- El sistema prioriza dumps en radio de 10km

**Flujo de Excepción (E1 - Sin Conexión):**
- El sistema muestra dumps cacheados localmente
- Muestra banner "Modo offline" con IonBadge
- Botón para reintentar conexión

**Flujo de Excepción (E2 - Feed Vacío):**
- Para nuevos usuarios sin seguidores, muestra contenido popular local
- Incluye sugerencias para seguir usuarios

**Postcondición:**  
El usuario ha consumido contenido y el sistema registra métricas de engagement.

---

## UC-004: Interactuar con Contenido

**UC ID:** UC-004  
**Nombre:** Interactuar con Contenido (Like, Guardar, Seguir)  
**Objetivo:** Permitir al actor expresar interés en contenido y usuarios (HU-010, HU-011).  
**Actor Principal:** Usuario Estándar  
**Precondición:** El actor está viendo contenido en Feed o perfil.

**Flujo Principal (Like):**
1. El actor pulsa el icono de corazón en DumpCard
2. El sistema incrementa contador en Firestore
3. El icono cambia a estado activo (rojo)
4. Se registra la interacción en subcolección

**Flujo Principal (Guardar):**
1. El actor pulsa el icono de bookmark
2. El sistema añade dump a lista de guardados del usuario
3. El icono cambia a estado activo
4. El dump queda disponible en sección "Guardados" del perfil

**Flujo Principal (Seguir Usuario):**
1. El actor pulsa "Seguir" en perfil de usuario
2. El sistema añade relación en Firestore
3. El botón cambia a "Siguiendo"
4. El contador de seguidores se actualiza

**Flujo Alternativo (A1 - Unlike/Unsave/Dejar de Seguir):**
- Al repetir la acción, se revierte el estado
- Se remueve la relación correspondiente

**Flujo de Excepción (E1 - Error de Interacción):**
- El sistema detecta fallo en la operación
- Muestra mensaje temporal "Intenta nuevamente"
- Mantiene estado visual anterior

**Postcondición:**  
Las relaciones de interacción están actualizadas en Firestore y reflejadas en la UI.

---

## UC-005: Gestionar Perfil Propio

**UC ID:** UC-005  
**Nombre:** Gestionar Perfil Propio  
**Objetivo:** Mostrar historial de dumps y estadísticas del usuario (HU-013).  
**Actor Principal:** Usuario Estándar  
**Precondición:** El actor está autenticado.

**Flujo Principal:**
1. El actor navega a ProfilePage
2. El sistema carga perfil con IonTabs (Dumps, Guardados, Estadísticas)
3. En pestaña "Dumps", muestra grid con historial agrupado por fecha
4. En pestaña "Guardados", muestra dumps marcados como favoritos
5. En pestaña "Estadísticas", muestra métricas (seguidores, seguidos, total dumps)
6. El actor puede editar información básica (nombre, foto)

**Flujo Alternativo (A1 - Edición de Perfil):**
- El actor pulsa "Editar perfil"
- Puede cambiar nombre de usuario y foto de perfil
- Los cambios se guardan en Firestore

**Flujo Alternativo (A2 - Ver Dump en Detalle):**
- El actor pulsa cualquier dump en el grid
- Se abre modal con vista ampliada y opciones adicionales

**Flujo de Excepción (E1 - Perfil No Cargado):**
- El sistema muestra skeleton screens durante carga
- Si falla, muestra opción para reintentar

**Postcondición:**  
El usuario puede revisar y gestionar su presencia en la plataforma.

---

## UC-006: Etiquetar Negocio

**UC ID:** UC-006  
**Nombre:** Etiquetar Negocio  
**Objetivo:** Vincular publicación a perfil empresarial para recomendación orgánica (HU-014).  
**Actor Principal:** Usuario Estándar  
**Precondición:** El actor está en PostReviewPage (UC-002).

**Flujo Principal:**
1. El actor pulsa "Etiquetar negocio" en PostReviewPage
2. El sistema abre modal con IonSearchbar
3. El actor escribe nombre o categoría de negocio
4. El sistema muestra lista de negocios que coinciden (máximo 10 resultados)
5. El actor selecciona negocio de la lista
6. El ID del negocio se añade a taggedBusiness del dump
7. El sistema muestra chip con nombre del negocio

**Flujo Alternativo (A1 - Búsqueda por Ubicación):**
- El sistema sugiere negocios cercanos a la ubicación del dump
- Ordena resultados por proximidad

**Flujo Alternativo (A2 - Negocio No Encontrado):**
- Si no hay resultados, muestra "¿No encuentras el negocio?"
- Ofrece opción para sugerir nuevo negocio (redirige a formulario)

**Flujo de Excepción (E1 - Negocio Inactivo):**
- Si el negocio está marcado como inactivo, muestra advertencia
- Permite etiquetar igualmente o elegir otro

**Postcondición:**  
El dump incluye referencia al negocio etiquetado para descubrimiento orgánico.

---

## UC-007: Gestionar Perfil de Negocio

**UC ID:** UC-007  
**Nombre:** Gestionar Perfil de Negocio  
**Objetivo:** Permitir visualización y gestión de perfil empresarial (HU-015).  
**Actor Principal:** Usuario Empresarial  
**Precondición:** El negocio tiene perfil creado y usuario autenticado es owner.

**Flujo Principal (Ver Perfil):**
1. Cualquier usuario accede a perfil de negocio
2. El sistema muestra información empresarial (nombre, categoría, contacto)
3. Muestra galería de dumps donde el negocio fue etiquetado
4. Incluye estadísticas de engagement (total etiquetas, reach)

**Flujo Principal (Gestionar Perfil - Owner):**
1. Owner accede a "Gestionar negocio"
2. Puede editar información (descripción, horarios, contacto)
3. Puede subir imágenes de catálogo/menú
4. Puede ver analytics avanzados (opcional)

**Flujo Alternativo (A1 - Seguir Negocio):**
- Usuarios pueden seguir negocio para recibir actualizaciones
- Aparece en sección "Negocios que sigo"

**Flujo de Excepción (E1 - Perfil No Verificado):**
- Si el negocio no está verificado, muestra badge "En revisión"
- Algunas funcionalidades pueden estar limitadas

**Postcondición:**  
Presencia digital del negocio actualizada y accesible para la comunidad.

---

## UC-008: Gestionar Notificaciones

**UC ID:** UC-008  
**Nombre:** Gestionar Notificaciones  
**Objetivo:** Alertar sobre actividad relevante (etiquetas, interacciones) - HU-016.  
**Actor Principal:** Usuario Estándar, Usuario Empresarial  
**Precondición:** El actor está autenticado.

**Flujo Principal (Recibir Notificación):**
1. El sistema detecta evento relevante (nuevo seguidor, like, etiqueta)
2. Crea documento en colección notifications del usuario
3. Si la app está en foreground, muestra IonToast
4. Si está en background, envía push notification via FCM
5. Incrementa badge en icono de notificaciones

**Flujo Principal (Ver Notificaciones):**
1. El actor pulsa icono de campana
2. El sistema muestra lista de notificaciones no leídas
3. Al pulsar una notificación, navega al contenido relevante
4. Marca notificación como leída

**Flujo Alternativo (A1 - Configuración de Notificaciones):**
- El actor puede configurar tipos de notificaciones que recibe
- Puede silenciar notificaciones temporalmente

**Flujo de Excepción (E1 - Notificaciones Desactivadas):**
- El sistema detecta que el usuario desactivó notificaciones
- Muestra prompt para reactivar cuando hay actividad relevante

**Postcondición:**  
El usuario está informado sobre actividad relevante en su red.

---

## 📊 Resumen de Cobertura de HU

| HU ID | Cubierta por UC(s) | Estado |
|-------|-------------------|---------|
| HU-001 | UC-001 | ✅ Completo |
| HU-002 | UC-001, UC-002 | ✅ Completo |
| HU-003 | UC-002 | ✅ Completo |
| HU-004 | UC-002 | ✅ Completo |
| HU-005 | UC-002 | ✅ Completo |
| HU-007 | UC-003 | ✅ Completo |
| HU-008 | UC-003 | ✅ Completo |
| HU-009 | UC-003 | ✅ Completo |
| HU-010 | UC-004 | ✅ Completo |
| HU-011 | UC-004 | ✅ Completo |
| HU-012 | UC-000 | ✅ Completo |
| HU-013 | UC-005 | ✅ Completo |
| HU-014 | UC-006 | ✅ Completo |
| HU-015 | UC-007 | ✅ Completo |
| HU-016 | UC-008 | ✅ Completo |

**Documento:** `doc/requirements/use-cases.md`  
**Última actualización:** Octubre 2025  
**Próxima revisión:** --- 