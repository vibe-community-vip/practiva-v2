# Agente de IA para Telegram
Este es un flujo de trabajo de n8n diseñado para un agente de IA que recibe información a través de Telegram y distribuye las tareas entre tres sub-agentes especializados.

## Estructura del Agente
El agente principal actúa como un orquestador, dirigiendo las solicitudes de los usuarios a los sub-agentes adecuados en función de la función requerida.

1. **Agente de Agendamiento**

    **Función**: Gestiona todo lo relacionado con reuniones y contactos.
    **Herramientas (Tools)**:


        - Agendar reunión Cal.com: Crea nuevas reuniones en Cal.com.
        - Cancelar reunión Cal.com: Elimina reuniones existentes.
        - Reprogramar Cal.com: Modifica la fecha y hora de reuniones.
        - Consultar disponibilidad Cal.com: Verifica los horarios disponibles para agendar.
        - Llenar base de contactos: Registra nuevos contactos en una base de datos.

2. **Agente de Generación de Contenido**

    **Función**: Crea y adapta contenido multimedia.   
    **Herramientas (Tools):**

        - Edición de imágenes: Utiliza modelos como nano banana para modificar imágenes.

        - Generación de imágenes: Crea imágenes nuevas a partir de descripciones.

        - Combinación de imágenes: Fusiona varias imágenes en una sola.

        - Generación de videos: Crea contenido de video.

        - Adaptación de publicación: Prepara contenido para plataformas como LinkedIn, Instagram y Facebook.

3. **Agente de Optimización de Procesos**
    **Función**: Mejora la eficiencia y organización de las tareas diarias.
    **Herramientas (Tools):**

        - Implementación de base de conocimiento (FAQs): Responde preguntas frecuentes.

        - Implementación de base de conocimiento (RAG): Utiliza un modelo de generación aumentada de recuperación para dar respuestas más precisas.

        - Investigar proveedor RAG: Busca el proveedor más adecuado para la implementación.

        - Leer imagen/PDF (OCR): Extrae texto de imágenes y documentos para el registro de gastos y facturas.

        - Creación de base de datos de gastos: Registra y organiza la información de gastos.

        - Registro de tareas pendientes: Mantiene un listado de tareas por completar.