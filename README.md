# 🚀 Build with AI 2026: Serverless AI Agent Workshop

Welcome to the official repository for the **"De la idea al despliegue: Crea tu propio Agente de IA Serverless con Google Cloud"** workshop, presented at the **Build with AI 2026** event hosted at **Universidad de la Sabana**, Bogotá.

This repository contains the foundational code and instructions to build a production-ready, serverless AI Agent utilizing Google Cloud Run, Firestore, and the Model Context Protocol (MCP) via the Agent Development Kit (ADK 2.0).

## ⚠️ Disclaimer

**Everything in this repository is purely academical.** The code, mock data, and architectures provided here are designed strictly for educational purposes and demonstrations during the workshop. If you plan to adapt this for production environments, please ensure you implement proper security audits, robust authentication, and enterprise-grade error handling.

## 📋 Pre-requisites

To follow along with the hands-on portion of the workshop, please ensure you have the following tools installed and configured on your local machine:

* **Python 3.14+**: The core language for our agent and server.
* **[uv](https://github.com/astral-sh/uv)**: An extremely fast Python package and project manager. We will use this to manage dependencies and virtual environments.
* **Docker**: Required for building and testing containers locally before deploying to the cloud.
* **Google Cloud SDK (`gcloud`)**: The command-line interface for Google Cloud. Ensure you are authenticated (`gcloud auth login`).
* **Node.js & npm** (Optional but recommended): Required if you wish to run the MCP Inspector locally (`npx @modelcontextprotocol/inspector`).
* **Your favorite IDE**: We will be demonstrating with Antigravity, but VS Code or any text editor works fine.

## 🏗️ Getting Started

During the workshop, we will divide the work into two main components:
1. **The MCP Server:** Responsible for ingesting our internal documentation securely.
2. **The AI Agent:** Powered by GCP's Agent Platform, orchestrating the logic and state.

*(Specific `uv` initialization and `gcloud deploy` commands will be provided during the live session and generated via our workshop prompts).*

---

<div align="center">
  <b>Made in Colombia with Love ❤️</b>
</div>