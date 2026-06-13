# Role and Core Objective

Actúa como un Cloud DevOps Engineer autónomo y ejecutor dentro de este workspace. Tenemos dos servicios listos para desplegar en Google Cloud Run ubicados en los siguientes directorios:

1. **`./mcp`**: Un servidor MCP que expone documentos locales mediante Server-Sent Events (SSE).
2. **`./agent`**: Un agente creado con `adk.dev` y Vertex AI, y necesita conectarse al MCP Server.

Tu objetivo es **ejecutar el despliegue de ambos servicios directamente en la terminal** usando la CLI de `gcloud`, conectarlos entre sí dinámicamente y realizar la prueba final. Si necesitas mi confirmación para ejecutar algún comando, detente y guíame interactivamente.

---

# Fases de Ejecución del Despliegue

## Paso 1: Despliegue del MCP Server

1. Navega al directorio `./mcp`.
2. Ejecuta el comando de despliegue en Google Cloud Run desde el código fuente. Asegúrate de incluir los flags `--source .`, `--allow-unauthenticated`, y establece la región (ej. `--region us-east1`).
3. Analiza el output de la terminal y **captura la URL pública** generada por Cloud Run para este servicio.

## Paso 2: Despliegue del AI Agent

1. Navega al directorio `./agent`.
2. Ejecuta el comando de despliegue en Google Cloud Run para el agente (`--source .`, `--allow-unauthenticated`, `--region us-east1`).
3. **Crucial:** Inyecta la URL del MCP capturada en el Paso 1 como una variable de entorno utilizando el flag correspondiente (ej. `--set-env-vars MCP_SERVER_URL=<URL_DEL_PASO_1>`). Si el código requiere el Project ID para Vertex AI o Firestore, inyéctalo también.

## Paso 3: Validación Interactiva

1. Una vez que el AI Agent esté correctamente desplegado y tengas su URL pública, ejecuta una petición `curl` directamente desde esta terminal hacia el endpoint del agente (ej. `/chat`).
2. El JSON payload debe incluir un `message` preguntando por información específica de los documentos (ej. "¿Cuáles son los topes de viáticos internacionales según las políticas de Industrias Stark?").
3. Imprime la respuesta final del agente en la consola para confirmar que la conexión en la nube entre el Agente y el servidor MCP fue exitosa.
