# Rol y Objetivo Principal

Eres un Ingeniero Principal de IA y Arquitecto de Google Cloud experto. Tu objetivo es estructurar la base (scaffold) de un Agente de IA Serverless desde cero, altamente flexible y listo para producción.

La base de código debe estar escrita en Python, utilizando el framework `adk.dev` 2.0 (Agent Development Kit), y estar estrictamente optimizada para su despliegue en Google Cloud Run.

---

## Especificaciones Técnicas y Requisitos

### 1. Integración con GCP Agent Platform (Vertex AI)

* El LLM central del agente debe estar impulsado por **Google Cloud's Agent Platform (Vertex AI)**.
* Inicializa el agente ADK utilizando el proveedor de modelos nativo de Vertex AI (por ejemplo, `gemini-3.1-flash-lite` o el endpoint de Vertex adecuado).
* Asegúrate de que el código asuma la autenticación estándar de Google Cloud (Application Default Credentials) para que se autentique sin problemas al desplegarse en Cloud Run.

### 2. Integración Dinámica de MCP

* El agente debe ser capaz de comunicarse con *cualquier* servidor MCP (Model Context Protocol) externo.
* No dejes herramientas escritas en duro (hardcoded). En su lugar, el agente debe cargar dinámicamente las configuraciones del servidor MCP (URLs, autenticación o puntos de entrada locales) desde un archivo `mcp_config.json`.

### 3. Prompt de Sistema Configurable

* El prompt/instrucciones del sistema central del agente debe estar completamente desacoplado del código.
* La aplicación debe intentar cargar el prompt del sistema desde una variable de entorno (por ejemplo, `AGENT_SYSTEM_PROMPT`).
* Si la variable de entorno no está configurada, debe recurrir a leerlo desde un archivo `config.json`.

### 4. Estándares de Python y ADK 2.0

* La base de código debe estar escrita en Python moderno (3.11+).
* Utiliza estrictamente la especificación `adk.dev` versión 2.0 para la inicialización del agente, la gestión de memoria y el enlace de herramientas (tool binding).
* **Documentación:** Cada función, clase y módulo debe cumplir estrictamente con los **Google Style Python Docstrings**.

### 5. Gestión de Paquetes (`uv`)

* Utiliza `uv` exclusivamente para la gestión de paquetes y el aislamiento del entorno.
* Genera el archivo `pyproject.toml` necesario que incluya las dependencias: `adk`, `mcp`, `fastapi` (o equivalente para la capa web) y un servidor ASGI de producción como `uvicorn`.
* Proporciona los comandos exactos de la CLI de `uv` en la salida para inicializar el proyecto y sincronizar las dependencias.

### 6. Optimización para Google Cloud Run

* Genera un `Dockerfile` optimizado específicamente para Google Cloud Run:
  * Utiliza una imagen base de Python slim o distroless.
  * Asegúrate de que la aplicación se vincule a `0.0.0.0` y escuche en el puerto definido por la variable de entorno `PORT` (por defecto 8080).
  * Implementa las mejores prácticas: ejecutar como usuario no raíz (non-root), minimizar las capas y evitar la instalación de herramientas de compilación innecesarias en la imagen final.
  * Incluye un archivo `.dockerignore`.

---

## Reglas de Generación de la Salida

1. Primero, muestra una representación limpia en árbol ASCII de la estructura del proyecto.
2. Proporciona el código completo para cada archivo, asegurándote de que sea autocontenido y esté listo para ejecutar.
3. Incluye un bloque `README.md` conciso con los comandos de terminal exactos necesarios para inicializar el proyecto localmente usando `uv` y desplegarlo usando `gcloud run deploy`.