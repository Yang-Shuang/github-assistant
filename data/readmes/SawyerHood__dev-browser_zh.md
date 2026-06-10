<p align="center">
  <img src="assets/header.png" alt="Dev Browser - Browser automation for Claude Code" width="100%">
</p>

由 [Do Browser](https://dobrowser.io) 提供支持。

一款浏览器自动化工具，允许 AI 智能体和开发者通过沙盒化的 JavaScript 脚本来控制浏览器。

**核心特性：**

- **沙盒执行（Sandboxed execution）** - 脚本在 QuickJS WASM 沙盒中运行，无法访问宿主机环境
- **页面持久化（Persistent pages）** - 只需导航一次，即可在多个脚本间跨会话交互
- **自动连接（Auto-connect）** - 连接到正在运行的 Chrome，或启动全新的 Chromium
- **完整的 Playwright API** - 支持 `goto`、`click`、`fill`、定位器（locators）、`evaluate`、截图等功能

## 演示

https://github.com/user-attachments/assets/c6cf7fb9-b1dc-46ed-93b9-6e7240990c53

## CLI 安装

```bash
npm install -g dev-browser
dev-browser install    # installs Playwright + Chromium
```

### 快速入门

```bash
# Launch a headless browser and run a script
dev-browser --headless <<'EOF'
const page = await browser.getPage("main");
await page.goto("https://example.com", { waitUntil: "domcontentloaded" });
console.log(await page.title());
EOF

# Connect to your running Chrome (enable at chrome://inspect/#remote-debugging)
dev-browser --connect <<'EOF'
const tabs = await browser.listPages();
console.log(JSON.stringify(tabs, null, 2));
EOF
```

### PowerShell（Windows）

```powershell
@"
const page = await browser.getPage("main");
await page.goto("https://example.com", { waitUntil: "domcontentloaded" });
console.log(await page.title());
"@ | dev-browser
```

With `--connect`:

```powershell
@"
const page = await browser.getPage("main");
console.log(await page.title());
"@ | dev-browser --connect
```

### Windows 注意事项

PowerShell 安装：

```powershell
npm install -g dev-browser
dev-browser install
```

要在 Windows 上附加到正在运行的 Chrome 实例：

```powershell
chrome.exe --remote-debugging-port=9222
dev-browser --connect
```

Windows 的 npm 安装会在 `postinstall` 阶段下载原生的 `dev-browser-windows-x64.exe` 发布文件，生成的 npm shim 包装脚本会直接调用该可执行文件。

### 与 AI 智能体配合使用

安装完成后，只需让智能体运行 `dev-browser --help` ——帮助输出中包含完整的 LLM 使用指南、示例及 API 参考。无需额外安装插件或技能（skill）。

<details>
<summary>在 Claude Code 中免权限提示运行 dev-browser</summary>

默认情况下，Claude Code 每次运行 Bash 命令时都会请求审批。你可以将其添加到设置中的允许（allow）列表，从而预授权 `dev-browser`，使其无需权限检查即可直接运行。

**项目级配置** —— 在项目根目录的 `.claude/settings.json` 中添加：

```json
{
  "permissions": {
    "allow": [
      "Bash(dev-browser *)"
    ]
  }
}
```

**用户级（全局）配置** —— 添加到 `~/.claude/settings.json`：

```json
{
  "permissions": {
    "allow": [
      "Bash(dev-browser *)"
    ]
  }
}
```

模式 `Bash(dev-browser *)` 可匹配任何以 `dev-browser ` 开头并跟随参数的命令（例如 `dev-browser --headless`、`dev-browser --connect`）。这是安全的，因为 dev-browser 脚本在沙盒化的 QuickJS WASM 环境中运行，无法访问宿主机文件系统或网络。

你也可以在同一列表中允许相关命令：

```json
{
  "permissions": {
    "allow": [
      "Bash(dev-browser *)",
      "Bash(npx dev-browser *)"
    ]
  }
}
```

> **提示：** 如果你之前已被请求并点击了“始终允许”，Claude Code 会自动添加该特定命令模式。通过设置文件的方式可让你在首次运行前完成预授权。

</details>

<details>
<summary>传统插件安装（Claude Code / Amp / Codex）</summary>

### Claude Code

```
/plugin marketplace add sawyerhood/dev-browser
/plugin install dev-browser@sawyerhood/dev-browser
```

安装完成后请重启 Claude Code。

### Amp / Codex

将技能（skill）复制到你的 skills 目录：

```bash
# For Amp: ~/.claude/skills | For Codex: ~/.codex/skills
SKILLS_DIR=~/.claude/skills  # or ~/.codex/skills

mkdir -p $SKILLS_DIR
git clone https://github.com/sawyerhood/dev-browser /tmp/dev-browser-skill
cp -r /tmp/dev-browser-skill/skills/dev-browser $SKILLS_DIR/dev-browser
rm -rf /tmp/dev-browser-skill
```

</details>

## 脚本 API

脚本在沙盒化的 QuickJS 运行时中执行（非 Node.js）。可用的全局对象：

```javascript
// Browser control
browser.getPage(nameOrId)    // Get/create named page, or connect to tab by targetId
browser.newPage()            // Create anonymous page (cleaned up after script)
browser.listPages()          // List all tabs: [{id, url, title, name}]
browser.closePage(name)      // Close a named page

// File I/O (restricted to ~/.dev-browser/tmp/)
await saveScreenshot(buf, name)   // Save screenshot buffer, returns path
await writeFile(name, data)       // Write file, returns path
await readFile(name)              // Read file, returns content

// Output
console.log/warn/error/info       // Routed to CLI stdout/stderr
```

页面是完整的 [Playwright Page 对象](https://playwright.dev/docs/api/class-page) —— 支持 `goto`、`click`、`fill`、定位器（locator）、`evaluate`、截图等功能，以及 `page.snapshotForAI({ track?, depth?, timeout? })` 等所有其他方法。后者会返回 `{ full, incremental? }`，专为 AI 友好的页面快照设计。

## 性能基准测试

| Method                  | Time    | Cost  | Turns | Success |
| ----------------------- | ------- | ----- | ----- | ------- |
| **Dev Browser**         | 3m 53s  | $0.88 | 29    | 100%    |
| Playwright MCP          | 4m 31s  | $1.45 | 51    | 100%    |
| Playwright Skill        | 8m 07s  | $1.45 | 38    | 67%     |
| Claude Chrome Extension | 12m 54s | $2.81 | 80    | 100%    |

_See [dev-browser-eval](https://github.com/SawyerHood/dev-browser-eval) for methodology._

## 许可证

MIT

## 作者

[Sawyer Hood](https://github.com/sawyerhood)