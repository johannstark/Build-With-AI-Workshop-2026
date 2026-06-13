# 🚀 Build with AI 2026: Workshop de Agentes de IA Serverless

Bienvenido al repositorio oficial del workshop **"De la idea al despliegue: Crea tu propio Agente de IA Serverless con Google Cloud"**, presentado en el evento **Build with AI 2026** en la **Universidad de la Sabana**, Bogotá.

Este repositorio contiene el código base y las instrucciones para construir un Agente de IA serverless listo para producción, utilizando Google Cloud Run, Firestore y el Model Context Protocol (MCP) a través del Agent Development Kit (ADK 2.0).

## ⚠️ Aviso Legal (Disclaimer)

**Todo el contenido de este repositorio es netamente académico.** El código, los datos simulados (mock data) y las arquitecturas proporcionadas aquí están diseñados estrictamente para fines educativos y de demostración durante el workshop. Si planeas adaptar esto para entornos de producción, asegúrate de implementar auditorías de seguridad adecuadas, autenticación robusta y un manejo de errores a nivel empresarial.

## 📋 Prerrequisitos

Para poder seguir la parte práctica del workshop, asegúrate de tener las siguientes herramientas instaladas y configuradas en tu máquina local:

* **Python 3.14+**: El lenguaje principal para nuestro agente y servidor MCP.
* **[uv](https://github.com/astral-sh/uv)**: Un gestor de proyectos y paquetes de Python extremadamente rápido. Lo usaremos para gestionar las dependencias y los entornos virtuales.
* **Docker**: Necesario para construir y probar contenedores localmente antes de desplegarlos en la nube.
* **Google Cloud SDK (`gcloud`)**: La interfaz de línea de comandos para Google Cloud. Asegúrate de estar autenticado ejecutando (`gcloud auth login`).
* **Node.js y npm** (Opcional pero recomendado): Necesario si deseas ejecutar el MCP Inspector localmente (`npx @modelcontextprotocol/inspector`).
* **Tu IDE favorito**: Haremos la demostración usando Antigravity, pero VS Code o cualquier editor de código funcionará perfectamente.

## ☁️ Preparación de Google Cloud (Antes de Desplegar)

Para que los contenedores puedan subirse y comunicarse en la nube, debes tener tu proyecto de GCP configurado. Por favor, asegúrate de completar estos pasos antes de la Fase 4 del workshop:

1. **Crear un Proyecto y habilitar Facturación:**
   * Crea un proyecto nuevo en [Google Cloud Console](https://console.cloud.google.com/).
   * Asegúrate de tener una cuenta de facturación activa vinculada al proyecto (Cloud Run requiere facturación, aunque usaremos la capa gratuita).
2. **Habilitar las APIs necesarias:**
   Abre la terminal de Cloud Shell (o tu terminal local autenticada) y ejecuta:

    ```bash
    gcloud services enable run.googleapis.com cloudbuild.googleapis.com aiplatform.googleapis.com firestore.googleapis.com
    ```

3. **Inicializar Firestore:**
    * Ve a la consola de GCP, busca Firestore y haz clic en "Create Database".
    * Selecciona el modo Native (Nativo) y elige la misma región donde desplegarás tus servicios (ej. us-central1).

4. **Autenticación Local:**
    * Asegúrate de que tu CLI esté apuntando al proyecto correcto:

    ```bash
    gcloud auth login
    gcloud config set project TU_PROJECT_ID
    ```


## 🏗️ Primeros Pasos

Durante el workshop, dividiremos el trabajo en dos componentes principales:
1. **El Servidor MCP:** Responsable de ingerir nuestra documentación interna de forma segura.
2. **El Agente de IA:** Impulsado por la plataforma de agentes de GCP (Vertex AI), encargado de orquestar la lógica y mantener el estado de la conversación.

*(Los comandos específicos de inicialización con `uv` y despliegue con `gcloud` se proporcionarán durante la sesión en vivo y se generarán a través de los prompts maestros de nuestro workshop).*

---

<div align="center">
  <b>Hecho en Colombia con Amor ❤️</b>
</div>