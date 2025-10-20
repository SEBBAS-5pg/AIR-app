# 📘 ESPECIFICACIÓN DE REQUISITOS DE SOFTWARE (SRS) - IEEE 830

**Proyecto:** AIR (A Image Real) - Red Social de Fotos Espontáneas  
**Versión:** 1.0.2 (MVP)  
**Fecha:** Agosto 2025  
**Responsable:** Sebastián Puentes Gonzalez  
**Estado:** En Desarrollo

---

## 1.1 Introducción

### 1.1.1 Propósito

Este documento especifica los requisitos funcionales y no funcionales para la aplicación móvil **AIR (A Image Real)**, una plataforma diseñada para facilitar la captura y compartición espontánea de momentos geolocalizados, reduciendo la barrera de la perfección en redes sociales tradicionales.

### 1.1.2 Alcance

**AIR** es una aplicación móvil híbrida desarrollada en **React Native** (recomendado) o **Ionic con React**, con backend en **Firebase/Firestore**.

**Alcance del MVP:**

- Autenticación y registro de usuarios
- Captura rápida de fotos con geolocalización automática
- Feed principal con contenido de amigos y ubicación
- Perfiles básicos de usuario
- Almacenamiento local para funcionalidad offline limitada

**Exclusiones del MVP:**

- Perfiles empresariales avanzados
- Integración con APIs de música
- Sistema de mensajería privada
- Análiticas avanzadas

### 1.1.3 Definiciones, Acrónimos y Abreviaturas

| Término      | Definición                                      |
| ------------ | ----------------------------------------------- |
| **AIR**      | A Image Real - Nombre de la aplicación          |
| **Dump**     | Publicación individual de un momento espontáneo |
| **Feed**     | Flujo principal de contenido de la aplicación   |
| **GeoPoint** | Coordenadas geográficas (latitud, longitud)     |
| **MVP**      | Producto Mínimo Viable                          |
| **RF**       | Requisito Funcional                             |
| **RNF**      | Requisito No Funcional                          |
| **SRS**      | Especificación de Requisitos de Software        |

### 1.1.4 Referencias

- IEEE Std 830-1998 - Estándar para Especificación de Requisitos de Software
- Documentación oficial de React Native
- Guías de Material Design (Android) y Human Interface Guidelines (iOS)
- Políticas de privacidad de Google Play Store y Apple App Store
- Documento: `doc/backlog/user-stories.md`
- Documento: `doc/architecture/data-model.md`

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

- **Cliente Móvil**: Aplicación iOS/Android desarrollada en React Native
- **Backend como Servicio**: Firebase (Authentication, Firestore, Storage)
- **Servicios Externos**: APIs de geolocalización (Google Maps/Apple Maps)
- **Almacenamiento Local**: SQLite para caché y funcionalidad offline

### 1.2.2 Funciones del Producto

1. **Gestión de Usuarios**

   - Registro y autenticación
   - Perfiles de usuario básicos
   - Sistema de seguimiento entre usuarios

2. **Captura de Momentos**

   - Acceso rápido a cámara
   - Geolocalización automática
   - Metadatos contextuales

3. **Contenido y Descubrimiento**

   - Feed principal personalizado
   - Búsqueda por ubicación
   - Contenido offline favorito

4. **Gestión de Datos**
   - Sincronización en segundo plano
   - Almacenamiento local eficiente
   - Gestión de permisos

### 1.2.3 Características de los Usuarios

| Tipo de Usuario         | Perfil                                                         | Edad  | Nivel Tecnológico | Frecuencia de Uso          |
| ----------------------- | -------------------------------------------------------------- | ----- | ----------------- | -------------------------- |
| **Usuario Individual**  | Personas que buscan compartir momentos espontáneos sin edición | 18-35 | Medio             | Diario (2-5 veces/día)     |
| **Usuario Empresarial** | Negocios locales que buscan visibilidad orgánica               | 20-40 | Medio-Alto        | Semanal (3-5 veces/semana) |

### 1.2.4 Restricciones

- **Tecnológicas**: Desarrollo con React Native, Firebase como BaaS
- **Temporales**: Entrega en ciclo académico (16 semanas)
- **Plataforma**: Publicación en App Store y Google Play Store
- **Legales**: Cumplimiento de GDPR/LGPD para datos de ubicación

### 1.2.5 Supuestos y Dependencias

- **Conectividad**: Los usuarios tendrán acceso intermitente a internet
- **Dispositivos**: Los usuarios contarán con smartphones con cámara y GPS
- **Servicios**: Firebase mantendrá disponibilidad del 99.9%
- **Permisos**: Los usuarios concederán permisos de cámara y ubicación

---

## 1.3 Requerimientos Específicos

### 1.3.1 Interfaces Externas

- **Interfaz de Usuario**: Diseño minimalista centrado en contenido, siguiendo principios de Material Design 3 y HIG
- **Interfaz de Hardware**: Cámara, GPS, almacenamiento local
- **Interfaz de Comunicaciones**: REST APIs con Firebase, WebSockets para actualizaciones en tiempo real

### 1.3.2 Funciones del Sistema (RF)

**RF-001 - Autenticación de Usuario**

- El sistema debe permitir registro con email y contraseña
- El sistema debe permitir autenticación con Google Sign-In
- El usuario debe poder recuperar contraseña

**RF-002 - Captura de Momentos**

- La aplicación debe acceder a la cámara en menos de 1 segundo
- La captura de foto debe incluir metadatos de ubicación automáticamente
- El usuario debe poder añadir descripción opcional antes de publicar

**RF-003 - Gestión de Feed**

- El feed debe cargar contenido en orden cronológico inverso
- El sistema debe priorizar contenido de usuarios seguidos
- Debe permitir pull-to-refresh para actualizar contenido

_(Lista completa en `./doc/backlog/historias de usuario.md`)_

### 1.3.3 Rendimiento (RNF-Performance)

| Código           | Requisito                                | Valor Objetivo |
| ---------------- | ---------------------------------------- | -------------- |
| **RNF-PERF-001** | Tiempo de carga inicial de la aplicación | < 3 segundos   |
| **RNF-PERF-002** | Tiempo de apertura de cámara             | < 1 segundo    |
| **RNF-PERF-003** | Tiempo de carga del feed                 | < 2 segundos   |
| **RNF-PERF-004** | Uso de memoria en dispositivos básicos   | < 150 MB RAM   |

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
}

Dumps {
  dumpId: string (UUID)
  userId: string
  imageUrl: string
  caption: string
  location: GeoPoint
  timestamp: timestamp
  visibility: 'public' | 'friends' | 'private'
  taggedBusiness: string (optional)
}

{
  Interactions{
    interactionId: String(UUID)
    userId: string
    dumpId: string
    type: 'like' | 'coment' | 'share'
    createAt: timestamp
  }
}

{
  Businesses{
    businessId: string(UUID)
    name: string
    description: string
    category: string
    address: string
    geopoint: geopoint
    contactEmail: string
    phone: string
    website: string
    dumpCount: number
    ownerId: string
    isVeryfield: boolea
    createAt: timestamp
  }
}
```

### 1.3.5 Restricciones de Diseño

- **Compatibilidad**: iOS 13+ y Android 8.0+ (API 26+)
- **Accesibilidad**: Soporte para VoiceOver (iOS) y TalkBack (Android)
- **Diseño Responsive**: Soporte para pantallas desde 4.7" hasta 6.7"
- **Navegación**: Patrón de navegación por pestañas inferior

### 1.3.6 Atributos del Sistema (RNF)

| Categoría          | Requisitos                                                                                                            |
| ------------------ | --------------------------------------------------------------------------------------------------------------------- |
| **Seguridad**      | Autenticación con Firebase Auth, datos en tránsito cifrados con TLS 1.2+, validación de entrada en cliente y servidor |
| **Disponibilidad** | 99% uptime durante horario pico (18:00-23:00)                                                                         |
| **Mantenibilidad** | Código documentado, arquitectura modular, uso de ESLint y Prettier                                                    |
| **Usabilidad**     | Tiempo de aprendizaje < 5 minutos, touch targets ≥ 44x44 dp                                                           |

### 1.3.7 Requisitos de Internacionalización/Localización

- **Idioma Principal**: Español
- **Soporte Futuro**: Inglés, Portugués
- **Formato**: Fechas y horas según configuración regional del dispositivo

### 1.3.8 Requisitos Legales y de Privacidad

- **Política de Privacidad**: Explicación clara del uso de datos de ubicación
- **Consentimiento**: Obtención explícita para recolección de datos sensibles
- **Derechos del Usuario**: Capacidad de eliminar cuenta y todos los datos asociados
- **Edad Mínima**: 18 años de edad

---

## 1.4 Apéndices

### 1.4.1 Diagrama de Arquitectura Simplificado

_(Ver `./doc/architecture/Arquitectura del Sistema.md`)_

### 1.4.2 Políticas de Datos

- Retención de datos: 36 meses de inactividad
- Backup automático cada 24 horas
- Exportación de datos de usuario disponible on-demand

---

**Documento:** SSR_IEE830  
**Última actualización:** octubre 2025  
**Próxima revisión:** ---

---
