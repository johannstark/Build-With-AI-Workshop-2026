# Role and Core Objective

Actúa como un Principal AI Engineer y experto en Google Cloud. En nuestro workspace actual tenemos una carpeta local llamada `./politicas` que contiene 3 archivos Markdown con documentación oficial de la compañía (políticas internas, beneficios, etc.).

Tu objetivo es analizar estos archivos y diseñar la mejor estrategia para exponer esta información a un Agente de IA mediante un Servidor MCP (Model Context Protocol). El sistema debe ser robusto, seguro y estar listo para desplegarse en producción usando una arquitectura Serverless.

---

# Fases de Ejecución

## Fase 1: Análisis y Estrategia de Herramientas (Tools)

1. Lee y analiza el contenido de los 3 archivos `.md` ubicados en `./politicas`.
2. Basado en la estructura, longitud y tipo de datos de esos documentos, diseña la mejor estrategia de herramientas MCP (`@mcp.tool()`). Por ejemplo: decide si es más eficiente crear una herramienta de búsqueda por palabras clave, una que extraiga secciones específicas mediante expresiones regulares, o una que devuelva el contenido íntegro.
3. Implementa validaciones de seguridad estrictas en las herramientas diseñadas para prevenir vulnerabilidades de *path traversal* o inyecciones al leer los archivos.

## Fase 2: Implementación del Servidor (`server.py`)

Implementa el servidor en Python utilizando la librería oficial (preferiblemente la abstracción `FastMCP`).

* **Transporte Híbrido:** El servidor debe ser capaz de operar en dos entornos sin cambiar el código:

  * **Modo Local:** Por defecto, debe inicializarse usando `Stdio` para permitir la integración y pruebas en el entorno de desarrollo local.
  * **Modo Nube (Cloud Run):** Si el código detecta la variable de entorno `PORT` (inyectada automáticamente por GCP), debe cambiar dinámicamente a **SSE (Server-Sent Events)**, exponiendo el servicio en la IP `0.0.0.0` y el puerto correspondiente.

## Fase 3: Infraestructura como Código y Estándares

* **Gestión de Dependencias:** Utiliza `uv`. Genera el archivo `pyproject.toml` con las dependencias exactas (`mcp`, servidores ASGI si aplica, etc.).
* **Calidad de Código:** Obligatorio el uso de docstrings bajo el estándar de Google para todas las funciones y clases.
* **Contenedor:** Genera un `Dockerfile` multi-stage optimizado para Google Cloud Run (imagen base Python slim, usuario non-root, minimización de capas).

---

# Output Esperado

1. **Estrategia:** Un breve párrafo explicando por qué elegiste el set de herramientas (`tools`) basándote en lo que leíste de los Markdowns.
2. **Código:** El código completo y listo para ejecutarse de `server.py`, `pyproject.toml` y el `Dockerfile`.
3. **README:** Instrucciones precisas con:
   * El comando exacto para levantar y probar el servidor usando `npx @modelcontextprotocol/inspector`.
   * El comando de despliegue usando `gcloud run deploy`.