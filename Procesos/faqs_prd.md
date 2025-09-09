# 🤖 PRD: Chatbot FAQs con Telegram + n8n (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**  
Un bot de Telegram que responde FAQs automáticamente usando n8n como backend.

**Stack Simple:**
- 📱 **Telegram** - Canal de comunicación  
- ⚡ **n8n** - Motor de automatización  
- 📊 **Google Sheets** - Base de datos (principal)  
- 🗃️ **Airtable** - Base de datos (opcional/alternativa)

**Resultado Final:**  
Bot funcional que responde preguntas frecuentes en Telegram con búsqueda inteligente.

---

## 🎯 Plan de 15 Días Simplificado

### **SEMANA 1: CORE (Días 1-7)**

#### **Día 1: Setup Telegram Bot** 🤖
- [ ] Crear bot con @BotFather en Telegram
- [ ] Obtener API Token del bot
- [ ] Configurar webhook en n8n para recibir mensajes
- [ ] Probar envío/recepción básica

#### **Día 2: Base de Datos** 📊
- [ ] **Opción A:** Crear Google Sheets con columnas: Pregunta | Respuesta | Keywords
- [ ] **Opción B:** Configurar Airtable con misma estructura
- [ ] Poblar 20 FAQs de ejemplo
- [ ] Conectar n8n con la base elegida

#### **Día 3-4: Búsqueda Básica** 🔍
- [ ] Crear Function node para limpiar texto (minúsculas, acentos)
- [ ] Implementar búsqueda por palabras clave
- [ ] Configurar respuesta cuando encuentra match
- [ ] Respuesta "No entendí" cuando no encuentra nada

#### **Día 5-6: Mejoras de Búsqueda** ⚡
- [ ] Agregar búsqueda por sinónimos básicos
- [ ] Implementar scoring simple (más keywords = mejor match)
- [ ] Respuestas formateadas con emojis
- [ ] Testing con diferentes tipos de preguntas

#### **Día 7: Testing Semana 1** ✅
- [ ] Probar 20 preguntas diferentes
- [ ] Verificar todas las respuestas
- [ ] Ajustar keywords si es necesario
- [ ] Documentar lo que funciona

### **SEMANA 2: FUNCIONALIDADES (Días 8-14)**

#### **Día 8-9: Analytics Simple** 📈
- [ ] Crear hoja separada para logs: Usuario | Pregunta | Respuesta | Fecha
- [ ] Guardar cada consulta automáticamente
- [ ] Contador de consultas por día
- [ ] Comando `/stats` para ver estadísticas

#### **Día 10-11: Administración** ⚙️
- [ ] Comando `/admin` para agregar nueva FAQ
- [ ] Validar que no existan duplicados
- [ ] Comando `/list` para ver todas las FAQs
- [ ] Solo permitir admin a usuarios autorizados

#### **Día 12-13: Features Extra** 🚀
- [ ] Comando `/help` con instrucciones
- [ ] Respuestas con botones inline para opciones
- [ ] Búsqueda por categorías
- [ ] Comando `/categorias` para listar temas

#### **Día 14: Pulir y Optimizar** ✨
- [ ] Mejorar mensajes de respuesta con formato
- [ ] Agregar manejo de errores
- [ ] Testing completo de todos los comandos
- [ ] Optimizar velocidad de respuesta

### **Día 15: Entrega Final** 🎯
- [ ] Testing final completo
- [ ] Documentar comandos disponibles
- [ ] Crear video demo de 3 minutos
- [ ] Preparar presentación del proyecto

---

## 🛠️ Estructura Técnica Simple

### **Base de Datos (Elegir una):**

#### **Opción A: Google Sheets** (Recomendado para principiantes)
```
Hoja "FAQs":
| Pregunta | Respuesta | Keywords | Categoria |
|----------|-----------|----------|-----------|
| ¿Cómo funciona? | Es muy fácil... | funciona,como,ayuda | General |
```

#### **Opción B: Airtable** (Más profesional)
```
Tabla "FAQs":
- Pregunta (Text)
- Respuesta (Long text) 
- Keywords (Tags)
- Categoria (Select)
- Activo (Checkbox)
```

### **Workflows n8n:**

#### **Workflow Principal: "Telegram-FAQ-Bot"**
1. **Telegram Trigger** → Recibe mensajes
2. **Function Node** → Procesa texto
3. **Google Sheets/Airtable** → Busca FAQ
4. **Function Node** → Calcula mejor match
5. **Telegram Node** → Envía respuesta

#### **Workflow Admin: "FAQ-Admin"** (Opcional)
1. **Telegram Trigger** → Comandos admin
2. **Switch Node** → /admin, /list, /stats
3. **Google Sheets/Airtable** → CRUD operations
4. **Telegram Node** → Confirma acción

---

## 📋 Checklist de Funcionalidades

### **Core (Obligatorio):**
- [ ] ✅ Bot responde en Telegram
- [ ] 🔍 Búsqueda funciona con 20+ FAQs
- [ ] 📝 Respuestas formateadas y claras
- [ ] ❌ Maneja consultas no encontradas

### **Intermedio (Deseable):**
- [ ] 📊 Guarda logs de consultas
- [ ] ⚙️ Comando admin para agregar FAQs
- [ ] 📈 Comando /stats básico
- [ ] 🏷️ Búsqueda por categorías

### **Avanzado (Bonus):**
- [ ] 🔘 Botones inline para opciones
- [ ] 👥 Sistema de usuarios admin
- [ ] 📊 Dashboard de analytics
- [ ] 🤖 Respuestas inteligentes contextuales

---

## 🎯 Criterios de Éxito Simple

### **Funcionalidad (60%):**
- Bot responde correctamente 15/20 preguntas de prueba
- Tiempo de respuesta < 5 segundos
- No se rompe con mensajes extraños

### **Código (25%):**
- Workflows n8n organizados y comentados
- Function nodes con código limpio
- Manejo básico de errores

### **Documentación (15%):**
- README con instrucciones de uso
- Lista de comandos disponibles
- Video demo funcionando

---

## 💡 Tips para Éxito Garantizado

### **Setup Rápido:**
1. 🚀 **Empieza con Google Sheets** - es más fácil que Airtable
2. 📱 **Usa tu Telegram personal** para testing
3. ⚡ **Una FAQ por día** mínimo para no quedarte sin contenido

### **Desarrollo:**
- 🧪 **Prueba cada nodo** antes de conectar el siguiente
- 📝 **Usa console.log** en Function nodes para debug
- 🔄 **Guarda progreso diario** por si algo se rompe

### **Contenido:**
- ❓ **FAQs reales** funcionan mejor que inventadas
- 🏷️ **Keywords específicas** mejoran la búsqueda
- 😊 **Agrega emojis** para respuestas más amigables

---

## 📞 ¿Necesitas Ayuda?

### **Recursos Útiles:**
- 📖 [Documentación n8n](https://docs.n8n.io)
- 🤖 [Telegram Bot API](https://core.telegram.org/bots/api)
- 📊 [Google Sheets API en n8n](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/)

### **Problemas Comunes:**
- **Bot no responde:** Verificar webhook URL
- **No encuentra FAQs:** Revisar keywords en la base
- **Error de permisos:** Verificar credenciales de Google/Airtable

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Un chatbot funcional en Telegram**  
✅ **Sistema de FAQs automatizado**  
✅ **Experiencia práctica con n8n**  
✅ **Proyecto demostrable para portfolio**  
✅ **Conocimiento de integraciones reales**

**¡15 días para demostrar que puedes automatizar procesos reales!** 🚀
