# Unified App Launcher Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a static application launcher at `www.zaza.de5.net` that links to the three deployed Hydro SAP tools.

**Architecture:** Create a small static site in the `Hydro_sap` workspace. `index.html` owns semantic content and links, `styles.css` owns responsive presentation, and `README.md` records deployment/domain notes.

**Tech Stack:** Static HTML5, CSS3, no JavaScript, no backend.

---

## File Structure

- Create `index.html`: the launcher page with header, three app cards, and direct HTTPS links.
- Create `styles.css`: responsive layout, accessible focus states, card styling, and mobile adjustments.
- Create `README.md`: deployment notes for `www`, `fraction`, `report`, and `dn` subdomains.

## Task 1: Static Launcher Markup

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the launcher HTML**

Create `index.html` with exactly this structure:

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hydro SAP 工作台</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <main class="shell">
    <header class="page-header" aria-labelledby="page-title">
      <p class="eyebrow">Hydro SAP</p>
      <h1 id="page-title">应用启动器</h1>
      <p class="lede">统一入口，快速打开常用业务工具。</p>
    </header>

    <section class="app-grid" aria-label="应用列表">
      <article class="app-card">
        <div class="app-icon" aria-hidden="true">分</div>
        <div class="app-content">
          <h2>分数计算工具</h2>
          <p>用于录取分数、分数线或相关历史工具查询与计算。</p>
          <a class="app-url" href="https://fraction.zaza.de5.net">fraction.zaza.de5.net</a>
        </div>
        <a class="open-button" href="https://fraction.zaza.de5.net">打开应用</a>
      </article>

      <article class="app-card">
        <div class="app-icon" aria-hidden="true">报</div>
        <div class="app-content">
          <h2>销售报表工具</h2>
          <p>上传 Excel 文件，完成字段映射、预览和销售报表导出。</p>
          <a class="app-url" href="https://report.zaza.de5.net">report.zaza.de5.net</a>
        </div>
        <a class="open-button" href="https://report.zaza.de5.net">打开应用</a>
      </article>

      <article class="app-card">
        <div class="app-icon" aria-hidden="true">DN</div>
        <div class="app-content">
          <h2>Delivery Note 工具</h2>
          <p>处理 Delivery Note PDF 和客户资料，生成更新后的 PDF 文件。</p>
          <a class="app-url" href="https://dn.zaza.de5.net">dn.zaza.de5.net</a>
        </div>
        <a class="open-button" href="https://dn.zaza.de5.net">打开应用</a>
      </article>
    </section>
  </main>
</body>
</html>
```

- [ ] **Step 2: Verify the links in markup**

Run: `Select-String -Path .\index.html -Pattern 'https://fraction.zaza.de5.net|https://report.zaza.de5.net|https://dn.zaza.de5.net'`

Expected: output includes all three URLs.

## Task 2: Responsive Visual Styling

**Files:**
- Create: `styles.css`

- [ ] **Step 1: Create the stylesheet**

Create `styles.css` with exactly this content:

```css
:root {
  color-scheme: light;
  --bg: #f4f7f8;
  --panel: #ffffff;
  --text: #172026;
  --muted: #5f6f78;
  --line: #d9e2e6;
  --accent: #006c67;
  --accent-strong: #004f4b;
  --accent-soft: #e5f3f1;
  --focus: #f3b233;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-height: 100vh;
  font-family: "Segoe UI", "Microsoft YaHei", Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}

a {
  color: inherit;
}

.shell {
  width: min(1120px, calc(100% - 32px));
  margin: 0 auto;
  padding: 56px 0;
}

.page-header {
  margin-bottom: 28px;
}

.eyebrow {
  margin: 0 0 8px;
  color: var(--accent);
  font-size: 14px;
  font-weight: 700;
  letter-spacing: 0;
  text-transform: uppercase;
}

h1 {
  margin: 0;
  font-size: 40px;
  line-height: 1.15;
  letter-spacing: 0;
}

.lede {
  margin: 12px 0 0;
  color: var(--muted);
  font-size: 17px;
}

.app-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.app-card {
  display: flex;
  min-height: 280px;
  flex-direction: column;
  gap: 20px;
  justify-content: space-between;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: var(--panel);
  padding: 22px;
  box-shadow: 0 14px 30px rgba(26, 47, 55, 0.08);
}

.app-icon {
  display: inline-flex;
  width: 44px;
  height: 44px;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  background: var(--accent-soft);
  color: var(--accent-strong);
  font-weight: 800;
}

.app-content h2 {
  margin: 0 0 10px;
  font-size: 22px;
  line-height: 1.25;
  letter-spacing: 0;
}

.app-content p {
  margin: 0 0 18px;
  color: var(--muted);
  font-size: 15px;
  line-height: 1.65;
}

.app-url {
  color: var(--accent-strong);
  font-size: 14px;
  font-weight: 600;
  overflow-wrap: anywhere;
  text-decoration: none;
}

.app-url:hover {
  text-decoration: underline;
}

.open-button {
  display: inline-flex;
  min-height: 44px;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  background: var(--accent);
  color: #ffffff;
  font-weight: 700;
  text-decoration: none;
}

.open-button:hover {
  background: var(--accent-strong);
}

.open-button:focus-visible,
.app-url:focus-visible {
  outline: 3px solid var(--focus);
  outline-offset: 3px;
}

@media (max-width: 860px) {
  .shell {
    padding: 36px 0;
  }

  .app-grid {
    grid-template-columns: 1fr;
  }

  .app-card {
    min-height: 0;
  }
}

@media (max-width: 520px) {
  .shell {
    width: min(100% - 20px, 1120px);
    padding: 28px 0;
  }

  h1 {
    font-size: 32px;
  }

  .lede {
    font-size: 16px;
  }

  .app-card {
    padding: 18px;
  }
}
```

- [ ] **Step 2: Verify CSS avoids one-note blue/purple styling**

Run: `Select-String -Path .\styles.css -Pattern '#|rgb|hsl'`

Expected: colors include neutral, teal, and yellow focus values; no dominant purple or dark-blue palette.

## Task 3: Deployment Notes

**Files:**
- Create: `README.md`

- [ ] **Step 1: Create deployment notes**

Create `README.md` with exactly this content:

```markdown
# Hydro SAP 应用启动器

This repository contains the static homepage for `https://www.zaza.de5.net`.

## Applications

| Name | URL |
| --- | --- |
| 分数计算工具 | https://fraction.zaza.de5.net |
| 销售报表工具 | https://report.zaza.de5.net |
| Delivery Note 工具 | https://dn.zaza.de5.net |

## Deployment

Deploy `index.html` and `styles.css` to the web root for `www.zaza.de5.net`.

The application launcher only links to the deployed systems. It does not start, proxy, embed, or merge them.

## Domain Mapping

- `www.zaza.de5.net`: unified application launcher
- `fraction.zaza.de5.net`: fraction calculator tool
- `report.zaza.de5.net`: sales report tool
- `dn.zaza.de5.net`: Delivery Note tool
```

- [ ] **Step 2: Verify documentation includes all domains**

Run: `Select-String -Path .\README.md -Pattern 'www.zaza.de5.net|fraction.zaza.de5.net|report.zaza.de5.net|dn.zaza.de5.net'`

Expected: output includes all four domains.

## Task 4: Local Verification

**Files:**
- Verify: `index.html`
- Verify: `styles.css`
- Verify: `README.md`

- [ ] **Step 1: Confirm the site is static**

Run: `Get-ChildItem -File`

Expected: output includes `index.html`, `styles.css`, and `README.md`; no backend files are required.

- [ ] **Step 2: Open locally in a browser**

Open `index.html` through the in-app browser or a local static server.

Expected: page shows the Hydro SAP header and three cards: 分数计算工具, 销售报表工具, Delivery Note 工具.

- [ ] **Step 3: Verify desktop layout**

Use a viewport around `1440x900`.

Expected: three cards appear in one row, text fits inside each card, and buttons are visible.

- [ ] **Step 4: Verify mobile layout**

Use a viewport around `390x844`.

Expected: cards stack vertically, URLs wrap without overflow, and no text overlaps.

- [ ] **Step 5: Verify link targets**

Inspect or click each card button.

Expected:

- 分数计算工具 opens `https://fraction.zaza.de5.net`
- 销售报表工具 opens `https://report.zaza.de5.net`
- Delivery Note 工具 opens `https://dn.zaza.de5.net`

- [ ] **Step 6: Commit if a git repository exists**

Run: `git status --short`

If the workspace is a git repository, run:

```bash
git add index.html styles.css README.md docs/superpowers/specs/2026-06-14-unified-app-launcher-design.md docs/superpowers/plans/2026-06-14-unified-app-launcher.md
git commit -m "feat: add unified app launcher"
```

If the workspace is not a git repository, record that commit was skipped because no `.git` directory exists.

## Self-Review

- Spec coverage: The plan creates a static launcher, includes all three app cards, preserves independent deployments, and documents the `www` to `fraction` domain change.
- Placeholder scan: No placeholder tasks remain.
- Type consistency: File names and URLs are consistent across tasks.
