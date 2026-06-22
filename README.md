# 🛠 Tools Hub

A personal directory of mini tools, scripts, and deployed utilities — hosted on GitHub Pages.

**Live URL:** https://dead-simba.github.io/glowve-tool-hub  
**Repo:** https://github.com/dead-simba/glowve-tool-hub  
**Owner:** Ali Tahir (LumaLabs / Glowve)

---

## For AI Sessions — How to Add a Tool Programmatically

All tool data lives in **one place** inside [`index.html`](./index.html): the `defaultTools` array in the `<script>` block. Tools added by the user via the browser UI are saved to `localStorage` and are separate from this array.

To permanently add a tool (so it shows up for everyone, not just one browser session), **edit the `defaultTools` array in `index.html`**.

### Tool Object Schema

```js
{
  id:       'unique-kebab-case-id',   // REQUIRED. Unique string, no spaces.
  name:     'Tool Name',              // REQUIRED. Human-readable display name.
  type:     'script',                 // REQUIRED. One of: 'script' | 'webapp' | 'cli' | 'api' | 'other'
  desc:     'What this tool does.',   // Optional. One sentence shown on the card.
  tags:     ['Python', 'Images'],     // Optional. Array of strings for filtering.
  url:      'https://...',            // Optional. Link for web apps, APIs, deployed tools.
  filepath: '/path/to/file.py',       // Optional. Local path or GitHub URL to the source file.
  code:     `# Commands to use it\npython3 script.py --flag`,  // Optional. Shown in a code block with a Copy button.
  icon:     '🖼'                      // Optional. Emoji shown on the card. Defaults to type icon if omitted.
}
```

**Type → what fields make sense:**

| Type | Use `url` | Use `filepath` | Use `code` |
|------|-----------|----------------|------------|
| `script` | ✗ | ✓ local path | ✓ commands |
| `webapp` | ✓ live URL | ✗ | ✗ |
| `cli` | ✗ | ✓ | ✓ commands |
| `api` | ✓ endpoint | ✗ | ✓ example curl |
| `other` | ✓ optional | ✓ optional | ✓ optional |

---

### Step-by-step: Add a New Tool

1. **Open** `index.html`
2. **Find** the `defaultTools` array (search for `const defaultTools = [`)
3. **Append** a new object to the array before the closing `]`
4. **Commit and push** — GitHub Pages auto-deploys within ~1 minute

#### Example — Adding a new script tool:

```js
// Find this in index.html:
const defaultTools = [
  { id: 'default-webp', ... },  // existing tool
  // ← ADD NEW TOOL HERE
];
```

```js
// Add this object:
{
  id: 'resize-images',
  name: 'Image Resizer',
  type: 'script',
  desc: 'Batch-resizes images to a target width while preserving aspect ratio.',
  tags: ['Python', 'Images'],
  filepath: '',
  code: `python3 resize.py --dir ./images --width 1200`,
  icon: '📐'
},
```

#### Example — Adding a Vercel web app:

```js
{
  id: 'glowve-demand-test',
  name: 'Glowve Demand Test',
  type: 'webapp',
  desc: 'Landing page demand-testing tool for Glowve product concepts.',
  tags: ['Vercel', 'Glowve', 'Testing'],
  url: 'https://your-project.vercel.app',
  filepath: '',
  code: '',
  icon: '🌐'
},
```

---

### Git Workflow

The repo is at `/Users/alitahir/Documents/Programming Projects/Claude Code/tools-hub/`.

```bash
cd "/Users/alitahir/Documents/Programming Projects/Claude Code/tools-hub"

# After editing index.html:
git add index.html
git commit -m "add tool: [tool name]"
git push
```

GitHub Pages deploys automatically. Live in ~60 seconds.

---

## Architecture Notes

- **Single file** — the entire app is `index.html`. No build step, no dependencies, no npm.
- **User-added tools** — tools added via the browser UI ("Add tool" button) are stored in `localStorage` under the key `tools-hub-v1`. These are browser-local only.
- **Default tools** — the `defaultTools` array in the JS is the fallback when `localStorage` is empty or on a fresh browser. This is where AI sessions should add permanent tools.
- **No backend** — everything runs client-side. No server, no database.
- **Hosted on** GitHub Pages (static, free).

---

## Current Tools

| Tool | Type | Description |
|------|------|-------------|
| WebP Image Converter | Script | Batch-converts JPG/PNG → WebP. ~95% size reduction. |

> Update this table when adding new tools.
