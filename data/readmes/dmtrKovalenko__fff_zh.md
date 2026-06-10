<img alt="FFF" src="./assets/logo-orange.png" width="300">

<p>
  <i>A file search toolkit for humans and AI agents. Really fast.</i>
</p>

Typo-resistant path and content search, frecency-ranked file access, a background watcher, and a lightweight in-memory content index. Way faster than CLIs like ripgrep and fzf in any long-running process that searches more than once.

Originally started as [Neovim plugin](#neovim-plugin) people loved, but it turned out that plenty of AI harnesses and code editors need the same thing: accurate, fast file search as a library. That is what fff is.

---

Pick what you are interested in:

<details id="mcp-server">
<summary>
<h2>MCP server</h2>
</summary>

Works with Claude Code, Codex, OpenCode, Cursor, Cline, and any MCP-capable client. Fewer grep roundtrips, less wasted context, faster answers.

![Benchmark chart comparing FFF against the built-in AI file-search tools](./chart.png)

### One-line install

Linux / macOS:

```bash
curl -L https://dmtrkovalenko.dev/install-fff-mcp.sh | bash
```

Windows (PowerShell):

```powershell
irm https://raw.githubusercontent.com/dmtrKovalenko/fff.nvim/main/install-mcp.ps1 | iex
```

The scripts live at [`install-mcp.sh`](./install-mcp.sh) and [`install-mcp.ps1`](./install-mcp.ps1) if you want to read them first.

It prints the exact wiring instructions for your client. Once the server is connected, ask the agent to "use fff" and it picks up the `ffgrep`, `fffind`, and `fff-multi-grep` tools.

### Recommended agent prompt

Drop this into your project's `CLAUDE.md` or equivalent:

```markdown
For any file search or grep in the current git-indexed directory, use fff tools.
```

### What changes

- Frecency memory. Files you actually open rank higher next time. Warm-up from git touch history runs automatically.
- Definition-first hinting. Lines that look like code definitions are classified on the Rust side, no regex overhead in your prompt.
- Smart-case with auto-fuzzy fallback. `IsOffTheRecord` finds snake_case variants; zero-match queries retry as fuzzy and surface the best approximate hits.
- Git-aware annotations. Modified, untracked, and staged files are tagged so the agent reaches for what you are actively changing.

Source: [`crates/fff-mcp/`](./crates/fff-mcp/).

</details>

The MCP server gives any agent a file search tool that is faster and more token-efficient than the built-in one.

<details id="pi-extension">
<summary>
<h2>Pi agent extension</h2>
</summary>

### Install

```bash
pi install npm:@ff-labs/pi-fff
```

### Modes

Three operating modes, switchable at runtime with `/fff-mode`:

| Mode                     | What it does                                                                      |
| ------------------------ | --------------------------------------------------------------------------------- |
| `tools-and-ui` (default) | Adds `ffgrep` and `fffind` tools, replaces `@`-mention autocomplete with FFF.     |
| `tools-only`             | Only tool injection. Keeps pi's native editor autocomplete.                       |
| `override`               | Replaces pi's built-in `grep`, `find`, and `multi_grep` with FFF implementations. |

Env vars: `PI_FFF_MODE`, `FFF_FRECENCY_DB`, `FFF_HISTORY_DB`. Flags: `--fff-mode`, `--fff-frecency-db`, `--fff-history-db`.

### Agent-facing tools

- `ffgrep`. Content search. Accepts `path`, `exclude` (comma, space, or array; leading `!` optional), `caseSensitive`, `context`, and cursor pagination. Auto-detects regex, falls back to fuzzy on zero exact matches, rejects `.*`-style wildcard-only patterns up front.
- `fffind`. Path and filename search. Matches the whole repo-relative path, not just the filename. Frecency-aware. The weak-match detector flags scattered fuzzy noise before it floods the agent's context.

### Commands

- `/fff-mode [tools-and-ui | tools-only | override]`. Show or switch the mode.
- `/fff-health`. Picker, frecency, and git integration status.
- `/fff-rescan`. Force a rescan.

Source: [`packages/pi-fff/`](./packages/pi-fff/).

</details>

The Pi extension swaps pi's native tools for FFF implementations and feeds the interactive editor's `@`-mention autocomplete from the frecency-ranked index.

<details id="neovim-plugin">
<summary>
<h2>fff.nvim</h2>
</summary>

Demo on the Linux kernel repo (100k files, 8GB):

https://github.com/user-attachments/assets/5d0e1ce9-642c-4c44-aa88-01b05bb86abb

### Installation

#### lazy.nvim

```lua
{
  'dmtrKovalenko/fff.nvim',
  build = function()
    -- downloads a prebuilt binary or falls back to cargo build
    require("fff.download").download_or_build_binary()
  end,
  -- for nixos:
  -- build = "nix run .#release",
  opts = {
    debug = {
      enabled = true,
      show_scores = true,
    },
  },
  lazy = false, -- the plugin lazy-initialises itself
  keys = {
    { "ff", function() require('fff').find_files() end, desc = 'FFFind files' },
    { "fg", function() require('fff').live_grep() end, desc = 'LiFFFe grep' },
    { "fz",
      function() require('fff').live_grep({ grep = { modes = { 'fuzzy', 'plain' } } }) end,
      desc = 'Live fffuzy grep',
    },
    { "fc",
      function() require('fff').live_grep({ query = vim.fn.expand("<cword>") }) end,
      desc = 'Search current word',
    },
  },
}
```

#### vim.pack

```lua
vim.pack.add({ 'https://github.com/dmtrKovalenko/fff.nvim' })

vim.api.nvim_create_autocmd('PackChanged', {
  callback = function(ev)
    local name, kind = ev.data.spec.name, ev.data.kind
    if name == 'fff.nvim' and (kind == 'install' or kind == 'update') then
      if not ev.data.active then vim.cmd.packadd('fff.nvim') end
      require('fff.download').download_or_build_binary()
    end
  end,
})

vim.g.fff = {
  lazy_sync = true,
  debug = { enabled = true, show_scores = true },
}

vim.keymap.set('n', 'ff', function() require('fff').find_files() end, { desc = 'FFFind files' })
```

### Public API

```lua
require('fff').find_files()                        -- find files in current repo
require('fff').live_grep()                         -- live content grep
require('fff').scan_files()                        -- force rescan
require('fff').refresh_git_status()                -- refresh git status
require('fff').find_files_in_dir(path)             -- find in a specific dir
require('fff').change_indexing_directory(new_path) -- change root

-- Programmatic search (no UI). Useful for plugin integrations.
require('fff').file_search(query, opts)            -- fuzzy search files / dirs / mixed
require('fff').content_search(query, opts)         -- programmatic grep
```

#### `file_search(query, opts)`

Returns a structured result `{ items, scores, total_matched, total_files?, total_dirs?, location? }`. Each item has a `type` field (`"file"` or `"directory"`) and `name` / `relative_path`. File items also expose `size`, `modified`, `git_status`, `is_binary`, and frecency scores.

```lua
local r = require('fff').file_search('button', {
  mode             = 'mixed',  -- 'files' (default) | 'directories' | 'mixed'
  max_results      = 50,
  page             = 0,        -- 0-based pagination
  current_file     = nil,      -- path to deprioritize for distance scoring
  max_threads      = 4,
  cwd              = nil,      -- switch indexed root if different (see below)
  wait_for_index_ms = nil,     -- override the default scan wait timeout
})
for _, item in ipairs(r.items) do
  print(item.type, item.relative_path)
end
```

#### `content_search(query, opts)`

Returns a `GrepResult` `{ items, total_matched, total_files_searched, total_files, filtered_file_count, next_file_offset, regex_fallback_error? }`. Each match item has `relative_path`, `name`, `line_number`, `col`, `line_content`, `match_ranges`, plus the same file metadata as `file_search`.

```lua
local r = require('fff').content_search('TODO', {
  mode                  = 'plain',  -- 'plain' (default) | 'regex' | 'fuzzy'
  max_file_size         = 10 * 1024 * 1024,
  max_matches_per_file  = 100,
  smart_case            = true,
  page_size             = 50,
  file_offset           = 0,
  time_budget_ms        = 0,
  trim_whitespace       = false,
  cwd                   = nil,      -- switch indexed root if different
  wait_for_index_ms     = nil,      -- override the default scan wait timeout
})
for _, m in ipairs(r.items) do
  print(string.format('%s:%d %s', m.relative_path, m.line_number, m.line_content))
end
```

Both functions accept the same constraint syntax as the UI pickers (e.g. `git:modified`, `*.rs`, `!test/`, glob patterns).

#### `cwd` and indexing

Both `file_search` and `content_search` honour an optional `cwd` field. The first call to either function lazily initialises the picker at `config.base_path` (your Neovim cwd by default).

- If `cwd` matches the currently indexed root, the call returns immediately against the existing index.
- If `cwd` differs, the picker is re-indexed at the new root and the call **blocks** (default up to 10 s) until the new picker is installed and its initial scan completes — so callers always get results from the right tree.
- If the index is still warming up after a `change_indexing_directory`, you can pass `wait_for_index_ms = N` to block for up to `N` ms regardless of whether `cwd` triggered the swap. Pass `0` to skip waiting entirely (useful for fire-and-forget calls where partial results are acceptable).
- Invalid or non-existent `cwd` paths return an empty result and emit an error via `vim.notify`.

### Commands

- `:FFFScan`. Rescan files.
- `:FFFRefreshGit`. Refresh git status.
- `:FFFClearCache [all|frecency|files]`. Clear caches.
- `:FFFHealth`. Health check.
- `:FFFDebug [on|off|toggle]`. Toggle the scoring display.
- `:FFFOpenLog`. Open `~/.local/state/nvim/log/fff.log`.

### Configuration

Defaults are sensible. Override only what you care about.

```lua
require('fff').setup({
  base_path = vim.fn.getcwd(),
  prompt = '> ',
  title = 'FFFiles',
  max_results = 100,
  max_threads = 4,
  lazy_sync = true,
  prompt_vim_mode = false,
  layout = {
    height = 0.8,
    width = 0.8,
    prompt_position = 'bottom',   -- or 'top'
    preview_position = 'right',   -- 'left' | 'right' | 'top' | 'bottom'
    preview_size = 0.5,
    flex = { size = 130, wrap = 'top' },
    min_list_height = 10, --  do not display anything except the list below this threshold
    show_scrollbar = true,
    path_shorten_strategy = 'middle_number', -- 'middle_number' | 'middle' | 'end' | 'start'
    anchor = 'center',
  },
  preview = {
    enabled = true,
    max_size = 10 * 1024 * 1024,
    chunk_size = 8192,
    binary_file_threshold = 1024,
    imagemagick_info_format_str = '%m: %wx%h, %[colorspace], %q-bit',
    line_numbers = false,
    cursorlineopt = 'both',
    wrap_lines = false,
    filetypes = {
      svg = { wrap_lines = true },
      markdown = { wrap_lines = true },
      text = { wrap_lines = true },
    },
  },
  keymaps = {
    close = '<Esc>',
    select = '<CR>',
    select_split = '<C-s>',
    select_vsplit = '<C-v>',
    select_tab = '<C-t>',
    move_up = { '<Up>', '<C-p>' },
    move_down = { '<Down>', '<C-n>' },
    preview_scroll_up = '<C-u>',
    preview_scroll_down = '<C-d>',
    toggle_debug = '<F2>',
    cycle_grep_modes = '<S-Tab>',
    cycle_previous_query = '<C-Up>',
    toggle_select = '<Tab>',
    send_to_quickfix = '<C-q>',
    focus_list = '<leader>l',
    focus_preview = '<leader>p',
  },
  frecency = {
    enabled = true,
    db_path = vim.fn.stdpath('cache') .. '/fff_nvim',
  },
  history = {
    enabled = true,
    db_path = vim.fn.stdpath('data') .. '/fff_queries',
    min_combo_count = 3,
    combo_boost_score_multiplier = 100,
  },
  git = {
    status_text_color = false, -- true to color filenames by git status
  },
  grep = {
    max_file_size = 10 * 1024 * 1024,
    max_matches_per_file = 100,
    smart_case = true,
    time_budget_ms = 150,
    modes = { 'plain', 'regex', 'fuzzy' },
    trim_whitespace = false,
    location_format = ':%d:%d', -- printf format for line:col prefix in grep results, e.g. ':%d' for line-only
  },
  debug = {
    enabled = false, -- show the file info panel next to the preview
    show_scores = false, -- inline scores in the file list
    -- Per-section toggles for the file info panel. Accepts a boolean shorthand
    -- (`show_file_info = true|false`) to flip everything at once. The panel
    -- adapts to width: narrow renders sections vertically, wide renders them
    -- as a two-column grid. Disable a section to also shrink the panel.
    show_file_info = {
      file_info = true, -- size, type, git status, frecency
      score_breakdown = true, -- total + match type, bonuses, modifiers, penalty
      -- modified + accessed timestamps; pass a table to hide individual rows:
      --   timings = { modified = false, accessed = true }
      timings = true,
      full_path = true, -- relative path at the bottom (wraps if too long)
    },
  },
  logging = {
    enabled = true,
    log_file = vim.fn.stdpath('log') .. '/fff.log',
    log_level = 'info',
  },
})
```

### Live grep modes

`<S-Tab>` cycles between `plain`, `regex`, and `fuzzy`. The list is configurable via `grep.modes`, and single-mode setups hide the indicator entirely.

Per-call override:

```lua
require('fff').live_grep({ grep = { modes = { 'fuzzy', 'plain' } } })
require('fff').live_grep({ query = 'search term' }) -- pre-fill
```

### Constraints

Both find and grep accept these tokens to refine a query:

- `git:modified`. One of `modified`, `staged`, `deleted`, `renamed`, `untracked`, `ignored`.
- `test/`. Any deeply nested children of `test/`.
- `!something`, `!test/`, `!git:modified`. Exclusion.
- `./**/*.{rs,lua}`. Any valid glob, powered by [zlob](https://github.com/dmtrKovalenko/zlob).

Grep-only:

- `*.md`, `*.{c,h}`. Extension filter.
- `src/main.rs`. Grep inside a single file.

Mix freely: `git:modified src/**/*.rs !src/**/mod.rs user controller`.

### Multi-select and quickfix

- `<Tab>`. Toggle selection (shows a thick `▊` in the signcolumn).
- `<C-q>`. Send selected files to the quickfix list and close the picker.

### Git status highlighting

Sign-column indicators are on by default. To color filename text by git status, set `git.status_text_color = true` and adjust the `hl.git_*` groups. See `:help fff.nvim` for the full list.

### Float colors

The picker maps its float content to `NormalFloat` (via `hl.normal`) and the border to `FloatBorder`. Default `FloatBorder` links to `NormalFloat`, so border and content share a background out of the box and the picker reads as a single popup. Override `hl.normal = 'Normal'` to make the picker blend with the editor instead.

For finer control, set `hl.winhl` to override the per-window `winhighlight`. It accepts either a single string applied to every picker window, or a table with optional `prompt`, `list`, `preview`, and `file_info` keys. Missing keys fall back to the default built from `hl.normal`, `hl.border`, and `hl.title`.

```lua
-- Apply the same winhighlight to all picker windows
hl = { winhl = 'Normal:NormalFloat,FloatBorder:FloatBorder,FloatTitle:Title' }

-- Or override specific windows only
hl = {
  winhl = {
    prompt  = 'Normal:Pmenu,FloatBorder:FloatBorder',
    list    = 'Normal:NormalFloat,FloatBorder:FloatBorder',
    preview = 'Normal:NormalFloat,FloatBorder:FloatBorder',
  },
}
```

### File info panel

Enable with `debug.enabled = true`. The panel sits above the preview and shows
file metadata, score breakdown, timestamps and the full absolute path. It
adapts to the panel width: at narrow widths sections stack vertically (B2),
at wide widths sections render as a two-column grid (H2). Each section can be
disabled individually via `debug.show_file_info`.

Customise the panel via `hl`:

| key                          | default              | used for                            |
| ---------------------------- | -------------------- | ----------------------------------- |
| `file_info_section`          | `Title`              | section header label                |
| `file_info_separator`        | `FloatBorder`        | dashes that act as section borders  |
| `file_info_label`            | `Comment`            | row labels (Size, Type, Git, ...)   |
| `file_info_value`            | `Normal` fg          | plain values                        |
| `file_info_value_dim`        | `NonText`            | dim values, separators inside rows  |
| `file_info_size`             | `Number`             | file size value                     |
| `file_info_type`             | `Type`               | filetype value                      |
| `file_info_path`             | `Directory`          | full path                           |
| `file_info_total_score`      | bold + `Number`      | total score (bold)                  |
| `file_info_match_type`       | bold + `Special`     | match type (bold)                   |
| `file_info_score_pos`        | `DiagnosticOk`       | positive score components           |
| `file_info_score_neg`        | `DiagnosticError`    | negative score components           |

### File filtering

FFF honours `.gitignore`. For picker-only ignores that do not touch git, add a sibling `.ignore` file:

```gitignore
*.md
docs/archive/**/*.md
```

Run `:FFFScan` to force a rescan.

### Troubleshooting

- `:FFFHealth` verifies picker init, optional dependencies, and DB connectivity.
- `:FFFOpenLog` opens the log file.

</details>

The best file search picker for neovim. Period. Faster and more intuitive queries, frecency ranking, definition classification and much more.

<details id="node-sdk">
<summary>
<h2>Node & Bun SDK</h2>
</summary>

```bash
npm install @ff-labs/fff-node
# or
bun add @ff-labs/fff-node
```

```ts
import { FileFinder } from "@ff-labs/fff-node";

const finder = FileFinder.create({ basePath: process.cwd(), aiMode: true });
if (!finder.ok) throw new Error(finder.error);
await finder.value.waitForScan(10_000);

const files = finder.value.fileSearch("incognito profile", { pageSize: 20 });
const hits = finder.value.grep("GetOffTheRecordProfile", {
  mode: "plain",
  smartCase: true,
  beforeContext: 1,
  afterContext: 1,
  classifyDefinitions: true,
});

finder.value.destroy();
```

Every method returns a `Result<T>` (`{ ok: true, value } | { ok: false, error }`). Full type reference: [`packages/fff-node/src/types.ts`](./packages/fff-node/src/types.ts).

</details>

TypeScript wrapper over the C library for nodejs and bun. Build custom agent tools, CLIs, or IDE integrations on top of FFF.

<details id="rust-crate">
<summary>
<h2>Rust crate</h2>
</summary>

### Add the dependency

FFF is written in Rust, so this is the lowest-overhead way to use it.

```toml
[dependencies]
fff-search = "0.6"
```

Full API documentation: [docs.rs/fff-search](https://docs.rs/fff-search/latest/fff_search/).

</details>

Native rust crate that is performing all the search. Stable and well documented.

<details id="c-library">
<summary>
<h2>C library</h2>
</summary>

### Build

```bash
# Builds only the C cdylib (fastest):
make build-c-lib

# or directly with cargo:
cargo build --release -p fff-c --features zlob
```

The output is a `cdylib` (`libfff_c.so` / `libfff_c.dylib` / `fff_c.dll`). The header lives at [`crates/fff-c/include/fff.h`](./crates/fff-c/include/fff.h).

Prebuilt binaries for every version, including every commit on main, are on the [releases page](https://github.com/dmtrKovalenko/fff.nvim/releases). The same binaries also ship inside the `@ff-labs/fff-bin-*` npm packages.

### Install

```bash
# System-wide (needs sudo):
sudo make install

# User-local, no sudo:
make install PREFIX=$HOME/.local

# Staged install for packagers:
make install DESTDIR=/tmp/pkgroot PREFIX=/usr
```

Drops `libfff_c.{so,dylib,dll}` into `$(PREFIX)/lib` and the header into `$(PREFIX)/include/fff.h`. Remove with `make uninstall`, which honours the same `PREFIX` and `DESTDIR`.

Link against it after install:

```bash
cc my_app.c -lfff_c -o my_app
```

Ensure `$(PREFIX)/lib` is on your runtime library search path (`LD_LIBRARY_PATH` on Linux, `DYLD_LIBRARY_PATH` on macOS, or an entry in `/etc/ld.so.conf.d/`).

### Minimal example

```c
#include <fff.h>
#include <stdio.h>

int main(void) {
    FffResult *res = fff_create_instance(
        ".",        // base_path
        "",         // frecency_db_path (empty = default)
        "",         // history_db_path
        false,      // use_unsafe_no_lock
        true,       // enable_mmap_cache
        true,       // enable_content_indexing
        true,       // watch
        false       // ai_mode
    );
    if (!res->success) {
        fprintf(stderr, "init failed: %s\n", res->error);
        fff_free_result(res);
        return 1;
    }
    void *handle = res->handle;
    fff_free_result(res);

    // Search
    FffResult *search = fff_search(handle, "main.rs", "", 0, 0, 20, 100, 3);
    // ... read FffSearchResult from search->handle, then fff_free_search_result()

    fff_destroy(handle);
    return 0;
}
```

### Notes

- Every function returning `FffResult*` allocates with Rust's `Box`. Free with `fff_free_result`, do not use malloc's free
- Payloads (search results, grep results, scan progress) have their own dedicated free functions listed in the header.
- C strings returned in the `handle` field (e.g. from `fff_get_base_path`) are freed with `fff_free_string`.

Source: [`crates/fff-c/`](./crates/fff-c/).

</details>

Stable C ABI. Bind from C/C++, Zig, Go via cgo, Python via ctypes, or anything with C FFI.

---

## What is FFF and why use it over ripgrep or fzf?

FFF 是一个文件搜索库，而非 CLI 工具。Ripgrep 和 fzf 是优秀的工具，但它们是命令行程序：每次调用都会 fork 新进程、重新读取 `.gitignore`、重新统计目录，并在内存中重建所需状态才能返回结果。从 shell 执行一次 grep 时这没问题。但当编辑器或 AI Agent 希望在单次会话中运行数百次搜索时，这就成了性能瓶颈。

FFF 将索引和文件缓存驻留在一个长期运行的进程中，并通过四个轻量级层暴露相同的 Rust 核心：原生 crate（`fff-search`）、C 库（`libfff_c`）、Node/Bun SDK（`@ff-labs/fff-node`）以及 MCP 服务器。你只需调用一次 `FileFinder.create()`，后续每次搜索都会命中已预热的内存。在包含 50 万个文件的 Chromium 代码库中，这意味着 ripgrep 每次启动需要 3-9 **秒**，而 FFF 查询仅需不到 10 **毫秒**。

模糊匹配算法比 fzf 的算法更全面，具备**防错拼写（Typo-resistant）**能力。我们提供带有额外约束解析的查询语言用于预过滤，例如 `"*.rs !test/ shcema"` 对 FFF 是完全合法的查询；但即使 "shcema" 只有一个字母打错，fzf 也找不到任何结果。

### Why a programmatic API matters

- **无进程创建开销**。每次调用均驻留在进程中，避免了短生命周期 `rg` 调用中主导性能的 fork、exec、argv 解析和 stdout 管道建立过程。
- **单次文件系统遍历与 `.gitignore` 解析**。忽略规则 walker 仅在扫描时运行一次，结果将在后续所有搜索中被复用。
- **返回类型化对象而非文本**。SDK 直接提供 `{ relativePath, lineNumber, lineContent, gitStatus, totalFrecencyScore, isDefinition, ... }`，无需二次解析。
- **跨调用持久化的光标分页（Cursor pagination）**。Ripgrep 没有“这些匹配结果的第 2 页”的概念；FFF 有。
- **长期运行进程可启用一次性 CLI 无法实现的优化**：预热缓存、增量重索引、跨查询 Frecency 共享以及 SIMD 状态复用。

### What the core actually does

- **基于 Frecency（近期频率）排名的模糊匹配**。每个已索引文件都带有访问分数和修改分数。搜索会将你最近且频繁打开的文件排在冷数据之前。这与 VS Code 的“最近打开”列表理念相同，但应用于每次搜索结果而不仅是侧边栏。
- **路径与内容的防错拼写匹配**。Grep 路径提供 Smith-Waterman 模糊评分；路径搜索使用 SIMD 加速的模糊匹配（基于 [`frizbee`](https://github.com/saghen/frizbee) 衍生核心），可容忍字符丢失和顺序打乱。
- **支持三种模式的 Content grep**。纯文本字面量（SIMD memmem）、正则表达式（Rust `regex` crate）以及模糊搜索（逐行 Smith-Waterman）。自动根据模式检测使用哪种方式，当纯文本搜索返回零结果时回退为模糊匹配。
- **多模式 OR 搜索**。基于 SIMD Aho-Corasick 算法实现“一次性查找这 20 个标识符中的任意一个”，比正则表达式交替匹配更快，远快于执行 20 次独立的 ripgrep。
- **后台文件监听器（Background file watcher）**。索引随文件变更实时更新。你永远不会在热路径上为重新扫描付费。
- **Git 状态感知**。已修改、已暂存、未跟踪和忽略的状态会被缓存并随每次结果返回，调用方可直接排序或过滤而无需 shell 调用 git。监听器直接与 libgit2 通信而非 fork `git` CLI。
- **定义分类器（Definition classifier）**。Rust 端的字节级扫描器会对以 `struct`、`fn`、`class`、`def`、`impl` 等开头的行进行标记。

### Performance choices that matter

- 高效的内存分配器与策略（见下文）。默认使用 `mimaloc`
- 并行多线程搜索流水线，不受编排逻辑干扰
- 全面采用 SIMD 优先算法。高效且无分配的排序机制
- 平台特定的文件系统优化（Linux 的 [getdents64](https://linux.die.net/man/2/getdents64)、Windows NTFS API 等）
- 轻量级实时内容索引，支持防错拼写 grep
- 内存映射内容缓存。将部分文件存储在虚拟内存中（数量有限制）
- 字符串块的单连续区域存储（Single contiguous arena）。显著减少内存操作开销并大幅提升 CPU 缓存命中率

### Memory allocation

是的，FFF 在底层确实比单次调用子进程需要更多内存。这正是其性能优势的主要来源。在实际使用中，作为 Neovim 最受欢迎的文件搜索选择器之一，[fff 的内存占用实际上低于 ripgrep 的突发调用](https://x.com/neogoose_btw/status/2041606853155811442)。

FFF 还会维护一个内容索引，每个已索引文件约占用 360 字节，因此对于 10 万文件的仓库大约为 36 MB。并非所有文件都会被索引——二进制文件、超大文件以及不适合 grep 的内容会被跳过。如果连这个 footprint 对你来说仍然过大，索引也可通过内存映射文件（memory-mapped file）而非匿名 RAM 来支持。

### What this means in practice

如果你正在构建 Agent、IDE 扩展、pre-commit 检查器或任何需要多次搜索同一仓库的长期运行工具，以库的形式调用 FFF 比 shell 调用 ripgrep 成本低得多。代价是真实的内存占用：FFF 将索引保留在 RAM 中并预热内容缓存。对于包含 1.4 万文件的仓库，驻留内存约为 26 MB。对于像 Chromium 这样包含 50 万文件的仓库，预计需要几百 MB。作为交换，每次搜索都会附带 Git 状态、Frecency 排名、文件元数据、最后访问和编辑时间戳等丰富信息。

如果你只是从终端执行一次 grep，`rg` 仍然是合适的选择。如果你在同一个进程中运行数十次搜索，FFF 将在第二次调用时收回成本。如果你是 AI Agent 开发者，FFF 会在你的 AI 有机会调用它之前就完成准备工作。

### How it compares

- **ripgrep**：FFF 使用相同的底层正则引擎及更先进的纯文本匹配算法。维护内容索引与文件树。在重复搜索场景下优势明显。但在“从 bash 执行一次 grep 并退出”的场景下不占优。
- **fzf**：FFF 的路径搜索同样支持模糊匹配，但额外具备 Frecency 感知和 Git 感知能力，且提供更宽容的错拼算法。fzf 是纯粹的匹配过滤工具；FFF 会根据你实际打开文件的频率对结果进行排名。
- **Telescope / fzf-lua / snacks.picker**：FFF 自带 Neovim 选择器，使用与 MCP 服务器和 SDK 相同的排序逻辑。该选择器为可选组件；核心库保持一致。
- **Tantivy 或其他全文搜索引擎**：属于不同类别的工具。Tantivy 针对大规模查询时评分对文档进行索引。FFF 限定于单一仓库范围，并优化至亚 10 毫秒响应。它不会将倒排索引持久化到磁盘。

---

## Repository layout

- `crates/fff-search`, `crates/fff-grep`, `crates/fff-query-parser` - Rust core.
- `crates/fff-c` - C FFI used by every language binding.
- `crates/fff-nvim` - Lua/mlua bindings for the Neovim plugin.
- `crates/fff-mcp` - MCP server binary.
- `packages/fff-node` - Node.js SDK (`@ff-labs/fff-node`).
- `packages/fff-bun` - Bun SDK (`@ff-labs/fff-node`).
- `packages/pi-fff` - pi extension (`@ff-labs/pi-fff`).
- `lua/` - Neovim-side plugin code.

## Contributing

Bug reports and pull requests welcome. Agentic coding tools are welcome to be used, but human review is mandatory.

## License

[MIT](./LICENSE) & open source forever.