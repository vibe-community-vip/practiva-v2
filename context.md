# Contexto del Proyecto

Este proyecto es un flujo de trabajo de **N8N** diseñado para automatizar las interacciones con un agente de inteligencia artificial a través de Telegram. La idea principal es que un solo punto de entrada (el agente principal) pueda derivar y gestionar múltiples tareas complejas, distribuyendo el trabajo a sub-agentes especializados.

## Tecnologías y Componentes Requeridos
El flujo de trabajo se basa en las siguientes tecnologías y herramientas:

    - N8N: Es la plataforma de automatización de código abierto que orquesta todo el flujo de trabajo.
    - Telegram: Sirve como la interfaz principal donde los usuarios interactúan con el agente.
    - Modelos de IA (LLMs): El flujo utiliza modelos de lenguaje grande (LLMs) para procesar las solicitudes de los usuarios. En este caso, se menciona el modelo GPT-4.1 para el agente orquestador, y nano banana o veo3 para las tareas de generación de contenido.
    - Herramientas Específicas (Tools): El flujo integra herramientas de terceros para ejecutar acciones concretas:
        - Cal.com: Para la gestión de reuniones.
        - Modelos de IA Generativa: Para la creación de imágenes y videos.
        - OCR (Reconocimiento Óptico de Caracteres): Para leer y procesar texto de imágenes y documentos.
        - Bases de Datos: Se utilizan para almacenar información como contactos, gastos y tareas.
    - Lógica de Flujo de Trabajo: El flujo de n8n incorpora nodos clave para su funcionamiento:
        - Telegram Trigger: Inicia el flujo al recibir un mensaje.
        - Switch: Dirige la solicitud en función del tipo de mensaje (texto, audio, imagen).
        - Agente Orquestador: El LLM principal que analiza el mensaje del usuario y decide qué sub-agente debe activarse.
        - Nodos de sub-agentes: Cada uno de estos nodos representa un agente con sus propias herramientas y funcionalidades.
        - Nodos de Set y Code: Se utilizan para manipular y estructurar los datos a lo largo del flujo.


## Aplicación del Flujo
El flujo de trabajo n8n aplica un enfoque de **orquestación de agentes**. El agente principal recibe la solicitud del usuario, la procesa y decide qué sub-agente (Agendamiento, Generación de Contenido u Optimización de Procesos) es el más adecuado para manejar la tarea. Esto permite una división eficiente de responsabilidades y la integración de funcionalidades especializadas, creando un sistema robusto y modular.
