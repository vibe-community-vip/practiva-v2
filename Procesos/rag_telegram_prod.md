# 🤖 PRD: Bot RAG con Telegram + n8n Cloud (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**  
Un bot de Telegram inteligente que usa RAG (Retrieval-Augmented Generation) para responder preguntas basándose en documentos específicos usando APIs de IA en la nube.

**Stack en la Nube:**
- 📱 **Telegram** - Canal de comunicación  
- ⚡ **n8n Cloud** - Motor de automatización (plan gratuito)  
- 🤗 **HuggingFace** - Embeddings gratuitos  
- 📊 **Airtable** - Base de vectores simplificada  
- 🧠 **OpenAI/Claude/Gemini** - LLM via API (opción libre)

**Diferencia vs FAQs Simples:**  
En lugar de buscar coincidencias exactas, RAG entiende el contexto y genera respuestas inteligentes basadas en tus documentos.

---

## 🎯 ¿Qué es RAG? (Explicación para Principiantes)

### **Analogía Simple:**
Imagina que tienes un **asistente super inteligente** que:
1. 📚 **Lee toda tu biblioteca** de documentos empresariales
2. 🧠 **Entiende y memoriza** el contenido (pero en formato matemático)
3. 🔍 **Busca información relevante** cuando le preguntas algo
4. 💬 **Genera respuestas naturales** combinando lo que encontró

### **Ejemplo Práctico:**
- **Sin RAG:** "No sé sobre políticas de vacaciones"
- **Con RAG:** "Según el manual de RRHH que tengo indexado, puedes solicitar hasta 15 días consecutivos con 30 días de anticipación..."

### **Por qué RAG es revolucionario:**
- ✅ Respuestas basadas en TUS documentos
- ✅ Actualizable sin reentrenar modelos
- ✅ Cita fuentes específicas
- ✅ Entiende contexto y sinónimos

---

## 🎯 Plan de 15 Días Simplificado

### **SEMANA 1: FUNDAMENTOS RAG (Días 1-7)**

#### **Día 1: Setup en la Nube** ☁️
- [ ] Crear cuenta gratuita en n8n Cloud
- [ ] Crear bot con @BotFather en Telegram
- [ ] Configurar webhook Telegram en n8n
- [ ] **Elegir tu API de IA:**
  - 🔥 **OpenAI** (ChatGPT) - $5 inicial, muy estable
  - 🎯 **Anthropic** (Claude) - $5 inicial, excelente para texto
  - 🌟 **Google** (Gemini) - Plan gratuito disponible

#### **Día 2: Preparar Documentos** 📚
- [ ] Recopilar 5-10 documentos de prueba (máx 2-3 páginas cada uno)
- [ ] **Ejemplos sugeridos:**
  - Manual de empleado básico
  - FAQ de producto
  - Políticas de empresa
  - Guía de procesos
- [ ] Convertir a texto plano (copiar/pegar en Google Docs)

#### **Día 3: Base de Datos Simple** 🗄️
- [ ] Crear cuenta gratuita en Airtable
- [ ] Crear tabla "Knowledge_Base" con campos:
  - `ID` (auto-número)
  - `Document_Title` (texto)
  - `Content_Chunk` (texto largo)
  - `Embedding` (texto largo) - para guardar vectores
  - `Source` (texto)
- [ ] Poblar manualmente 10 chunks de ejemplo

#### **Día 4-5: Embeddings con HuggingFace** 🤗
- [ ] Configurar credenciales HuggingFace en n8n (API gratuita)
- [ ] Crear workflow "RAG-Indexer":
  - Leer texto de Airtable
  - Generar embedding con HuggingFace
  - Guardar embedding en Airtable
- [ ] **Modelo recomendado:** `sentence-transformers/all-MiniLM-L6-v2`
- [ ] Procesar tus 10 chunks iniciales

#### **Día 6-7: Primera Búsqueda RAG** 🔍
- [ ] Crear Function node para calcular similitud coseno
- [ ] Workflow básico: Pregunta → Embedding → Buscar similar → Responder
- [ ] **Testing:** Preguntar algo relacionado con tus documentos
- [ ] **Objetivo:** Encontrar el chunk más relevante

### **SEMANA 2: FUNCIONALIDADES AVANZADAS (Días 8-14)**

#### **Día 8-9: Integración con LLM** 🧠
- [ ] **Configurar tu API elegida:**
  
  **Opción A: OpenAI (Recomendado para principiantes)**
  ```
  Endpoint: https://api.openai.com/v1/chat/completions
  Modelo: gpt-4o-mini (más barato)
  Costo: ~$0.002 por 1K tokens
  ```
  
  **Opción B: Claude (Anthropic)**
  ```
  Endpoint: https://api.anthropic.com/v1/messages
  Modelo: claude-3-haiku-20240307 (más barato)
  Costo: ~$0.0008 por 1K tokens
  ```
  
  **Opción C: Gemini (Google)**
  ```
  Endpoint: https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent
  Modelo: gemini-pro
  Costo: Gratis hasta 60 req/min
  ```

#### **Día 10-11: Prompt Engineering** 📝
- [ ] Crear template de prompt RAG:
```
Eres un asistente experto. Responde basándote ÚNICAMENTE en el contexto proporcionado.

CONTEXTO:
{chunks_relevantes}

PREGUNTA: {pregunta_usuario}

INSTRUCCIONES:
- Si la respuesta está en el contexto, responde de forma clara y natural
- Si NO está en el contexto, di "No tengo esa información en mis documentos"
- Cita la fuente al final: "Fuente: {nombre_documento}"

RESPUESTA:
```
- [ ] Testing con diferentes tipos de preguntas
- [ ] Ajustar prompt según resultados

#### **Día 12-13: Features de Usuario** 👥
- [ ] Comandos básicos:
  - `/start` - Bienvenida y explicación
  - `/help` - Cómo usar el bot
  - `/example` - Ejemplo de pregunta
- [ ] Manejo de errores graceful
- [ ] Logging básico en Airtable (usuario, pregunta, respuesta)

#### **Día 14: Optimización Simple** ⚡
- [ ] Limitar búsqueda a top 3 chunks más relevantes
- [ ] Agregar typing indicator en Telegram
- [ ] Respuestas formateadas con emojis
- [ ] Testing de performance con múltiples consultas

### **Día 15: Entrega Final** 🎯
- [ ] Testing completo del flujo RAG
- [ ] Documentación de setup y uso
- [ ] Video demo de 3-5 minutos
- [ ] Preparar presentación explicando RAG

---

## 🛠️ Arquitectura Técnica Simplificada

### **Workflow Principal n8n:**

```
📱 Telegram Trigger
    ↓
🔧 Function: Procesar pregunta
    ↓
🤗 HuggingFace: Generar embedding de pregunta
    ↓
📊 Airtable: Buscar chunks con embeddings similares
    ↓
🔧 Function: Calcular similitud y seleccionar top 3
    ↓
🔧 Function: Construir prompt con contexto
    ↓
🧠 HTTP Request: API LLM (OpenAI/Claude/Gemini)
    ↓
🔧 Function: Procesar respuesta
    ↓
📱 Telegram: Enviar respuesta al usuario
    ↓
📊 Airtable: Log de la interacción
```

### **Estructura de Datos Airtable:**

```
Tabla: Knowledge_Base
┌─────────────────────────────────────────────────────┐
│ ID │ Title │ Content_Chunk │ Embedding │ Source    │
├─────────────────────────────────────────────────────┤
│ 1  │ RRHH  │ "Las vacaciones se │ [0.1,-0.3...] │ Manual │
│    │       │ solicitan con 30   │               │ V1.2   │
│    │       │ días de anticip..." │               │        │
├─────────────────────────────────────────────────────┤
│ 2  │ RRHH  │ "El horario flexi- │ [0.4,0.1...]  │ Manual │
│    │       │ ble permite..."    │               │ V1.2   │
└─────────────────────────────────────────────────────┘

Tabla: Query_Logs
┌────────────────────────────────────────────────────┐
│ ID │ User │ Question │ Answer │ Timestamp │ Source │
└────────────────────────────────────────────────────┘
```

---

## 📋 Checklist de Funcionalidades

### **Core RAG (Obligatorio - 80% del valor):**
- [ ] ✅ Convierte documentos en embeddings
- [ ] 🔍 Busca chunks relevantes por similitud semántica
- [ ] 🤖 Genera respuestas contextuales con LLM
- [ ] 📚 Incluye citas de fuentes

### **UX Básico (Deseable - 15% del valor):**
- [ ] 💬 Comandos de ayuda claros
- [ ] ⚡ Respuestas en menos de 10 segundos
- [ ] 😊 Manejo amigable de errores
- [ ] 📝 Formato de respuesta legible

### **Analytics (Bonus - 5% del valor):**
- [ ] 📊 Log de todas las consultas
- [ ] 📈 Métricas básicas de uso
- [ ] 🔍 Tracking de chunks más consultados

---

## 💰 Estimación de Costos (Muy Bajo)

### **APIs de IA - Elige la mejor para ti:**

#### **🥇 Opción 1: Gemini (Google) - GRATIS**
- ✅ **Costo:** $0 hasta 60 requests/minuto
- ✅ **Pros:** Completamente gratis para testing
- ❌ **Contras:** Límites de rate más estrictos

#### **🥈 Opción 2: OpenAI (ChatGPT) - ~$2-5/mes**
- ✅ **Costo:** ~$0.002 por 1K tokens (muy barato)
- ✅ **Pros:** Muy estable, documentación excelente
- ✅ **Para 1000 consultas:** ~$2-3

#### **🥉 Opción 3: Claude (Anthropic) - ~$1-3/mes**
- ✅ **Costo:** ~$0.0008 por 1K tokens (más barato)
- ✅ **Pros:** Excelente para análisis de texto
- ✅ **Para 1000 consultas:** ~$1-2

### **Otras Herramientas:**
- 🆓 **n8n Cloud:** Plan gratuito (5,000 operaciones/mes)
- 🆓 **Airtable:** Plan gratuito (1,200 records)
- 🆓 **HuggingFace:** API gratuita para embeddings
- 🆓 **Telegram:** Completamente gratis

**💡 Total estimado para aprender: $0-5 por mes máximo**

---

## 🎯 Criterios de Éxito

### **Funcionalidad RAG (70%):**
- [ ] Bot encuentra información relevante en documentos indexados
- [ ] Genera respuestas naturales basadas en contexto
- [ ] No alucina información que no está en los documentos
- [ ] **Test:** 8/10 preguntas respondidas correctamente

### **Calidad Técnica (20%):**
- [ ] Workflow n8n funciona sin errores
- [ ] Embeddings y búsqueda por similitud operativos
- [ ] API de LLM integrada correctamente
- [ ] **Test:** Sistema estable por 48 horas

### **Comprensión RAG (10%):**
- [ ] Documentación explica cada paso del proceso
- [ ] Demo muestra diferencia vs búsqueda tradicional
- [ ] **Test:** Explicar RAG en 3 minutos a otra persona

---

## 💡 Ejemplos de Preguntas para Testing

### **Nivel Básico (Información directa):**
- "¿Cuántos días de vacaciones tengo?"
- "¿Cuál es el horario de oficina?"
- "¿Cómo solicito un permiso?"

### **Nivel Intermedio (Contexto):**
- "¿Puedo trabajar remoto si estoy enfermo?"
- "¿Qué pasa si llego tarde por tráfico?"
- "¿Hay descuentos en el gimnasio?"

### **Nivel Avanzado (Inferencia):**
- "¿Qué opciones tengo si quiero más flexibilidad laboral?"
- "¿Cómo afecta mi evaluación si tomo muchas vacaciones?"
- "¿Puedo cambiar mi horario por estudios?"

---

## 🔗 Referencias y Tutoriales

### **RAG Conceptos:**
- [¿Qué es RAG? - AWS](https://aws.amazon.com/what-is/retrieval-augmented-generation/) - Explicación conceptual clara de RAG
- [RAG Tutorial - LangChain](https://python.langchain.com/docs/tutorials/rag/) - Tutorial técnico paso a paso
- [RAG Guide - Pinecone](https://www.pinecone.io/learn/retrieval-augmented-generation/) - Guía completa con ejemplos

### **n8n Específico:**
- [n8n RAG Chatbot](https://blog.n8n.io/rag-chatbot/) - Tutorial oficial de n8n para crear chatbots RAG
- [Telegram + n8n](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/) - Documentación completa del nodo Telegram
- [HuggingFace Embeddings n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.embeddingshuggingfaceinference/) - Configuración de embeddings

### **APIs de IA:**
- [OpenAI API Docs](https://platform.openai.com/docs/api-reference) - Documentación oficial de OpenAI
- [Claude API Docs](https://docs.anthropic.com/claude/reference/) - Documentación de Anthropic
- [Gemini API Docs](https://ai.google.dev/docs) - Documentación de Google AI

### **Herramientas Gratuitas:**
- [Airtable Guides](https://support.airtable.com/docs) - Documentación para usar Airtable como base de datos
- [HuggingFace Models](https://huggingface.co/sentence-transformers) - Modelos de embeddings gratuitos

---

## 🚀 Tips para Éxito Garantizado

### **🎯 Enfoque en lo Esencial:**
1. **Semana 1:** Haz que funcione básicamente
2. **Semana 2:** Mejora la experiencia de usuario
3. **No te compliques** con optimizaciones avanzadas

### **📚 Preparación de Documentos:**
- ✅ **Documentos cortos** (2-3 páginas máximo)
- ✅ **Texto claro** sin tablas complejas
- ✅ **Contenido variado** para testing diverso
- ❌ **Evita PDFs** escaneados o imágenes

### **🧪 Testing Incremental:**
- 🔧 **Día 1-3:** Setup básico funcionando
- 🔍 **Día 4-7:** Búsqueda semántica operativa  
- 🤖 **Día 8-11:** RAG completo con LLM
- ✨ **Día 12-15:** Pulir y optimizar

### **💰 Control de Costos:**
- 📊 **Monitorea uso** de APIs diariamente
- 🎯 **Usa modelos baratos** para testing (gpt-4o-mini, claude-haiku)
- 🔄 **Aprovecha planes gratuitos** (Gemini, n8n, Airtable)

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Comprensión sólida de RAG**  
✅ **Bot inteligente que responde con contexto**  
✅ **Experiencia práctica con embeddings y LLMs**  
✅ **Pipeline RAG completo en la nube**  
✅ **Proyecto demostrable para portfolio**  
✅ **Base para sistemas RAG más complejos**

**¡15 días para dominar la tecnología que está transformando la IA conversacional!** 🚀

---

## 📖 Glosario RAG Simplificado

- **🔍 RAG:** Buscar información relevante + Generar respuesta inteligente
- **📊 Embeddings:** Convertir texto a números que la computadora entiende
- **🔢 Vector:** Lista de números que representa el "significado" del texto
- **📏 Similitud:** Qué tan parecidos son dos textos (matemáticamente)
- **🧠 LLM:** Large Language Model - IA que entiende y genera texto
- **📋 Chunk:** Pedazo pequeño de documento (párrafo o sección)
- **💬 Prompt:** Instrucciones que le das al LLM para generar respuestas
