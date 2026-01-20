---
tags:
  - type/literature
  - media/article
  - status/reading
  - topic/dev
source: "OpenAI Beta Docs"
date_saved: 2026-01-12
---

# 📑 OpenAI : Connectors and MCP Servers

## 🧐 Contexte
Documentation officielle sur l'utilisation des **Connectors** et **Remote MCP Servers** pour donner des capacités externes aux modèles (Beta).

## 🔑 Idées Clés (Extraction)
- [[Model Context Protocol (MCP)]]
- [[Connectors vs Remote MCP Servers]]
- [[Risques de sécurité MCP]]

---

## 📄 Contenu Original

Use connectors and remote MCP servers to give models new capabilities.

In addition to tools you make available to the model with [function calling](https://platform.openai.com/docs/guides/function-calling), you can give models new capabilities using **connectors** and **remote MCP servers**. These tools give the model the ability to connect to and control external services when needed to respond to a user's prompt. These tool calls can either be allowed automatically, or restricted with explicit approval required by you as the developer.

*   **Connectors** are OpenAI-maintained MCP wrappers for popular services like Google Workspace or Dropbox, like the connectors available in [ChatGPT](https://chatgpt.com).
*   **Remote MCP servers** can be any server on the public Internet that implements a remote [Model Context Protocol](https://modelcontextprotocol.io/introduction) (MCP) server.

[... Rest of the content would go here, truncated for layout clarity ...]
