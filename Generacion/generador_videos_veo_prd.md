# 🎬 PRD: Generador de Videos con IA + Telegram + n8n (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**
Un sistema que genera videos cortos (3-10 segundos) usando IA a partir de prompts de texto o imágenes base, optimizado para redes sociales.

**Stack en la Nube:**
- 📱 **Telegram** - Interface de usuario
- ⚡ **n8n Cloud** - Orquestación de workflows
- 🎬 **APIs de Video IA:**
  - 🥇 **Veo (Google)** - Alta calidad, buenos precios
  - 🥈 **Stability Video** - Económico y eficiente
  - 🥉 **Pika Labs** - Opción gratuita con límites
- 📊 **Bunny CDN** - Streaming optimizado
- 🧠 **Claude/GPT** - Optimización de prompts

---

## 🎯 ¿Por qué Generación de Videos con IA?

### **Problema Actual:**
- 🎬 Producción de video es cara y compleja
- ⏰ Edición toma días o semanas
- 💰 Equipo y software costosos
- 👥 Requiere equipo especializado

### **Solución con IA:**
- 💬 Describes el video que necesitas
- 🤖 IA genera video en minutos
- 📱 Optimizado para redes sociales
- 🔄 Iteraciones rápidas ilimitadas

---

## 🎯 Plan de 15 Días Estructurado

### **SEMANA 1: GENERACIÓN BÁSICA (Días 1-7)**

#### **Día 1-2: Setup de APIs de Video** 🎬
- [ ] Configurar Veo API (Google)
- [ ] Comparar alternativas y costos
- [ ] Setup Bunny CDN para streaming
- [ ] Crear estructura de almacenamiento

#### **Día 3-4: Text-to-Video Básico** 📹
- [ ] Workflow de generación simple
- [ ] Comando `/video [descripción]`
- [ ] Sistema de cola para procesamiento largo
- [ ] Notificaciones de progreso (1%, 50%, 100%)

#### **Día 5-6: Image-to-Video** 🖼️
- [ ] Animar imágenes estáticas
- [ ] Control de movimiento de cámara
- [ ] Efectos de transición
- [ ] Duraciones configurables (3s, 5s, 10s)

#### **Día 7: Optimización de Calidad** ✨
- [ ] Resoluciones múltiples (720p, 1080p, 4K)
- [ ] FPS configurable (24, 30, 60)
- [ ] Codecs optimizados para cada red social
- [ ] Compresión inteligente sin pérdida visible

### **SEMANA 2: FEATURES PROFESIONALES (Días 8-14)**

#### **Día 8-9: Templates por Industria** 🎨
- [ ] **E-commerce:** Productos 360°, unboxing
- [ ] **Real Estate:** Tours virtuales, walkthroughs
- [ ] **Educación:** Explicativos, tutoriales
- [ ] **Marketing:** Ads dinámicos, promos

#### **Día 10-11: Edición Avanzada** ✂️
- [ ] Música de fondo (biblioteca libre de copyright)
- [ ] Subtítulos automáticos multi-idioma
- [ ] Watermarks y branding personalizable
- [ ] Efectos de color, filtros y LUTs

#### **Día 12-13: Formatos Multi-Plataforma** 📱
- [ ] **Instagram Reels:** 9:16, 30-60s
- [ ] **YouTube Shorts:** 9:16, hasta 60s
- [ ] **TikTok:** 9:16, 15-60s
- [ ] **LinkedIn:** 16:9, 30s-10min
- [ ] **Stories:** 9:16 con safe zones

#### **Día 14-15: Sistema Completo** 🚀
- [ ] Biblioteca de videos generados
- [ ] Re-generación con variaciones
- [ ] Export bulk en diferentes formatos
- [ ] Analytics de generación y estilos

---

## 🛠️ Arquitectura de Workflows n8n

### **Workflow de Generación de Video:**
```mermaid
📱 Telegram Trigger (prompt o imagen)
↓
🔧 Function: Validar input y tipo
↓
🧠 Claude/GPT: Optimizar prompt de video
↓
🎬 Veo API: Generar video base
↓
⏳ Wait Node: Polling de status
↓
🎵 FFmpeg: Agregar audio/subtítulos
↓
☁️ Bunny CDN: Upload y streaming
↓
📊 Airtable: Guardar metadata
↓
📱 Telegram: Enviar video final
```
---

## 💡 Ejemplos de Generación

### **Producto (E-commerce):**
Prompt: "Zapatillas deportivas rojas girando 360 grados,
fondo blanco minimalista, iluminación de estudio"
Resultado: Video 5s, 1080p, perfecto para Amazon/Shopify

### **Marketing (Redes Sociales):**
Prompt: "Texto 'OFERTA 50%' apareciendo con efectos de neón,
fondo urbano nocturno, estilo cyberpunk"
Resultado: Video 3s loop, formatos para todas las redes

### **Educativo (Cursos):**
Prompt: "Manos escribiendo código en laptop, time-lapse,
ambiente de oficina moderna, luz natural"
Resultado: Video 10s, con espacio para voice-over

---

## 🗃️ Estructura de Datos

### **Tabla: `video_generations`**
┌─────────────────────────────────────────────────────
│ Field          │ Type      │ Description         │
├─────────────────────────────────────────────────────
│ video_id       │ UUID      │ ID único            │
│ user_id        │ Number    │ Telegram User ID    │
│ prompt         │ Text      │ Descripción usada   │
│ video_url      │ URL       │ CDN link            │
│ duration       │ Number    │ Segundos            │
│ resolution     │ Select    │ 720p/1080p/4K       │
│ style          │ Text      │ Estilo aplicado     │
│ platform       │ Select    │ Red social target   │
│ generation_time│ Number    │ Tiempo en segundos  │
│ created_at     │ Timestamp │ Fecha creación      │
└─────────────────────────────────────────────────────
---

## 💰 Estimación de Costos

- **Veo API:** ~$0.05 por segundo de video
- **Video de 5s:** ~$0.25
- **100 videos/mes:** ~$25
- **Bunny CDN:** $1-5/mes
- **n8n Cloud:** Gratis
- **Total:** $25-35/mes para 100 videos

---

## 🎯 Criterios de Éxito

- [ ] ✅ Generar 50+ videos únicos
- [ ] 🎬 3 formatos de video funcionales
- [ ] ⚡ Generación < 5 minutos
- [ ] 📱 Optimizado para 5+ plataformas
- [ ] 🎵 Sistema de audio funcional

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Generador de videos profesional**
✅ **Templates para múltiples industrias**
✅ **Pipeline de post-producción automático**
✅ **Biblioteca de videos generados**
✅ **Sistema escalable con n8n**

**¡15 días para crear tu propio estudio de video con IA!** 🚀
