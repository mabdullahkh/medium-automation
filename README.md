# Medium MCP Server & Automated SEO Blog Publishing Pipeline

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](medium-mcp-server/LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Model Context Protocol](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-black)](https://modelcontextprotocol.io/)
[![Playwright](https://img.shields.io/badge/Playwright-Browser%20Automation-2EAD33?logo=playwright&logoColor=white)](https://playwright.dev/)

**Publish, manage, and automate Medium articles directly from AI agents (Claude, Cursor, Windsurf, and custom LLM workflows) without a Medium API token.**

This repository combines a **browser-based Medium MCP (Model Context Protocol) Server** powered by TypeScript and Playwright with an end-to-end **SEO blog automation pipeline**—including Markdown articles and custom visual assets ready for automated publishing.

---

## Why Use a Browser-Based Medium MCP Server?

Medium stopped issuing new Integration API tokens in 2023, making traditional REST API automation impossible for new developers and AI workflows. **Medium MCP Server** solves this by automating a real Chromium browser via Playwright:

- **No Medium API Key Required:** Authenticates using your own Medium browser session.
- **Persistent Local Session:** Log in once interactively; subsequent runs execute headlessly using `medium-session.json` (gitignored and stored strictly locally).
- **Full AI Agent Integration:** Exposes standardized **Model Context Protocol (MCP)** tools so any MCP-compatible AI assistant can draft, publish, search, and read Medium posts.
- **SEO Content Pipeline Ready:** Includes structured SEO blog templates, metadata, and image assets (`blog-assets/`) for automated content marketing.

---

## Architecture & Workflow

```text
AI Agent (Claude / Cursor / LLM)
        │
        ▼  (Model Context Protocol - stdio)
Medium MCP Server (TypeScript)
        │
        ▼  (Playwright Browser Automation)
Medium Web Editor & Profile  ◄──►  Local Session (medium-session.json)
```

---

## Repository Structure

```text
medium-MCP/
├── medium-mcp-server/          # Core TypeScript MCP Server & Playwright client
│   ├── src/
│   │   ├── index.ts            # MCP server entry point & tool registration
│   │   └── browser-client.ts   # Playwright automation for Medium
│   ├── examples/               # Sample LLM / MCP client configurations
│   ├── .env.example            # Environment variable template
│   └── package.json
├── blog-assets/                # Hero & inline images for SEO blog posts
├── novtek-seo-blog*.md         # Automated SEO blog articles (Markdown + metadata)
├── .gitignore                  # Protects sessions, .env, build outputs & logs
└── README.md
```

---

## Quick Start & Installation

### Prerequisites
- **Node.js** v16 or higher
- **npm** or **yarn**
- A **Medium** account (email/password login recommended for persistent sessions)

### 1. Clone the Repository
```bash
git clone https://github.com/mabdullahkh/medium-automation.git
cd medium-automation/medium-mcp-server
```

### 2. Install Dependencies & Playwright Browser
```bash
npm install
npx playwright install chromium
```

### 3. Build the MCP Server
```bash
npm run build
```

### 4. Configure Your MCP Client (Claude Desktop / Cursor / IDE)
Add the following to your MCP configuration file (for example, `claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "medium-mcp": {
      "command": "node",
      "args": ["/absolute/path/to/medium-automation/medium-mcp-server/dist/index.js"],
      "cwd": "/absolute/path/to/medium-automation/medium-mcp-server"
    }
  }
}
```

> **First-Time Login:** On your first tool call (or by invoking `login-to-medium`), a Chromium window will open so you can sign in to Medium. Your session is saved locally to `medium-session.json` and reused automatically on future runs.

---

## Available MCP Tools

| Tool Name | Description | Key Parameters |
| :--- | :--- | :--- |
| `publish-article` | Publish a new article or save a draft to Medium | `title`, `content` (Markdown), `tags?`, `isDraft?` |
| `get-my-articles` | Retrieve published articles from your Medium profile | None |
| `get-article-content` | Extract full content from any Medium article URL | `url`, `requireLogin?` |
| `search-medium` | Search Medium articles by keywords | `keywords` (`string[]`) |
| `login-to-medium` | Open browser to authenticate and save session | None |

---

## Security & Privacy

This repository is configured for safe public hosting:
- **Session Isolation:** `medium-session.json`, `playwright-session.json`, and `session-*.json` are explicitly excluded via `.gitignore` and are **never** committed.
- **Environment Variables:** `.env`, `.env.local`, and `.env.*.local` are gitignored; only `.env.example` is tracked.
- **100% Local Execution:** All browser automation runs locally on your machine—no third-party proxy or external credential storage is used.

---

## Use Cases

- **Automated SEO Blogging:** Turn Markdown drafts and AI-researched articles into formatted Medium posts or drafts automatically.
- **AI Content Repurposing:** Connect Claude or LangGraph agents to publish technical tutorials, release notes, and thought-leadership pieces.
- **Research & Content Extraction:** Use `search-medium` and `get-article-content` inside agentic RAG workflows.

---

## Contributing & License

Contributions, issues, and feature requests are welcome! See [medium-mcp-server/CONTRIBUTING.md](medium-mcp-server/CONTRIBUTING.md) for guidelines.

Licensed under the **MIT License** — see [medium-mcp-server/LICENSE](medium-mcp-server/LICENSE) for details.

---

## Author & Custom AI Automation Services

Maintained by **Muhammad Abdullah** — Senior AI & Full-Stack Engineer at **[Novtek](https://novtek.co.uk/)** ([@mabdullahkh on Fiverr](https://www.fiverr.com/mabdullahkh)).

Need custom **MCP Servers, LangGraph AI Agents, RAG Pipelines, or AI SaaS Automation**?
- Website: [https://novtek.co.uk/](https://novtek.co.uk/)
- Fiverr: [https://www.fiverr.com/mabdullahkh](https://www.fiverr.com/mabdullahkh)

