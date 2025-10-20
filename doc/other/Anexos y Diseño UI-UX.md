# AIR - Anexos y Diseño UX/UI

## 📋 Información General

- **Proyecto**: AIR (A Image Real)
- **Versión**: 1.2 (Diseño de Interfaz Inicial)
- **Fecha**: Octubre 2025
- **Responsable**: Equipo de Diseño UX/UI
- **Estado**: Diseño Inicial - Iterativo

## 🎨 Filosofía de Diseño

**Enfoque**: "Las imágenes son el protagonista" - Interfaz que desaparece para destacar el contenido visual espontáneo.

**Principios Clave**:
- Minimalismo radical
- Contenido sobre chrome
- Acciones con un solo toque
- Oscuro para reducir fatiga visual

## 🎯 Esquema de Navegación Principal

Navegación por pestañas inferiores (IonTabs) para acceso rápido:

| Pestaña | Icono | Destino | Propósito |
|---------|-------|---------|-----------|
| **Feed** | 🏠 | FeedPage | Consumo principal de contenido |
| **Cámara** | 📸 | CameraPage | Acción principal - captura rápida |
| **Perfil** | 👤 | ProfilePage | Gestión personal y actividad |

## 🖼️ Paleta de Colores - Modo Oscuro

### Colores Base
```css
/* Foundation */
--air-black: #000000;
--air-dark: #121212;
--air-gray-800: #1E1E1E;
--air-gray-700: #2D2D2D;
--air-gray-600: #404040;

/* Texto */
--air-text-primary: #FFFFFF;
--air-text-secondary: #A0A0A0;
--air-text-disabled: #666666;

/* Acento */
--air-accent: #00D4AA; /* Verde azulado - sutil pero visible */
--air-accent-hover: #00B894;
```

### Aplicación de Colores
- **Fondo**: `--air-black` para fondo principal
- **Cards**: `--air-gray-800` con bordes sutiles
- **Texto**: Blanco puro para primario, gris para secundario
- **Botones**: Acento solo para acciones primarias

## 📱 Vistas Principales - Wireframes Conceptuales

### MOCKUP 1: Feed Principal (FeedPage)
**Objetivo**: Scroll infinito sin distracciones

**Layout**:
```
[Header sutil - Logo AIR]
|
[IonContent]
│
├── DumpCard 1
│   ├── [Imagen 16:9 - Ocupa 80% del card]
│   ├── [User Avatar + Name - línea superior]
│   ├── [Location Chip - línea inferior] 
│   └── [Like/Save - barra acciones inferior]
│
├── DumpCard 2
│   └── ...
│
[IonInfiniteScroll]
|
[IonTabs - Feed • Cámara • Perfil]
```

**Características**:
- Cards con bordes redondeados mínimos
- Espaciado generoso entre cards
- Sin sombras pesadas
- Imágenes con relación 16:9 optimizada

### MOCKUP 2: Cámara (CameraPage)  
**Objetivo**: Captura instantánea sin fricción

**Layout**:
```
[Fondo negro puro]
|
[Vista previa cámara - pantalla completa]
|
[Barra inferior flotante]
   ├── [Botón flip cámara]
   ├── [Botón captura - círculo grande acento]
   └── [Botón galería]
```

**Interacciones**:
- Botón de captura: 64x64px, color acento
- Gestos: Tap para enfocar, doble tap para flip
- Feedback: Vibración sutil al capturar

### MOCKUP 3: Revisión Post-Captura (PostReviewPage)
**Objetivo**: Metadatos rápidos sin obstruir la imagen

**Layout**:
```
[Imagen capturada - fondo]
|
[Overlay inferior translúcido]
   ├── [IonTextarea - caption opcional]
   ├── [IonSegment - público/amigos/privado]
   ├── [Chip negocio etiquetado - opcional]
   └── [Botón Publicar - acento]
```

### MOCKUP 4: Perfil de Usuario (ProfilePage)
**Objetivo**: Historial personal claro

**Layout**:
```
[Header perfil]
   ├── [Avatar usuario]
   ├── [Stats: Seguidores/Seguidos/Dumps]
   └── [Botón editar]
|
[IonTabs - Mis Dumps • Guardados]
|
[Grid de imágenes]
   └── [Thumbnails 1:1 con badges de tiempo]
```

## 🎪 Componentes de Diseño Reutilizables

### DumpCard
- **Imagen**: Relación 16:9, bordes redondeados 8px
- **Contenido**: Padding mínimo, tipografía compacta
- **Acciones**: Iconos outline, fill al activar

### Botones y Controles
- **Primarios**: Color acento, texto oscuro para contraste
- **Secundarios**: Outline blanco, fondo transparente
- **Iconos**: Family Ionicons, peso regular

### Estados de Interfaz
```css
/* Loading */
.skeleton {
  background: linear-gradient(90deg, #1E1E1E 25%, #2D2D2D 50%, #1E1E1E 75%);
}

/* Estados vacíos */
.empty-state {
  color: var(--air-text-secondary);
  text-align: center;
  padding: 3rem;
}
```

## 🔧 Estándares de Usabilidad

### Navegación
- **Tabs inferiores**: Siempre visibles, labels cortos
- **Gestos**: Pull-to-refresh en feed, swipe en imágenes
- **Back navigation**: Header consistente con botón atrás

### Accesibilidad
- **Touch targets**: Mínimo 44x44px
- **Contraste**: Texto 4.5:1 mínimo sobre fondos
- **VoiceOver**: Labels descriptivos para elementos interactivos

### Performance Visual
- **Lazy loading**: Imágenes fuera de viewport
- **Placeholders**: Skeleton screens durante carga
- **Transiciones**: Suaves pero rápidas (200-300ms)

## 🚀 Flujos de Interacción Principales

### Flujo Publicación Rápida
```
Feed → Tap Cámara (500ms) → Capturar → Revisión (opcional) → Publicar → Volver Feed
```

### Flujo Consumo
```
Feed → Scroll infinito → Tap imagen (modal) → Interactuar → Volver
```

### Flujo Perfil
```
Perfil → Ver historial → Tap dump → Modal detalle → Volver
```

## 🔄 Consideraciones para Iteraciones Futuras

### Mejoras de UX Pendientes
- [ ] Micro-interacciones más refinadas
- [ ] Modo claro opcional
- [ ] Temas de color personalizables
- [ ] Soporte para más gestos

### Validación Needed
- [ ] Testeo de contraste en dispositivos reales
- [ ] Feedback de usuarios sobre flujo cámara
- [ ] Optimización de tiempos de carga percibidos

---

**Documento**: `doc/design/ux-ui-guide.md`  
**Última actualización**: Octubre 2025  
**Próxima revisión**: ---

**Nota**: Este diseño es iterativo y evolucionará basado en testing de usabilidad y feedback de usuarios beta.