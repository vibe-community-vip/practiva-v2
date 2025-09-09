# 📸 PRD: OCR Expense Tracker con Telegram + n8n (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**  
Un sistema automatizado que extrae datos de facturas y recibos mediante OCR (Optical Character Recognition) y los registra automáticamente en una base de gastos empresariales.

**Stack en la Nube:**
- 📱 **Telegram** - Canal para enviar fotos de recibos/facturas  
- ⚡ **n8n Cloud** - Motor de automatización (plan gratuito)  
- 🔍 **Google Vision OCR** - Extracción de texto de imágenes  
- 📊 **Airtable/Google Sheets** - Base de datos de gastos  
- 🧠 **OpenAI/Gemini** - IA para estructurar datos extraídos

**Diferencia vs Entrada Manual:**  
En lugar de escribir manualmente cada gasto, simplemente fotografía el recibo y el sistema extrae automáticamente: fecha, monto, proveedor, categoría, etc.

---

## 🎯 ¿Qué es OCR para Gastos? (Explicación Simple)

### **Problema Actual:**
Registrar gastos empresariales es tedioso:
1. 📝 Escribir manualmente cada recibo
2. 🧮 Calcular totales y categorizar
3. 📊 Transferir a hojas de cálculo
4. 🗂️ Archivar recibos físicos

### **Solución OCR Inteligente:**
1. 📸 **Fotografía el recibo** con tu teléfono
2. 🔍 **OCR extrae texto** automáticamente
3. 🧠 **IA estructura datos** (fecha, monto, proveedor)
4. 📊 **Guarda en base de datos** automáticamente

### **Ejemplo Práctico:**
- **Input:** Foto de recibo de restaurante
- **OCR extrae:** "RESTAURANT BELLA VISTA 15/09/2025 $45.50 TARJETA"
- **IA estructura:** 
  ```json
  {
    "fecha": "2025-09-15",
    "proveedor": "Restaurant Bella Vista",
    "monto": 45.50,
    "categoria": "Alimentación",
    "metodo_pago": "Tarjeta"
  }
  ```
- **Resultado:** Registro automático en base de gastos

---

## 🎯 Plan de 15 Días Simplificado

### **SEMANA 1: FUNDAMENTOS OCR (Días 1-7)**

#### **Día 1: Setup Básico** 🔧
- [ ] Crear bot con @BotFather en Telegram
- [ ] Configurar cuenta n8n Cloud (plan gratuito)
- [ ] **Elegir API OCR:**
  - 🥇 **Google Vision** (300 páginas gratis/mes)
  - 🥈 **OCR.space** (25,000 requests gratis/mes)
  - 🥉 **Tesseract.js** (completamente gratis, local)
- [ ] Setup webhook Telegram en n8n

#### **Día 2: Base de Datos** 📊
**Opción A: Airtable (Recomendado - Más Visual)**
- [ ] Crear base "Expense_Tracker" con tablas:
  - `Expenses` - Gastos principales
  - `Categories` - Categorías predefinidas
  - `Providers` - Proveedores frecuentes
  - `Receipt_Images` - Almacén de imágenes

**Opción B: Google Sheets (Más Simple)**
- [ ] Crear hoja "Gastos_2025" con columnas:
  - Fecha, Proveedor, Monto, Categoría, Descripción, Método_Pago, Estado, Imagen_URL

#### **Día 3-4: OCR Básico** 🔍
- [ ] Configurar credenciales de API OCR elegida
- [ ] Crear workflow "OCR-Extractor":
  - Telegram Trigger (recibe imagen)
  - OCR Node (extrae texto)
  - Function Node (procesa texto crudo)
- [ ] **Testing:** Enviar foto de recibo simple
- [ ] **Objetivo:** Extraer texto básico legible

#### **Día 5-6: Estructuración con IA** 🧠
- [ ] Configurar API de IA (OpenAI/Gemini)
- [ ] Crear prompt para estructurar datos de gastos:
```
Extrae los siguientes datos del texto de un recibo/factura:
- fecha (formato YYYY-MM-DD)
- proveedor (nombre del negocio)
- monto (solo número, sin símbolo moneda)
- categoria (alimentación, transporte, oficina, etc.)
- descripcion (breve resumen del gasto)
- metodo_pago (efectivo, tarjeta, transferencia)

Texto del recibo:
{texto_ocr}

Responde solo en formato JSON válido.
```
- [ ] Testing con diferentes tipos de recibos

#### **Día 7: Integración Completa** ⚡
- [ ] Conectar flujo completo: Telegram → OCR → IA → Base de Datos
- [ ] Agregar validaciones básicas (monto > 0, fecha válida)
- [ ] Respuesta confirmatoria en Telegram
- [ ] **Objetivo:** Procesar 1 recibo de principio a fin

### **SEMANA 2: FUNCIONALIDADES AVANZADAS (Días 8-14)**

#### **Día 8-9: Mejora de Precisión** 📈
- [ ] **Pre-procesamiento de imágenes:**
  - Ajuste de contraste/brillo
  - Rotación automática
  - Recorte inteligente
- [ ] **Post-procesamiento de texto:**
  - Corrección de caracteres comunes (0→O, 1→I)
  - Detección de monedas y formatos de fecha
  - Validación de montos con regex

#### **Día 10-11: Categorización Inteligente** 🏷️
- [ ] **Sistema de categorías:**
  - Alimentación (restaurante, supermercado)
  - Transporte (uber, gasolina, estacionamiento)
  - Oficina (papelería, software, servicios)
  - Viajes (hotel, boletos, comidas)
  - Otros (especificar)
- [ ] **Auto-categorización basada en:**
  - Nombre del proveedor
  - Palabras clave en descripción
  - Rangos de montos típicos

#### **Día 12-13: Features de Usuario** 👥
- [ ] **Comandos de Telegram:**
  - `/gastos_hoy` - Resumen del día
  - `/gastos_mes` - Total del mes actual
  - `/categorias` - Gastos por categoría
  - `/ultimo` - Editar último gasto registrado
  - `/help` - Ayuda y ejemplos
- [ ] **Manejo de errores:**
  - Imagen borrosa o ilegible
  - Datos incompletos
  - Duplicados potenciales

#### **Día 14: Dashboard y Reportes** 📊
- [ ] **Vista de Dashboard en Airtable/Sheets:**
  - Gráfico de gastos por categoría
  - Tendencia mensual
  - Top 10 proveedores
  - Gastos pendientes de validar
- [ ] **Automatización de reportes:**
  - Resumen semanal automático
  - Alertas de presupuesto
  - Backup de datos mensual

### **Día 15: Entrega Final** 🎯
- [ ] Testing exhaustivo con 20+ recibos diferentes
- [ ] Optimización de prompts de IA
- [ ] Documentación completa del sistema
- [ ] Video demo de 5 minutos

---

## 🛠️ Arquitectura Técnica Detallada

### **Workflow Principal n8n:**

```
📱 Telegram Trigger (Recibe imagen)
    ↓
🔧 Function: Validar tipo de archivo
    ↓
🔍 OCR API: Extraer texto de imagen
    ↓ 
🔧 Function: Limpiar y procesar texto
    ↓
🧠 OpenAI/Gemini: Estructurar datos con IA
    ↓
🔧 Function: Validar datos extraídos
    ↓
📊 Airtable/Sheets: Guardar gasto
    ↓
📱 Telegram: Enviar confirmación
    ↓
📁 Google Drive: Guardar imagen original (opcional)
```

### **Estructura de Datos Airtable:**

#### **Tabla: Expenses**
```
┌─────────────────────────────────────────────────────────────────┐
│ ID │ Date │ Provider │ Amount │ Category │ Payment │ Status │ ... │
├─────────────────────────────────────────────────────────────────┤
│ 1  │ 2025-09-15 │ Uber │ 25.50 │ Transport │ Card │ ✅ │     │
│ 2  │ 2025-09-15 │ Starbucks │ 12.00 │ Food │ Cash │ ⏳ │     │
│ 3  │ 2025-09-16 │ Office Max │ 85.30 │ Office │ Card │ ✅ │     │
└─────────────────────────────────────────────────────────────────┘

Campos adicionales:
- Description (texto largo)
- Receipt_Image (attachment)
- OCR_Raw_Text (texto largo)
- Created_By (usuario)
- Notes (texto)
- Tax_Deductible (checkbox)
```

#### **Tabla: Categories**
```
┌──────────────────────────────────────────────┐
│ ID │ Name │ Budget │ Keywords │ Color │
├──────────────────────────────────────────────┤
│ 1  │ Food │ 500.00 │ restaurant,cafe │ 🍽️ │
│ 2  │ Transport │ 200.00 │ uber,taxi,gas │ 🚗 │
│ 3  │ Office │ 300.00 │ supplies,software │ 💼 │
└──────────────────────────────────────────────┘
```

---

## 📋 Checklist de Funcionalidades

### **Core OCR (Obligatorio - 70% del valor):**
- [ ] ✅ Extrae texto legible de recibos/facturas
- [ ] 🧠 Identifica automáticamente: fecha, monto, proveedor
- [ ] 📊 Guarda datos estructurados en base de datos
- [ ] 📱 Envía confirmación al usuario via Telegram

### **Inteligencia de Datos (Deseable - 20% del valor):**
- [ ] 🏷️ Categoriza gastos automáticamente
- [ ] 🔍 Detecta posibles duplicados
- [ ] 💰 Valida rangos de montos razonables
- [ ] 📅 Maneja diferentes formatos de fecha

### **UX y Reportes (Bonus - 10% del valor):**
- [ ] 📊 Dashboard con métricas básicas
- [ ] 💬 Comandos útiles en Telegram
- [ ] 📈 Reportes automáticos periódicos
- [ ] ⚡ Respuesta en menos de 15 segundos

---

## 💰 Estimación de Costos (Muy Económico)

### **APIs OCR - Elige según necesidad:**

#### **🥇 Google Vision API (Recomendado)**
- ✅ **Gratis:** 1,000 requests/mes
- ✅ **Calidad:** Excelente precisión
- ✅ **Costo adicional:** $1.50 por 1,000 requests
- ✅ **Para 500 recibos/mes:** ~$0.75

#### **🥈 OCR.space (Alternativa económica)**
- ✅ **Gratis:** 25,000 requests/mes
- ✅ **Calidad:** Buena para texto simple
- ✅ **Limitación:** 1MB por imagen
- ✅ **Para uso personal:** Completamente gratis

#### **🥉 Tesseract.js (Completamente gratis)**
- ✅ **Gratis:** Ilimitado, corre en n8n
- ❌ **Calidad:** Menor precisión que APIs comerciales
- ✅ **Ideal para:** Aprendizaje y testing

### **Otras Herramientas:**
- 🆓 **n8n Cloud:** 5,000 operaciones/mes gratis
- 🆓 **Airtable:** 1,200 registros gratis
- 🆓 **Google Sheets:** Ilimitado
- 💵 **OpenAI:** ~$2-5/mes para IA estructuración
- 💵 **Gemini:** Plan gratuito disponible

**💡 Total estimado mensual: $0-10 dependiendo del volumen**

---

## 🎯 Criterios de Éxito

### **Precisión OCR (50%):**
- [ ] Extrae correctamente fecha, monto y proveedor en 8/10 recibos
- [ ] Maneja recibos en español e inglés
- [ ] Procesa imágenes de diferentes calidades
- [ ] **Test:** 20 recibos de diferentes tipos de negocios

### **Automatización (30%):**
- [ ] Workflow completo funciona sin intervención manual
- [ ] Categorización automática funcional
- [ ] Datos se guardan correctamente en base de datos
- [ ] **Test:** Procesar 10 recibos seguidos sin errores

### **Usabilidad (20%):**
- [ ] Interface Telegram intuitiva
- [ ] Respuestas claras y útiles
- [ ] Manejo graceful de errores
- [ ] **Test:** Usuario nuevo puede usar sin explicación

---

## 💡 Ejemplos de Prompts para IA

### **Prompt Principal de Estructuración:**
```
Eres un experto contador. Extrae información estructurada de recibos/facturas.

REGLAS IMPORTANTES:
1. Extrae SOLO información que esté claramente visible
2. Para fechas usa formato YYYY-MM-DD
3. Para montos usa solo números (sin símbolos de moneda)
4. Si no encuentras un dato, usa "N/A"

DATOS A EXTRAER:
- fecha: Fecha de la transacción
- proveedor: Nombre del negocio/establecimiento
- monto: Cantidad total a pagar
- categoria: Clasifica en (alimentacion, transporte, oficina, salud, entretenimiento, otros)
- descripcion: Breve resumen de qué se compró
- metodo_pago: efectivo, tarjeta, transferencia o N/A

TEXTO DEL RECIBO:
{ocr_text}

FORMATO DE RESPUESTA (solo JSON válido):
{
  "fecha": "YYYY-MM-DD",
  "proveedor": "Nombre del negocio",
  "monto": 0.00,
  "categoria": "categoria_correspondiente", 
  "descripcion": "breve descripción",
  "metodo_pago": "tipo_de_pago"
}
```

### **Prompt de Categorización Avanzada:**
```
Categoriza este gasto basándote en el proveedor y descripción:

CATEGORÍAS DISPONIBLES:
- alimentacion: restaurantes, supermercados, delivery
- transporte: uber, taxi, gasolina, estacionamiento
- oficina: papelería, software, servicios, internet
- salud: farmacia, médicos, seguros médicos
- entretenimiento: cine, juegos, suscripciones
- viajes: hoteles, boletos, comidas en viaje
- otros: todo lo que no encaje arriba

DATOS DEL GASTO:
Proveedor: {proveedor}
Descripción: {descripcion}
Monto: {monto}

Responde solo con el nombre de la categoría.
```

### **Prompt de Validación:**
```
Valida si estos datos extraídos de un recibo son correctos y razonables:

DATOS:
Fecha: {fecha}
Proveedor: {proveedor}  
Monto: {monto}
Categoría: {categoria}

VALIDACIONES:
1. ¿La fecha es válida y no futura?
2. ¿El proveedor tiene sentido?
3. ¿El monto es razonable para esa categoría?
4. ¿La categoría coincide con el proveedor?

Responde: "VÁLIDO" o "REVISAR: [razón del problema]"
```

---

## 🔗 Referencias y Tutoriales

### **OCR en n8n:**
- [Telegram OCR with Tesseract](https://n8n.io/workflows/5413-extract-text-from-images-with-telegram-bot-and-ocr-tesseractjs/) - Template oficial de n8n para OCR con Telegram
- [Gemini Vision OCR](https://n8n.io/workflows/5864-extract-text-from-images-with-telegram-bot-and-gemini-20-flash-ocr/) - Template usando Google Gemini para OCR
- [n8n OCR Space Integration](https://n8n.io/integrations/ocrspace/) - Documentación para usar OCR.space

### **Automatización de Gastos:**
- [Automated Expense Tracking](https://n8n.io/workflows/5442-automated-expense-tracking-with-ai-receipt-analysis-and-google-sheets/) - Workflow completo de expenses con IA
- [Invoice OCR to Google Sheets](https://n8n.io/workflows/3618-auto-invoice-and-receipt-ocr-to-google-sheets-drive-gmail-and-telegram-triggers/) - Template con múltiples triggers

### **APIs OCR:**
- [Google Vision API Docs](https://cloud.google.com/vision/docs/ocr) - Documentación oficial de Google Vision
- [OCR.space API](https://ocr.space/ocrapi) - API gratuita para OCR básico
- [Tesseract.js GitHub](https://github.com/jreyesr/n8n-nodes-tesseractjs) - Nodo comunidad para OCR local

### **Templates de Gastos:**
- [Airtable Expense Template](https://www.airtable.com/templates/expense-tracking/expAJmFL8SkCqfjnj) - Template oficial de seguimiento de gastos
- [Google Sheets Expense Tracker](https://www.shoeboxed.com/blog/google-sheets-expense-tracker-template) - Templates y guías para Google Sheets

---

## 🚀 Tips para Éxito Garantizado

### **📸 Calidad de Imágenes:**
- ✅ **Buena iluminación** - evita sombras y reflejos
- ✅ **Enfoque nítido** - texto debe ser legible
- ✅ **Ángulo recto** - evita perspectivas distorsionadas
- ✅ **Contraste alto** - texto oscuro sobre fondo claro

### **🔧 Optimización OCR:**
- 🎯 **Testa con recibos reales** de tu día a día
- 🔄 **Itera prompts de IA** basándote en errores comunes
- 📊 **Monitorea precisión** y ajusta según resultados
- 🛠️ **Maneja casos edge** (recibos dañados, texto pequeño)

### **💼 Casos de Uso Específicos:**
- **Freelancers:** Tracking automático de gastos deducibles
- **Pequeñas empresas:** Control de gastos de empleados
- **Contadores:** Digitalización rápida de recibos de clientes
- **Viajeros de negocio:** Registro automático de expenses

### **🎨 Personalización:**
- 🏷️ **Adapta categorías** a tu tipo de negocio
- 💰 **Configura alertas** de presupuesto por categoría
- 📊 **Personaliza reportes** según necesidades
- 🔄 **Automatiza reportes** mensuales para contabilidad

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Sistema automático de registro de gastos**  
✅ **OCR funcional que lee cualquier recibo**  
✅ **IA que estructura datos automáticamente**  
✅ **Base de datos organizada de todos tus gastos**  
✅ **Dashboard para monitorear spending patterns**  
✅ **Proceso 10x más rápido que entrada manual**

**¡15 días para digitalizar completamente tu proceso de gestión de gastos!** 🚀

---

## 📖 Glosario OCR Simplificado

- **📷 OCR:** Optical Character Recognition - tecnología que "lee" texto en imágenes
- **🔍 Text Extraction:** Proceso de convertir imagen a texto legible
- **🧠 Data Structuring:** Organizar texto caótico en campos útiles (fecha, monto, etc.)
- **📊 Expense Tracking:** Seguimiento y categorización de gastos empresariales
- **🏷️ Auto-categorization:** Clasificación automática de gastos por tipo
- **💰 Budget Monitoring:** Control automático de límites de gasto por categoría
- **📈 Expense Analytics:** Análisis de patrones y tendencias de gastos
