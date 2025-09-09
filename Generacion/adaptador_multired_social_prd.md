# 📱 PRD: Adaptador Multi-Red Social con IA + Telegram + n8n (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**
Un sistema que transforma automáticamente un contenido en múltiples versiones optimizadas para cada red social, incluyendo copy, hashtags, dimensiones y formatos.

**Stack en la Nube:**
- 📱 **Telegram** - Input/Output de contenido
- ⚡ **n8n Cloud** - Motor de automatización
- 🖼️ **Sharp.js/Canvas API** - Procesamiento de imágenes
- 📝 **Claude/GPT-4** - Adaptación inteligente de copy
- 📊 **Airtable** - Templates y configuraciones
- 🎬 **FFmpeg Cloud** - Procesamiento de video

---

## 🎯 ¿Por qué Adaptación Multi-Red?

### **Problema Actual:**
- 📐 Cada red tiene requisitos diferentes
- ⏰ Adaptar manualmente toma horas
- 💰 Agencias cobran por cada versión
- 🔄 Mantener consistencia es difícil

### **Solución Automatizada:**
- 📸 Envías un contenido base
- 🤖 IA adapta para cada plataforma
- ✨ Recibes 10+ versiones optimizadas
- 📊 Todo en menos de 2 minutos

---

## 🎯 Plan de 15 Días Estructurado

### **SEMANA 1: ADAPTACIÓN BÁSICA (Días 1-7)**

#### **Día 1-2: Mapeo de Especificaciones** 📐
- [ ] **Investigar requisitos 2025 por plataforma:**
  - LinkedIn: 1200x627px posts, 1920x1080px videos
  - Instagram: 1080x1080px feed, 1080x1920px stories/reels
  - Facebook: 1200x630px posts, 1080x1920px stories
  - X/Twitter: 1200x675px posts, 1:1 y 16:9 videos
  - TikTok: 1080x1920px videos verticales
  - YouTube: 1280x720px thumbnails, 1080x1920px shorts

#### **Día 3-4: Motor de Redimensionado** 🖼️
- [ ] Detección inteligente de rostros y objetos
- [ ] Recorte con IA (mantener elementos importantes)
- [ ] Padding automático cuando necesario
- [ ] Optimización de peso por plataforma

#### **Día 5-6: Adaptación de Copy con IA** 📝
- [ ] **Tonos específicos por plataforma:**
  - LinkedIn: Profesional, insights, 1300 caracteres
  - Instagram: Visual, storytelling, 2200 caracteres
  - Twitter/X: Conciso, trending, 280 caracteres
  - TikTok: Gen Z, casual, 150 caracteres caption
  - Facebook: Conversacional, 63,206 caracteres max

#### **Día 7: Sistema de Hashtags** #️⃣
- [ ] Research automático de trending hashtags
- [ ] Generación contextual por nicho
- [ ] Límites óptimos: IG (30), LinkedIn (5), Twitter (2)
- [ ] Mix de alcance: populares + nicho + branded

### **SEMANA 2: AUTOMATIZACIÓN COMPLETA (Días 8-14)**

#### **Día 8-9: Templates Dinámicos** 🎨
- [ ] Plantillas por industria (tech, moda, food, etc.)
- [ ] Paletas de colores brand-safe
- [ ] Fuentes optimizadas para móvil
- [ ] Overlays y elementos gráficos dinámicos

#### **Día 10-11: Calendario Inteligente** 📅
- [ ] Mejores horarios por plataforma y zona
- [ ] Integración con Buffer/Hootsuite APIs
- [ ] Evitar saturación de audiencia
- [ ] Calendario visual exportable

#### **Día 12-13: Video Adaptation** 🎬
- [ ] Cortar videos para duraciones específicas
- [ ] Aspect ratios automáticos por plataforma
- [ ] Subtítulos quemados para autoplay
- [ ] Thumbnails optimizados con IA

#### **Día 14-15: Analytics y Optimización** 📊
- [ ] Predicción de engagement por plataforma
- [ ] A/B testing automático de variaciones
- [ ] Reportes de performance proyectado
- [ ] Sugerencias de mejora con IA

---

## 🛠️ Arquitectura de Workflows n8n

### **Workflow Multi-Adaptación:**
```mermaid
📱 Telegram Input (imagen/video/texto)
↓
🔧 Function: Detectar tipo de contenido
↓
📐 Switch por tipo:
├── Imagen → Sharp.js processor
├── Video → FFmpeg processor
└── Texto → Visual generator
↓
🧠 Claude/GPT: Generar copy adaptado
↓
🎨 Canvas: Aplicar templates y resize
↓
#️⃣ Function: Generar hashtags optimizados
↓
📊 Airtable: Guardar todas las versiones
↓
📦 ZIP: Empaquetar resultados
↓
📱 Telegram: Enviar preview grid + descarga
```
---

## 💡 Ejemplos de Adaptación

### **Input: Foto de producto + descripción**

**Output LinkedIn:**
- Imagen: 1200x627px con overlay profesional
- Copy: "Revolucionando la industria con innovación... [1300 chars]"
- Hashtags: #Innovation #TechTrends #BusinessGrowth

**Output Instagram:**
- Imagen: 1080x1080px centrada
- Copy: "✨ Nuevo lanzamiento que cambia todo... [storytelling]"
- Hashtags: 30 hashtags mixtos researched

**Output TikTok:**
- Video: 9:16 con música trending
- Copy: "POV: Encuentras el producto perfecto 💯"
- Hashtags: #FYP #Viral #TrendingNow

---

## 🗃️ Estructura de Datos

### **Tabla: `content_adaptations`**
┌──────────────────────────────────────────────────────────
│ Field           │ Type      │ Description               │
├──────────────────────────────────────────────────────────
│ adaptation_id   │ UUID      │ ID único del trabajo      │
│ user_id         │ Number    │ Telegram User ID          │
│ original_url    │ URL       │ Contenido original        │
│ platform        │ Select    │ Red social target         │
│ adapted_url     │ URL       │ Versión adaptada          │
│ copy_text       │ Long Text │ Copy optimizado           │
│ hashtags        │ Array     │ Hashtags generados        │
│ dimensions      │ Text      │ Dimensiones finales       │
│ engagement_score│ Number    │ Predicción de engagement  │
│ created_at      │ Timestamp │ Fecha de creación         │
└──────────────────────────────────────────────────────────
---

## 📊 Especificaciones por Red Social 2025

### **LinkedIn**
- Posts: 1200x627px, 8MB max
- Videos: 10min max, 5GB
- Copy: 1300 chars (200 visible)
- Hashtags: 3-5 óptimo

### **Instagram**
- Feed: 1080x1080px (1:1)
- Stories/Reels: 1080x1920px (9:16)
- Copy: 2200 chars
- Hashtags: 10-30 óptimo

### **Facebook**
- Posts: 1200x630px
- Stories: 1080x1920px
- Copy: 63,206 chars max
- Videos: 240min max, 10GB

### **X/Twitter**
- Posts: 1200x675px
- Copy: 280 chars
- Videos: 2:20 max
- Hashtags: 1-2 óptimo

### **TikTok**
- Videos: 1080x1920px
- Duración: 10min max
- Copy: 150 chars visible
- Hashtags: 3-5 trending

### **YouTube**
- Thumbnails: 1280x720px
- Shorts: 1080x1920px, 60s max
- Títulos: 100 chars
- Descripción: 5000 chars

---

## 💰 Estimación de Costos

- **Procesamiento de imágenes:** $0.001 por imagen
- **Claude/GPT para copy:** $0.01 por adaptación
- **5 redes x 100 posts:** ~$5/mes
- **Almacenamiento:** Gratis (Cloudinary)
- **n8n Cloud:** Gratis
- **Total:** $5-10/mes para uso moderado

---

## 🎯 Criterios de Éxito

- [ ] ✅ Adaptar a 5+ redes sociales
- [ ] 📐 100% de dimensiones correctas
- [ ] 📝 Copy optimizado por plataforma
- [ ] #️⃣ Hashtags researched y relevantes
- [ ] ⚡ Proceso completo < 2 minutos
- [ ] 📊 Preview visual de todas las versiones

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Sistema completo de adaptación multi-red**
✅ **Ahorro de 90% en tiempo de adaptación**
✅ **Consistencia de marca en todas las plataformas**
✅ **Pipeline escalable para agencias**
✅ **Conocimiento profundo de cada red social**

**¡15 días para automatizar tu presencia en redes sociales!** 🚀