# 📘 ESPECIFICACIÓN DE REQUISITOS DE SOFTWARE (SRS) - IEEE 830

**Proyecto:** AIR (A Image Real) - Red Social de Fotos Espontáneas  
**Versión:** 1.1.2 (MVP)  
**Fecha:** agosto 2025  
**Responsable:** Sebastián Puentes Gonzalez  
**Stack:** Ionic React + Capacitor + Firebase  
**Estado:** En Desarrollo

---

## 1.1 Introducción

### 1.1.1 Propósito

Este documento especifica los requisitos funcionales y no funcionales para la aplicación móvil **AIR (A Image Real)**, una plataforma diseñada para facilitar la captura y compartición espontánea de momentos geolocalizados, reduciendo la barrera de la perfección en redes sociales tradicionales.

### 1.1.2 Alcance

**AIR** es una aplicación móvil híbrida desarrollada en **Ionic con React y Capacitor**, con backend en **Firebase/Firestore**.

**Alcance del MVP:**
- Autenticación y registro de usuarios
- Captura rápida de fotos con geolocalización automática
- Feed principal con contenido de amigos y ubicación
- Perfiles básicos de usuario
- Funcionalidad offline básica con Ionic Storage

**Exclusiones del MVP:**
- Perfiles empresariales avanzados
- Integración con APIs de música
- Sistema de mensajería privada
- Análiticas avanzadas
- Cámara dual simultánea

### 1.1.3 Definiciones, Acrónimos y Abreviaturas

| Término | Definición |
|---------|------------|
| **AIR** | A Image Real - Nombre de la aplicación |
| **Dump** | Publicación individual de un momento espontáneo |
| **Feed** | Flujo principal de contenido de la aplicación |
| **GeoPoint** | Coordenadas geográficas (latitud, longitud) |
| **MVP** | Producto Mínimo Viable |
| **RF** | Requisito Funcional |
| **RNF** | Requisito No Funcional |
| **SRS** | Especificación de Requisitos de Software |
| **PWA** | Progressive Web App |
| **CAP** | Capacitor Plugin |

### 1.1.4 Referencias

- IEEE Std 830-1998 - Estándar para Especificación de Requisitos de Software
- Documentación oficial de Ionic React
- Guías de Material Design (Android) y Human Interface Guidelines (iOS)
- Políticas de privacidad de Google Play Store y Apple App Store
- Documento: `doc/backlog/user-stories.md`
- Documento: `doc/architecture/system-architecture.md`

### 1.1.5 Visión General del Documento

Este documento sigue el estándar IEEE 830 organizado en:
- **Sección 1.1**: Introducción y contexto del proyecto
- **Sección 1.2**: Descripción general del producto y usuarios
- **Sección 1.3**: Requisitos específicos detallados
- **Apéndices**: Información complementaria y modelos

---

## 1.2 Descripción General

### 1.2.1 Perspectiva del Producto

**AIR** es un sistema cliente-servidor compuesto por:

- **Cliente Móvil**: Aplicación iOS/Android desarrollada en Ionic React + Capacitor
- **Backend como Servicio**: Firebase (Authentication, Firestore, Storage)
- **Bridge Nativo**: Capacitor Plugins (Cámara, Geolocation, Storage)
- **Servicios Externos**: APIs de geolocalización (Google Maps/Apple Maps)
- **Almacenamiento Local**: Ionic Storage + IndexedDB para caché

### 1.2.2 Funciones del Producto

1. **Gestión de Usuarios**
   - Registro y autenticación con Firebase Auth
   - Perfiles de usuario básicos
   - Sistema de seguimiento entre usuarios

2. **Captura de Momentos**
   - Acceso rápido a cámara nativa via Capacitor
   - Geolocalización automática con GPS
   - Metadatos contextuales y caption opcional

3. **Contenido y Descubrimiento**
   - Feed principal con scroll infinito
   - Priorización por amigos y ubicación
   - Contenido offline básico

4. **Gestión de Datos**
   - Sincronización con Firebase Firestore
   - Almacenamiento local eficiente
   - Gestión de permisos nativos

### 1.2.3 Características de los Usuarios

| Tipo de Usuario | Perfil | Edad | Nivel Tecnológico | Frecuencia de Uso |
|-----------------|--------|------|-------------------|-------------------|
| **Usuario Individual** | Personas que buscan compartir momentos espontáneos sin edición | 18-35 | Medio | Diario (2-5 veces/día) |
| **Usuario Empresarial** | Negocios locales que buscan visibilidad orgánica | 20-40 | Medio-Alto | Semanal (3-5 veces/semana) |

### 1.2.4 Restricciones

- **Tecnológicas**: Desarrollo con Ionic React + Capacitor, Firebase como BaaS
- **Temporales**: Entrega en ciclo académico (16 semanas)
- **Plataforma**: Publicación en App Store, Google Play Store y PWA
- **Legales**: Cumplimiento de GDPR/LGPD para datos de ubicación

### 1.2.5 Supuestos y Dependencias

- **Conectividad**: Los usuarios tendrán acceso intermitente a internet
- **Dispositivos**: Los usuarios contarán con smartphones con cámara y GPS
- **Servicios**: Firebase mantendrá disponibilidad del 99.9%
- **Permisos**: Los usuarios concederán permisos de cámara y ubicación
- **Capacitor**: Los plugins nativos funcionarán en dispositivos compatibles

---

## 1.3 Requerimientos Específicos

### 1.3.1 Interfaces Externas

- **Interfaz de Usuario**: Diseño minimalista con componentes Ionic, siguiendo principios de Material Design 3
- **Interfaz de Hardware**: Cámara nativa, GPS, almacenamiento via Capacitor Plugins
- **Interfaz de Comunicaciones**: REST APIs con Firebase, listeners en tiempo real con Firestore
- **Interfaz Nativa**: Bridge Capacitor para acceso a APIs del dispositivo

### 1.3.2 Funciones del Sistema (RF)

**RF-001 - Autenticación de Usuario**
- El sistema debe permitir registro con email y contraseña usando Firebase Auth
- El sistema debe permitir autenticación con Google Sign-In
- El usuario debe poder recuperar contraseña
- Las sesiones deben persistir entre reinicios de app

**RF-002 - Captura de Momentos**
- La aplicación debe acceder a la cámara nativa en menos de 1.5 segundos usando Capacitor Camera
- La captura de foto debe incluir metadatos de ubicación automáticamente via Capacitor Geolocation
- El usuario debe poder añadir caption opcional (max 150 caracteres) antes de publicar

**RF-003 - Gestión de Feed**
- El feed debe cargar contenido en orden cronológico inverso
- El sistema debe priorizar contenido de usuarios seguidos
- Debe implementar scroll infinito con IonInfiniteScroll
- Debe soportar pull-to-refresh con IonRefresher

**RF-004 - Gestión de Perfiles**
- Los usuarios deben poder ver su perfil con historial de dumps
- Implementar sistema de seguimiento entre usuarios
- Mostrar estadísticas básicas (seguidores, seguidos, total dumps)

*(Lista completa en `doc/backlog/user-stories.md`)*

### 1.3.3 Rendimiento (RNF-Performance)

| Código | Requisito | Valor Objetivo |
|--------|-----------|----------------|
| **RNF-PERF-001** | Tiempo de carga inicial de la aplicación | < 3 segundos |
| **RNF-PERF-002** | Tiempo de apertura de cámara | < 1.5 segundos |
| **RNF-PERF-003** | Tiempo de carga del feed | < 2 segundos |
| **RNF-PERF-004** | Uso de memoria en dispositivos básicos | < 100 MB RAM |
| **RNF-PERF-005** | Tamaño inicial de la aplicación | < 50 MB |

### 1.3.4 Lógica de Datos / Base de Datos

**Estructura Principal:**
```javascript
Users {
  userId: string (UUID)
  email: string
  username: string
  profilePicture: string (URL)
  userType: 'individual' | 'business'
  createdAt: timestamp
  updatedAt: timestamp
  followers: number
  following: number
}

Dumps {
  dumpId: string (UUID)
  userId: string
  imageUrl: string
  caption: string (max 150)
  location: GeoPoint
  timestamp: timestamp
  visibility: 'public' | 'friends' | 'private'
  taggedBusiness: string (optional)
  likes: number
}

Interactions {
  interactionId: string (UUID)
  userId: string
  dumpId: string
  type: 'like' | 'save'
  createdAt: timestamp
}

Businesses {
  businessId: string (UUID)
  name: string
  description: string
  category: string
  address: string
  geopoint: GeoPoint
  contactEmail: string
  phone: string
  website: string
  dumpCount: number
  ownerId: string
  isVerified: boolean
  createdAt: timestamp
}
```

### 1.3.5 Restricciones de Diseño

- **Compatibilidad**: iOS 13+ y Android 8.0+ (API 26+), PWA compatible
- **Accesibilidad**: Soporte para VoiceOver (iOS) y TalkBack (Android)
- **Diseño Responsive**: Soporte para pantallas desde 4.7" hasta 6.7"
- **Navegación**: Patrón de navegación por pestañas inferiores con IonTabs
- **Componentes**: Uso de componentes Ionic oficiales para consistencia UI/UX

### 1.3.6 Atributos del Sistema (RNF)

| Categoría | Requisitos |
|-----------|------------|
| **Seguridad** | Autenticación con Firebase Auth, datos en tránsito cifrados con TLS 1.2+, validación de entrada en cliente y servidor, Security Rules de Firestore |
| **Disponibilidad** | 99% uptime durante horario pico (18:00-23:00) |
| **Mantenibilidad** | Código documentado, arquitectura modular con servicios, uso de ESLint y Prettier, componentes reutilizables |
| **Usabilidad** | Tiempo de aprendizaje < 5 minutos, touch targets ≥ 44x44 dp, navegación intuitiva |
| **Portabilidad** | Funcionamiento en iOS, Android y navegadores web via PWA |

### 1.3.7 Requisitos de Internacionalización/Localización

- **Idioma Principal**: Español
- **Soporte Futuro**: Inglés, Portugués
- **Formato**: Fechas y horas según configuración regional del dispositivo
- **Moneda**: Formato local para futuras funcionalidades de negocio

### 1.3.8 Requisitos Legales y de Privacidad

- **Política de Privacidad**: Explicación clara del uso de datos de ubicación e imágenes
- **Consentimiento**: Obtención explícita para recolección de datos sensibles (ubicación, cámara)
- **Derechos del Usuario**: Capacidad de eliminar cuenta y todos los datos asociados
- **Edad Mínima**: 18 años de edad
- **Términos de Servicio**: Aceptación obligatoria durante registro
- **Cookies y Tracking**: Minimal, solo para funcionalidad esencial

---

## 1.4 Apéndices

### 1.4.1 Diagrama de Arquitectura Simplificado
*(Ver `doc/architecture/system-architecture.md`)*

### 1.4.2 Políticas de Datos
- Retención de datos: 36 meses de inactividad
- Backup automático cada 24 horas en Firebase
- Exportación de datos de usuario disponible on-demand
- Eliminación automática de imágenes no referenciadas después de 30 días

### 1.4.3 Configuración Técnica Key
```typescript
// Capacitor Config
const config: CapacitorConfig = {
  appId: 'com.air.app',
  appName: 'AIR',
  webDir: 'build',
  server: {
    androidScheme: 'https'
  },
  plugins: {
    Camera: {
      quality: 80,
      allowEditing: false
    },
    Geolocation: {
      enableHighAccuracy: true
    }
  }
};
```

---

**Documento:** `doc/other/srs-ieee830-air.md`  
**Última actualización:** octubre 2025  
**Próxima revisión:**  ---

---