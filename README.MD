# TotalAgility – You.com Search Services Connector

This project provides integration between **Tungsten TotalAgility (KTA)** and **[You.com](https://you.com)**'s AI-powered search services. Two integration approaches are covered: **MCP (Model Context Protocol)** and **REST API**.

You.com offers three core capabilities that this connector exposes to TotalAgility:

| Capability | Description |
|------------|-------------|
| **Search** | Web search with AI-generated snippets |
| **Research** | Deep research with citations and source analysis |
| **Content** | AI content generation informed by live web data |

> For full details on available APIs see: <https://you.com/apis>

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Approach 1 – MCP Server](#approach-1--mcp-server)
- [Approach 2 – REST API](#approach-2--rest-api)
- [Project Contents](#project-contents)
- [Importing the TotalAgility Package](#importing-the-totalagility-package)
- [Resources](#resources)

---

## Prerequisites

Before you begin, choose **one** of the two integration paths below. Each path has its own prerequisite.

### Option A – MCP Server (no API key required)

You.com provides a **free MCP server** that can be used directly by compatible agents without needing an API key.

👉 **Get started:** <https://docs.you.com/build-with-agents/mcp-server>

### Option B – REST API (API key required)

To call the REST APIs you will need a valid You.com API key. There are two ways to obtain one:

| Tier | Details |
|------|---------|
| **Free** | Create a free account on the You.com platform. As of March 2025 this includes **$100 in free credits**. |
| **Paid** | Purchase a paid plan for higher rate-limits and production usage. |

👉 **Create your API key:** <https://you.com/platform>

---

## Approach 1 – MCP Server

The **Model Context Protocol (MCP)** approach allows TotalAgility agents to consume You.com's search, research, and content capabilities through a standards-based MCP server. This is the simplest way to get started — no API key management is required.

### How it works

1. The TotalAgility agent connects to You.com's hosted MCP server.
2. The MCP server exposes **Search**, **Research**, and **Content** tools.
3. The agent invokes tools via the MCP protocol; results are returned inline.

### Supported MCP Tools

| Tool | Description |
|------|-------------|
| `search` | Perform a web search and receive AI-summarised results |
| `research` | Conduct deep research with cited sources |
| `content` | Generate content grounded in live web data |

### Step-by-Step Setup

#### Step 1 – Add the MCP Server

Open **TotalAgility Advanced Studio** and navigate to **Integration → MCP Server**. Add the You.com MCP server URL to the configuration page.

> MCP Server URL can be found at: <https://docs.you.com/build-with-agents/mcp-server>

![Step 1 – Add the MCP Server](images/mcp_setup/1.%20Add%20the%20MCP%20Server.png)

#### Step 2 – Configure the GenAI Chat Control

On your TotalAgility form, add or configure a **GenAI Chat Control** and set it to use the newly added MCP service.

![Step 2 – Configure a GenAI Chat Control on a form](images/mcp_setup/2.%20Configure%20a%20GenAI%20Chat%20Control%20on%20a%20form.png)

#### Step 3 – Test it out

Run the form and interact with the chat control. The agent will now have access to You.com's Search, Research, and Content tools via MCP.

![Step 3 – Test the GenAI Chat Control](images/mcp_setup/3.%20Test%20the%20GenAI%20Chat%20Control.png)

### Example Prompt

An example prompt for formatting agent responses is provided in [`prompts/TA_Chat_Formatting_Example.md`](prompts/TA_Chat_Formatting_Example.md). This demonstrates how to instruct the agent on brand-consistent output formatting for use within TotalAgility chat controls.

---

## Approach 2 – REST API

The **REST API** approach gives full programmatic control over You.com's services. This is ideal when you need to call the APIs from TotalAgility custom services, business rules, or external integrations.

### Authentication

All REST API calls require an API key passed via the `X-API-Key` header:

```
X-API-Key: <YOUR_API_KEY>
```

The TotalAgility package included in this project stores the API key in a **Global Variable** so it can be managed securely and referenced across services.

### Available Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| Search | `GET` | Web search with AI snippets |
| Research | `GET` | Deep research with citations |
| Content | `GET` | Content generation from live web data |

> Full API reference & quickstart: <https://docs.you.com/quickstart>

### Getting Started

1. Obtain an API key from <https://you.com/platform>.
2. Import the Postman collection from the [`postman/`](postman/) directory and set your API key in the collection variables.
3. Test the endpoints to verify connectivity.
4. Import the TotalAgility package (see [Importing the TotalAgility Package](#importing-the-totalagility-package)) to deploy the custom services into your KTA environment.

---

## Project Contents

```
├── README.MD                  # This file
├── images/                    # Screenshots and diagrams
│   └── mcp_setup/             #   - MCP setup walkthrough screenshots
├── packages/                  # TotalAgility export package (.zip)
│   └── ...                    #   - Custom services for API integration
│   └── ...                    #   - Global variable for API key storage
│   └── ...                    #   - "Agent Services" category
│   └── ...                    #   - Web service definitions
│   └── ...                    #   - Example agent using the Search API
├── postman/                   # Postman collection & environment
│   └── ...                    #   - Pre-built requests for Search, Research & Content APIs
├── prompts/                   # Example prompts for TotalAgility agents
│   └── TA_Chat_Formatting_Example.md
```

### TotalAgility Package Includes

| Artefact | Description |
|----------|-------------|
| **Custom Services** | Server-side services that wrap the You.com REST APIs |
| **Global Variable** | Securely holds the You.com API key |
| **Category – "Agent Services"** | Organisational category for all connector artefacts |
| **Web Service Definitions** | WSDL / REST service definitions consumed by custom services |
| **Example Agent** | A working agent that demonstrates the Search API integration |

### Postman Collection

The [`postman/`](postman/) folder contains ready-made requests for each You.com API endpoint. Use these to explore and test the APIs before deploying into TotalAgility.

👉 Note that an environment variable should be used to configure the you.com ```X-API-Key``` under the Authorization tab of this collection. The imported collection looks for this key in an environment variable called ```{{you.com api key}}```.

---

## Importing the TotalAgility Package

To deploy the connector into your TotalAgility environment:

1. Open **TotalAgility Designer**.
2. Navigate to **Settings → Import / Export → Import Package**.
3. Select the package file from the [`packages/`](packages/) directory.
4. Follow the import wizard to map any environment-specific settings.
5. After import, update the **Global Variable** with your You.com API key.

> 📖 For detailed import instructions see the official documentation:
> <https://docshield.tungstenautomation.com//TotalAgility/en_US/2026.1-sy4i5uG9Tu/help/Designer/All_Shared/Import/t_importpackage.html>

---

## Resources

| Resource | Link |
|----------|------|
| You.com APIs Overview | <https://you.com/apis> |
| You.com Quickstart Guide | <https://docs.you.com/quickstart> |
| You.com MCP Server Docs | <https://docs.you.com/build-with-agents/mcp-server> |
| You.com Platform (API Keys) | <https://you.com/platform> |
| TotalAgility – Import Package | <https://docshield.tungstenautomation.com//TotalAgility/en_US/2026.1-sy4i5uG9Tu/help/Designer/All_Shared/Import/t_importpackage.html> |
