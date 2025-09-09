# ✅ PRD: Task Manager con Telegram + n8n (15 días)

## 📋 Resumen del Proyecto

**¿Qué vas a construir?**  
Un sistema completo de gestión de tareas (To-Do List) que permite crear, editar, eliminar y cambiar el estado de tareas a través de Telegram usando comandos naturales.

**Stack de Desarrollo:**
- 📱 **Telegram** - Interface de usuario principal  
- ⚡ **n8n Cloud** - Motor de automatización (plan gratuito)  
- 🗃️ **Base de Datos** (elige una):
  - 🥇 **Airtable** (visual, fácil de usar)
  - 🥈 **Supabase** (PostgreSQL, más potente)
  - 🥉 **Google Sheets** (simple, familiar)
- 🧠 **OpenAI/Gemini** - IA para comandos naturales (opcional)

**Funcionalidades Core:**  
✅ Crear tareas  ✏️ Editar tareas  ❌ Eliminar tareas  🔄 Cambiar estados  📊 Listar tareas

---

## 🎯 ¿Por qué un Task Manager vía Telegram?

### **Ventajas del Sistema:**
- 🚀 **Acceso instantáneo** desde cualquier dispositivo
- 💬 **Interface familiar** (todos saben usar Telegram)
- 🤖 **Comandos intuitivos** (/nueva, /listar, /completar)
- 📱 **Sin apps adicionales** que instalar
- ☁️ **Sincronizado en la nube** automáticamente

### **Casos de Uso:**
- **Personal:** Lista de pendientes diaria
- **Equipos:** Tareas colaborativas simples
- **Proyectos:** Seguimiento de hitos
- **Estudiantes:** Asignaciones y entregas

---

## 🎯 Plan de 15 Días Estructurado

### **SEMANA 1: FUNDAMENTOS CRUD (Días 1-7)**

#### **Día 1: Setup y Arquitectura** 🏗️
- [ ] Crear bot con @BotFather en Telegram
- [ ] Configurar n8n Cloud (plan gratuito)
- [ ] **Elegir y configurar base de datos:**
  
  **Opción A: Airtable (Recomendado para principiantes)**
  - Interfaz visual amigable
  - Templates predefinidos
  - API simple de usar
  
  **Opción B: Supabase (Para usuarios técnicos)**
  - PostgreSQL completo
  - Real-time capabilities
  - API REST automática
  
  **Opción C: Google Sheets (Más simple)**
  - Familiar para todos
  - Sin configuración compleja
  - Limitado pero funcional

#### **Día 2: Estructura de Base de Datos** 📊
- [ ] Diseñar esquema de tareas
- [ ] Crear tablas/hojas necesarias
- [ ] Configurar relaciones entre datos
- [ ] Poblar datos de prueba

#### **Día 3-4: Funcionalidad CREATE (Crear)** ➕
- [ ] Workflow: Crear nueva tarea
- [ ] Comando `/nueva [descripción]`
- [ ] Validaciones básicas
- [ ] Respuesta de confirmación

#### **Día 5: Funcionalidad READ (Listar)** 📖
- [ ] Workflow: Listar tareas
- [ ] Comando `/listar` - todas las tareas
- [ ] Comando `/pendientes` - solo no completadas
- [ ] Formato de respuesta clara

#### **Día 6-7: Funcionalidades UPDATE/DELETE** ✏️❌
- [ ] Workflow: Editar tarea existente
- [ ] Workflow: Eliminar tarea
- [ ] Comandos `/editar [id]` y `/eliminar [id]`
- [ ] Confirmaciones de seguridad

### **SEMANA 2: FUNCIONALIDADES AVANZADAS (Días 8-14)**

#### **Día 8-9: Estados y Prioridades** 🔄
- [ ] Sistema de estados (Pendiente, En Progreso, Completado)
- [ ] Niveles de prioridad (Baja, Media, Alta, Urgente)
- [ ] Comandos `/completar [id]` y `/prioridad [id] [nivel]`
- [ ] Filtros por estado y prioridad

#### **Día 10-11: Fechas y Recordatorios** 📅
- [ ] Fechas de vencimiento
- [ ] Recordatorios automáticos
- [ ] Comando `/vence [id] [fecha]`
- [ ] Notificaciones diarias de tareas vencidas

#### **Día 12-13: Interface Mejorada** 🎨
- [ ] Botones inline para acciones rápidas
- [ ] Menú principal con opciones
- [ ] Formato de mensajes mejorado con emojis
- [ ] Comandos de ayuda contextuales

#### **Día 14: Analytics y Reportes** 📊
- [ ] Dashboard de productividad
- [ ] Estadísticas de completado
- [ ] Comando `/stats` con métricas
- [ ] Exportar tareas completadas

### **Día 15: Entrega Final** 🎯
- [ ] Testing exhaustivo de todos los comandos
- [ ] Optimización de performance
- [ ] Documentación completa
- [ ] Video demo de funcionalidades

---

## 🗃️ Estructura de Base de Datos Detallada

### **Opción A: Esquema Airtable**

#### **Tabla Principal: `tasks`**
```
┌────────────────────────────────────────────────────────────────────────┐
│ Field Name    │ Type        │ Options                                │
├────────────────────────────────────────────────────────────────────────┤
│ id            │ Auto Number │ Primary Key                            │
│ title         │ Single Text │ Required, Max 100 chars               │
│ description   │ Long Text   │ Optional details                       │
│ status        │ Select      │ Pendiente, En Progreso, Completado    │
│ priority      │ Select      │ Baja, Media, Alta, Urgente             │
│ due_date      │ Date        │ Optional deadline                      │
│ created_at    │ Created     │ Auto timestamp                         │
│ updated_at    │ Modified    │ Auto timestamp                         │
│ created_by    │ Single Text │ Telegram User ID                       │
│ tags          │ Tags        │ Categorización (trabajo, personal)    │
│ completed_at  │ Date        │ When task was marked complete          │
│ notes         │ Long Text   │ Additional notes/comments              │
└────────────────────────────────────────────────────────────────────────┘
```

#### **Tabla Auxiliar: `users`**
```
┌────────────────────────────────────────────────────────────────┐
│ Field Name     │ Type        │ Options                        │
├────────────────────────────────────────────────────────────────┤
│ telegram_id    │ Number      │ Primary Key                    │
│ username       │ Single Text │ @username                      │
│ first_name     │ Single Text │ User's first name              │
│ created_at     │ Created     │ Registration date              │
│ is_active      │ Checkbox    │ User status                    │
│ timezone       │ Select      │ User timezone                  │
│ task_count     │ Rollup      │ Count of tasks                 │
└────────────────────────────────────────────────────────────────┘
```

### **Opción B: Esquema Supabase (SQL)**

```sql
-- Tabla de usuarios
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  telegram_id BIGINT UNIQUE NOT NULL,
  username TEXT,
  first_name TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  is_active BOOLEAN DEFAULT true,
  timezone TEXT DEFAULT 'UTC'
);

-- Tabla de tareas
CREATE TABLE tasks (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL CHECK (length(title) > 0),
  description TEXT,
  status TEXT DEFAULT 'pendiente' CHECK (status IN ('pendiente', 'en_progreso', 'completado')),
  priority TEXT DEFAULT 'media' CHECK (priority IN ('baja', 'media', 'alta', 'urgente')),
  due_date DATE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  completed_at TIMESTAMP WITH TIME ZONE,
  created_by INTEGER REFERENCES users(id) ON DELETE CASCADE,
  tags TEXT[],
  notes TEXT
);

-- Índices para performance
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_created_by ON tasks(created_by);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);

-- Row Level Security (RLS)
ALTER TABLE tasks ENABLE ROW LEVEL SECURITY;
ALTER TABLE users ENABLE ROW LEVEL SECURITY;

-- Políticas de seguridad
CREATE POLICY "Users can only see their own tasks" ON tasks
  FOR ALL USING (created_by = (
    SELECT id FROM users WHERE telegram_id = current_setting('request.jwt.claims', true)::json->>'telegram_id'
  ));
```

### **Opción C: Esquema Google Sheets**

```
Hoja "Tasks":
A: ID (auto-incremental)
B: Título
C: Descripción  
D: Estado (Pendiente/En Progreso/Completado)
E: Prioridad (Baja/Media/Alta/Urgente)
F: Fecha Vencimiento
G: Fecha Creación
H: Fecha Actualización
I: Usuario (Telegram ID)
J: Tags
K: Notas

Hoja "Users":
A: Telegram ID
B: Username
C: Nombre
D: Fecha Registro
E: Estado Activo
```

---

## 🛠️ Arquitectura de Workflows n8n

### **Workflow 1: Dispatcher Principal**
```
📱 Telegram Trigger (recibe todos los mensajes)
    ↓
🔧 Function: Parsear comando y parámetros
    ↓
🔀 Switch: Rutear según comando
    ├── /nueva → Workflow Crear Tarea
    ├── /listar → Workflow Listar Tareas  
    ├── /editar → Workflow Editar Tarea
    ├── /eliminar → Workflow Eliminar Tarea
    ├── /completar → Workflow Cambiar Estado
    └── otros → Workflow Ayuda
```

### **Workflow 2: Crear Tarea**
```
⚡ Webhook/Execute Workflow (desde dispatcher)
    ↓
🔧 Function: Validar datos de entrada
    ↓
🗃️ Database Insert: Crear nueva tarea
    ↓
📱 Telegram: Confirmar creación con detalles
    ↓
📝 Log: Registrar acción
```

### **Workflow 3: Listar Tareas**
```
⚡ Webhook/Execute Workflow (desde dispatcher)
    ↓
🗃️ Database Query: Buscar tareas del usuario
    ↓
🔧 Function: Formatear lista de tareas
    ↓
📱 Telegram: Enviar lista formateada
    ↓
🔘 Inline Buttons: Acciones rápidas (completar, editar)
```

### **Workflow 4: CRUD Operations**
```
⚡ Webhook/Execute Workflow (recibe ID + action)
    ↓
🔧 Function: Validar permisos de usuario
    ↓
🗃️ Database Operation: UPDATE/DELETE según acción
    ↓
📱 Telegram: Confirmar operación exitosa
    ↓
🔔 Notification: Actualizar otros usuarios si colaborativo
```

---

## 📋 Lista de Comandos Completa

### **Comandos Básicos:**
```
/start - Bienvenida e instrucciones
/help - Lista de comandos disponibles
/nueva [título] - Crear nueva tarea
/listar - Ver todas las tareas
/pendientes - Ver solo tareas pendientes
/completadas - Ver tareas completadas
```

### **Comandos de Gestión:**
```
/editar [id] [nuevo_título] - Editar título de tarea
/eliminar [id] - Eliminar tarea (con confirmación)
/completar [id] - Marcar tarea como completada
/reabrir [id] - Reabrir tarea completada
/prioridad [id] [baja/media/alta/urgente] - Cambiar prioridad
/vence [id] [YYYY-MM-DD] - Establecer fecha límite
```

### **Comandos Avanzados:**
```
/buscar [término] - Buscar en títulos y descripciones
/tag [id] [etiqueta] - Agregar etiqueta
/stats - Estadísticas de productividad
/export - Exportar tareas a CSV
/recordatorio [id] [días] - Configurar recordatorio
/urgentes - Ver tareas urgentes y vencidas
```

### **Comandos de Configuración:**
```
/timezone [zona] - Configurar zona horaria
/config - Ver configuración actual
/reset - Reiniciar configuración (confirmación requerida)
```

---

## 🎯 Criterios de Éxito

### **Funcionalidad CRUD (60%):**
- [ ] ✅ Crear tareas con título y descripción
- [ ] 📖 Listar tareas con formato claro
- [ ] ✏️ Editar tareas existentes
- [ ] ❌ Eliminar tareas con confirmación
- [ ] 🔄 Cambiar estados (pendiente→progreso→completado)

### **Usabilidad (25%):**
- [ ] 💬 Comandos intuitivos y fáciles de recordar
- [ ] 🚀 Respuesta rápida (< 3 segundos)
- [ ] 📱 Formato mobile-friendly en Telegram
- [ ] 🔘 Botones inline para acciones comunes
- [ ] ❓ Sistema de ayuda contextual

### **Robustez (15%):**
- [ ] 🛡️ Validación de datos de entrada
- [ ] 🔒 Seguridad (usuarios solo ven sus tareas)
- [ ] 📊 Manejo de errores graceful
- [ ] 💾 Persistencia de datos confiable
- [ ] 🔄 Recovery automático de fallos

---

## 💡 Ejemplos de Interacciones

### **Flujo Básico de Uso:**
```
Usuario: /nueva Comprar leche para el desayuno
Bot: ✅ Tarea creada exitosamente!
     📝 ID: 15
     📋 Título: Comprar leche para el desayuno
     🔄 Estado: Pendiente
     ⭐ Prioridad: Media
     📅 Creada: 15/09/2025 14:30

Usuario: /listar
Bot: 📋 **Tus tareas pendientes:**
     
     1️⃣ ID: 12 | ⭐ Alta
     📝 Preparar presentación cliente
     📅 Vence: 16/09/2025
     
     2️⃣ ID: 15 | ⭐ Media  
     📝 Comprar leche para el desayuno
     📅 Sin fecha límite
     
     📊 Total: 2 pendientes, 5 completadas

Usuario: /completar 15
Bot: ✅ ¡Tarea completada!
     📝 "Comprar leche para el desayuno"
     ⏰ Completada: 15/09/2025 18:45
     
     🎉 ¡Bien hecho! Llevas 6 tareas completadas esta semana.
```

### **Flujo Avanzado con Prioridades:**
```
Usuario: /nueva Entregar proyecto final para universidad
Bot: ✅ Tarea creada (ID: 16)

Usuario: /prioridad 16 urgente
Bot: 🚨 Prioridad actualizada a URGENTE
     📝 "Entregar proyecto final para universidad"

Usuario: /vence 16 2025-09-20
Bot: ⏰ Fecha límite establecida: 20/09/2025
     🔔 Te recordaré 1 día antes

Usuario: /urgentes
Bot: 🚨 **Tareas urgentes y vencidas:**
     
     ⚠️ VENCE HOY
     📝 ID: 16 | Entregar proyecto final
     📅 Vence: 20/09/2025
     
     ⏰ Recordatorio: ¡Solo quedan 5 días!
```

---

## 🔗 Referencias y Recursos

### **Templates de n8n Existentes:**
- [Task Management with Todoist](https://n8n.io/workflows/3052-effortless-task-management-create-todoist-tasks-directly-from-telegram-with-ai/) - Template para crear tareas en Todoist desde Telegram con IA
- [Telegram Task Manager](https://n8n.io/workflows/3656-ai-powered-telegram-task-manager-with-mcp-server/) - Bot de tareas con Google Tasks y IA
- [Google Sheets Task Management](https://n8n.io/workflows/5291-manage-tasks-and-send-scheduled-reminders-with-telegram-bot-google-sheets-and-gpt-4o-mini/) - Sistema completo con recordatorios

### **Documentación de APIs:**
- [Airtable API](https://airtable.com/developers/web/api/introduction) - Documentación completa de Airtable API
- [Supabase Database Guide](https://supabase.com/docs/guides/database/tables) - Guía para crear tablas y APIs
- [Google Sheets API](https://developers.google.com/sheets/api/guides/concepts) - Conceptos y operaciones básicas
- [n8n Telegram Node](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/) - Documentación completa del nodo Telegram

### **Ejemplos de Estructuras:**
- [Building CRUD Todo with Supabase](https://medium.com/@samwit/building-a-crud-to-do-list-with-flask-and-supabase-2ee9f5ba7e8d) - Tutorial completo de Todo CRUD con Supabase
- [Airtable Employee Management](https://n8n.io/workflows/4545-ai-powered-employee-database-management-via-telegram-using-openai-and-airtable/) - Gestión de base de datos con IA via Telegram

### **Tools & Integraciones:**
- [n8n Airtable Integration](https://n8n.io/integrations/airtable/) - Documentación oficial de integración
- [Telegram Bot API](https://core.telegram.org/bots/api) - API oficial de Telegram para bots
- [Supabase REST API](https://supabase.com/docs/guides/api) - Auto-generated REST API documentation

---

## 🚀 Tips para Implementación Exitosa

### **🎯 Empezar Simple:**
1. **Día 1-3:** Solo comandos básicos (/nueva, /listar)
2. **Día 4-7:** Agregar edición y eliminación
3. **Día 8-15:** Funcionalidades avanzadas

### **🗃️ Elección de Base de Datos:**
- **Airtable:** Mejor para principiantes, interfaz visual
- **Supabase:** Mejor para desarrolladores, más potente
- **Google Sheets:** Mejor para simplicidad extrema

### **💻 Mejores Prácticas de Desarrollo:**
- ✅ **Validar todos los inputs** del usuario
- ✅ **Usar IDs únicos** para identificar tareas
- ✅ **Implementar confirmaciones** para acciones destructivas
- ✅ **Formatear respuestas** de manera consistente
- ✅ **Manejar errores** con mensajes útiles

### **📱 UX en Telegram:**
- 🎨 **Usar emojis** para mejor legibilidad
- 🔘 **Botones inline** para acciones frecuentes
- 📝 **Mensajes concisos** (límite de caracteres)
- 🔄 **Estados de carga** para operaciones lentas

---

## 🏆 ¡Al Finalizar Tendrás!

✅ **Sistema completo de gestión de tareas**  
✅ **Interface intuitiva vía Telegram**  
✅ **Base de datos estructurada y escalable**  
✅ **Operaciones CRUD funcionales**  
✅ **Sistema de estados y prioridades**  
✅ **Recordatorios y notificaciones automáticas**  
✅ **Experiencia con APIs y automatización**  
✅ **Proyecto demostrable para portfolio**

**¡15 días para crear tu propio asistente personal de productividad!** 🚀

---

## 📖 Glosario de Términos

- **🔄 CRUD:** Create, Read, Update, Delete - operaciones básicas de base de datos
- **📱 Bot de Telegram:** Aplicación automatizada que interactúa via mensajes
- **🗃️ Base de Datos:** Sistema para almacenar y organizar información
- **⚡ Workflow:** Secuencia automatizada de pasos en n8n
- **🎯 Estado:** Condición actual de una tarea (pendiente, en progreso, completado)
- **⭐ Prioridad:** Nivel de importancia de una tarea
- **📅 Due Date:** Fecha límite para completar una tarea
- **🔘 Inline Buttons:** Botones que aparecen debajo de mensajes en Telegram
- **🔒 RLS:** Row Level Security - seguridad a nivel de registro en base de datos
