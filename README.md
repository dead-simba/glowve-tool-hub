# 🛠 Tools Hub

A personal directory of mini tools, scripts, and deployed utilities — backed by GitHub storage and hosted on GitHub Pages.

**Live URL:** https://dead-simba.github.io/glowve-tool-hub  
**Repo:** https://github.com/dead-simba/glowve-tool-hub  
**Owner:** Ali Tahir (LumaLabs / Glowve)

---

## How it Works

1. **GitHub Storage:** The single source of truth is [`tools.json`](./tools.json) in this repository.
2. **Dynamic UI:** The app (`index.html`) reads and writes to `tools.json` directly via the GitHub REST API using a personal access token (PAT).
3. **No Local State:** Adding, editing, or deleting a tool automatically commits the change back to the repository on GitHub, triggering an automatic redeployment of GitHub Pages.
4. **Script Bundles:** Each tool can contain multiple code files stored in its `files` array. The UI has a tabbed code viewer and copy buttons for quick access.
5. **Drag & Drop:** You can drag files directly from your computer or click to select them to attach them as files to any tool.

---

## For AI Sessions — How to Add a Tool Programmatically

Any AI agent interacting with this repo can easily register a tool by editing the [`tools.json`](./tools.json) file directly and pushing it to GitHub.

### 1. Tool JSON Schema

```json
{
  "id": "unique-kebab-case-id",
  "name": "Tool Name",
  "type": "script",
  "desc": "Short description of what the tool does.",
  "tags": ["Python", "Images"],
  "url": "https://...",
  "code": "# Quick command template\npython3 script.py",
  "files": [
    {
      "name": "script.py",
      "language": "python",
      "content": "print('Hello World')\n"
    }
  ],
  "icon": "🖼"
}
```

* **`id`** *(Required)*: Unique kebab-case string (e.g., `webp-converter`).
* **`name`** *(Required)*: Human-readable display name.
* **`type`** *(Required)*: One of `'script'`, `'webapp'`, `'cli'`, `'api'`, or `'other'`.
* **`files`** *(Optional)*: Array of objects representing files attached to the tool.
  * **`language`** options: `'python'`, `'javascript'`, `'typescript'`, `'bash'`, `'json'`, `'yaml'`, `'markdown'`, or `'text'`.

---

### 2. Programmatic Git Workflow

To add a tool from your terminal/agent environment:

1. **Pull the latest changes:**
   ```bash
   git pull --rebase
   ```
2. **Read & Edit `tools.json`:**
   Append your new tool object to the JSON array in [`tools.json`](./tools.json).
3. **Commit & Push:**
   ```bash
   git add tools.json
   git commit -m "feat: programmatically add tool [tool-id]"
   git push
   ```

Within 60 seconds, GitHub Pages will auto-deploy, and your tool will be visible on the live hub.

---

### 3. Setting Up Your Browser Token (One-time)

If you are using the web interface to add/edit tools:
1. Generate a GitHub **Fine-Grained Personal Access Token** at [github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta).
2. Under **Repository Access**, select **Only select repositories** and pick `glowve-tool-hub`.
3. Under **Repository permissions**, find **Contents** and set it to **Read and write** (this automatically gives you metadata access).
4. Generate the token, copy it, open the live website, click the ⚙ settings gear, paste your token, and click **Save & Connect**.

---

## Current Tools

| Tool | Type | Description |
| :--- | :--- | :--- |
| **WebP Image Converter** | Script | Batch-converts JPG & PNG to WebP. ~95% file size reduction. |
| **Glowvé Blog Writer & Cost Tracker** | CLI | Autonomous multi-agent pipeline using Gemini models, DataForSEO, and Pexels. Includes cost tracking script. |
| **Gemini TTS Script Creator & Generator** | Script | Batch Text-to-Speech generation scripts using Gemini 3.1 Flash. Supports emotion tags, voice customization, and WAV headers. |
| **PostEx COD Tracker & FIFO Allocator** | Script | PostEx COD (Cash on Delivery) API tracking client & FIFO/FEFO stock allocation engine using Drizzle ORM transactions. |
