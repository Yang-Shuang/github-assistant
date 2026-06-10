<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1775033787/readme-sandcastle-ondark_2x.png">
    <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1775033787/readme-sandcastle-onlight_2x.png">
    <img alt="Sandcastle" src="https://res.cloudinary.com/total-typescript/image/upload/v1775033787/readme-sandcastle-onlight_2x.png" height="200" style="margin-bottom: 20px;">
  </picture>
</div>

## Sandcastle 是什么？

一个用于在隔离沙箱中编排 AI 编程代理的 TypeScript 库：

1. 你通过单个 `sandcastle.run()` 调用代理。
2. Sandcastle 负责使用可配置的分支策略对代理进行沙箱化隔离。
3. 在分支上提交的更改会被合并回来。

Sandcastle 与提供商无关——它内置了 Docker、Podman 和 Vercel 的提供商支持，你也可以创建自己的提供商。非常适合并行处理多个 AFK（Away From Keyboard）代理、创建审查流水线，或者仅仅是编排你自己的代理。

## 前置条件

- [Git](https://git-scm.com/)
- 一个沙箱提供商 —— Sandcastle 需要一个隔离的环境来运行代理。内置选项：
  - [Docker Desktop](https://www.docker.com/) — 本地开发中最常用
  - [Podman](https://podman.io/) — Docker 的无根替代方案
  - [Vercel](https://vercel.com/) — 基于云的 Firecracker microVMs，通过 `@vercel/sandbox` 提供
  - 或者使用 `createBindMountSandboxProvider` 或 `createIsolatedSandboxProvider` [创建你自己的提供商](#custom-sandbox-providers)

## 快速开始

1. 安装该包：

```bash
npm install --save-dev @ai-hero/sandcastle
```

2. 运行 `npx @ai-hero/sandcastle init`。这将生成一个 `.sandcastle` 目录，其中包含所有必要的文件。

```bash
npx @ai-hero/sandcastle init
```

3. 编辑 `.sandcastle/.env` 并填写你的默认值 `ANTHROPIC_API_KEY`。如果你想使用 Claude 订阅而不是 API key，请参阅 [#191](https://github.com/mattpocock/sandcastle/issues/191)。

```bash
cp .sandcastle/.env.example .sandcastle/.env
```

4. 使用 `npx tsx` 运行 `.sandcastle/main.ts`（或 `main.mts`）文件。

```bash
npx tsx .sandcastle/main.ts
```

```typescript
// 3. Run the agent via the JS API
import { run, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(), // or podman(), vercel(), or your own provider
  promptFile: ".sandcastle/prompt.md",
});
```

## 沙箱提供商 (Sandbox Providers)

Sandcastle 使用 `SandboxProvider` 来创建隔离环境。`run()`、`interactive()` 和 `createSandbox()` 上的 `sandbox` 选项接受任何提供商，包括 `noSandbox()` —— 当不需要容器隔离时，选择直接在主机上运行代理。内置提供商：

| Provider   | Import path                                | Type       | Accepted by                                 |
| ---------- | ------------------------------------------ | ---------- | ------------------------------------------- |
| Docker     | `@ai-hero/sandcastle/sandboxes/docker`     | Bind-mount | `run()`, `createSandbox()`, `interactive()` |
| Podman     | `@ai-hero/sandcastle/sandboxes/podman`     | Bind-mount | `run()`, `createSandbox()`, `interactive()` |
| Vercel     | `@ai-hero/sandcastle/sandboxes/vercel`     | Isolated   | `run()`, `createSandbox()`, `interactive()` |
| No-sandbox | `@ai-hero/sandcastle/sandboxes/no-sandbox` | None       | `run()`, `createSandbox()`, `interactive()` |

Worktree 方法 (`wt.run()`, `wt.interactive()`, `wt.createSandbox()`) 接受与顶层对应项相同的提供商。当未指定沙箱时，`wt.interactive()` 默认为 `noSandbox()`。

```typescript
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";
import { podman } from "@ai-hero/sandcastle/sandboxes/podman";
import { vercel } from "@ai-hero/sandcastle/sandboxes/vercel";
import { noSandbox } from "@ai-hero/sandcastle/sandboxes/no-sandbox";

// Docker, Podman 和 Vercel 在 run() 和 createSandbox() 中是可互换的：
await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  prompt: "...",
});

// No-sandbox 直接在主机上运行代理 —— 接受于 run()、
// createSandbox() 和 interactive()。完全跳过容器隔离：
await interactive({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: noSandbox(),
  prompt: "...", // 可选 — 省略以启动不带初始提示的 TUI
  cwd: "/path/to/other-repo", // 可选 — 默认为 process.cwd()
});
```

你也可以使用 `createBindMountSandboxProvider` 或 `createIsolatedSandboxProvider` [创建你自己的提供商](#custom-sandbox-providers)。

## API

Sandcastle 导出了一个编程式 `run()` 函数，用于在脚本、CI 流水线或自定义工具中使用。下面的示例使用了 `docker()`，但任何 `SandboxProvider` 都可以替代使用。

```typescript
import { run, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

const result = await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  promptFile: ".sandcastle/prompt.md",
});

console.log(result.iterations.length); // number of iterations executed
console.log(result.iterations); // per-iteration results with optional sessionId
console.log(result.commits); // array of { sha } for commits created
console.log(result.branch); // target branch name
```

### 所有选项 (All options)

```typescript
import { run, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

const result = await run({
  // Agent provider — required. Pass a model string to claudeCode().
  // Optional second arg for provider-specific options like effort level.
  agent: claudeCode("claude-opus-4-7", { effort: "high" }),

  // Sandbox provider — required. Any SandboxProvider works (docker, podman, vercel, or custom).
  // Provider-specific config (like imageName, mounts) lives inside the provider factory call.
  sandbox: docker({
    imageName: "sandcastle:local",
    // Optional: override the UID/GID used for --user flag (defaults to host UID/GID).
    // Must match the UID baked into the image. Pre-flight check catches mismatches.
    // containerUid: 1000,
    // containerGid: 1000,
    // Optional: mount host directories into the sandbox (e.g. package manager caches)
    // hostPath supports absolute, tilde-expanded (~), and relative paths (resolved from cwd).
    // sandboxPath supports absolute and relative paths (resolved from the sandbox repo directory).
    mounts: [
      { hostPath: "~/.npm", sandboxPath: "/home/agent/.npm", readonly: true },
      { hostPath: "data", sandboxPath: "data" }, // mounts <cwd>/data → <sandbox-repo>/data
    ],
    // Optional: SELinux volume label — "z" (default, shared), "Z" (private), or false (none).
    // No-op on non-SELinux systems (Docker Desktop on macOS/Windows, Linux without SELinux).
    selinuxLabel: "z",
    // Optional: provider-level env vars merged at launch time
    env: { DOCKER_SPECIFIC: "value" },
    // Optional: attach container to Docker network(s) — string or string[]
    network: "my-network",
    // Optional: add the container user to supplementary groups via --group-add.
    // Accepts group names or numeric GIDs (e.g. for a bind-mounted Docker socket).
    groups: ["docker", 999],
    // Optional: expose host devices via --device. Each entry is a full device
    // spec in host[:container[:permissions]] form (e.g. "/dev/kvm").
    devices: ["/dev/kvm"],
    // Optional: limit CPU resources via --cpus. Fractional values allowed (e.g. 1.5).
    // cpus: 2,
  }),

  // Host repo directory — replaces process.cwd() as the anchor for
  // .sandcastle/ artifacts (worktrees, logs, env, patches) and git operations.
  // Relative paths resolve against process.cwd(). Defaults to process.cwd().
  cwd: "../other-repo",

  // Branch strategy — controls how the agent's changes relate to branches.
  // Defaults to { type: "head" } for bind-mount and { type: "merge-to-head" } for isolated providers.
  branchStrategy: { type: "branch", branch: "agent/fix-42" },

  // Prompt source — provide one of these, not both.
  // Note: promptFile resolves against process.cwd(), NOT cwd.
  promptFile: ".sandcastle/prompt.md", // path to a prompt file
  // prompt: "Fix issue #42 in this repo", // OR an inline prompt string

  // Values substituted for {{KEY}} placeholders in the prompt.
  promptArgs: {
    ISSUE_NUMBER: "42",
  },

  // Maximum number of agent iterations to run before stopping. Default: 1
  maxIterations: 5,

  // Display name for this run, shown as a prefix in log output.
  name: "fix-issue-42",

  // Lifecycle hooks grouped by where they run: host or sandbox.
  hooks: {
    host: {
      onWorktreeReady: [{ command: "cp .env.example .env" }],
      onSandboxReady: [{ command: "echo setup done" }],
    },
    sandbox: {
      onSandboxReady: [{ command: "npm install" }],
    },
  },

  // Host-relative file paths to copy into the sandbox before the container starts.
  // Not supported with branchStrategy: { type: "head" }.
  copyToWorktree: [".env"],

  // Override default timeouts for built-in lifecycle steps.
  // Unset keys keep their defaults.
  timeouts: {
    copyToWorktreeMs: 120_000, // default: 60_000
    gitSetupMs: 30_000, // default: 10_000
    commitCollectionMs: 60_000, // default: 30_000
    mergeToHostMs: 60_000, // default: 30_000
  },

  // How to record progress. Default: write to a file under .sandcastle/logs/
  logging: {
    type: "file",
    path: ".sandcastle/logs/my-run.log",
    // Optional: forward the agent's output stream to your own observability system.
    // Fires for each text chunk and tool call the agent produces. Errors thrown
    // by the callback are swallowed so a broken forwarder cannot kill the run.
    onAgentStreamEvent: (event) => {
      // event is { type: "text" | "toolCall", iteration, timestamp, ... }
      myLogger.info(event);
    },
  },
  // logging: { type: "stdout" }, // OR render an interactive UI in the terminal

  // String (or array of strings) the agent emits to end the iteration loop early.
  // Default: "<promise>COMPLETE</promise>"
  completionSignal: "<promise>COMPLETE</promise>",

  // Idle timeout in seconds — resets whenever the agent produces output. Default: 600 (10 minutes)
  idleTimeoutSeconds: 600,

  // Grace window in seconds after the agent emits a completion signal but
  // before its process has exited (a "hanging process" — typically a spawned
  // `gh`/git child or MCP server keeping stdout open). Resets on every
  // subsequent output line so trailing data is still captured. Default: 60
  completionTimeoutSeconds: 60,

  // Structured output — extract a typed payload from the agent's stdout.
  // Requires maxIterations === 1 and the tag must appear in the prompt.
  // output: Output.object({ tag: "result", schema: z.object({ answer: z.number() }) }),
  // output: Output.string({ tag: "summary" }),
});

console.log(result.iterations.length); // number of iterations executed
console.log(result.completionSignal); // matched signal string, or undefined if none fired
console.log(result.commits); // array of { sha } for commits created
console.log(result.branch); // target branch name
```

### `createSandbox()` —— 可复用的沙箱

当你需要在单个沙箱中运行多个代理（或同一代理的多个轮次）时，使用 `createSandbox()`。它只创建一次沙箱，你可以按需多次调用 `sandbox.run()`。这避免了重复启动容器的开销，并使所有运行都在同一个分支上。

如果你只需要单次一次性调用，请改用 `run()` —— 它会自动处理沙箱的生命周期。

#### 基本单次运行用法

```typescript
import { createSandbox, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

await using sandbox = await createSandbox({
  branch: "agent/fix-42",
  sandbox: docker(),
});

const result = await sandbox.run({
  agent: claudeCode("claude-opus-4-7"),
  prompt: "Fix issue #42 in this repo.",
});

console.log(result.commits); // [{ sha: "abc123" }]
```

#### 多轮次实现然后审查 (Multi-run implement-then-review)

```typescript
import { createSandbox, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

await using sandbox = await createSandbox({
  branch: "agent/fix-42",
  sandbox: docker(),
  hooks: { sandbox: { onSandboxReady: [{ command: "npm install" }] } },
});

// Step 1: implement
const implResult = await sandbox.run({
  agent: claudeCode("claude-opus-4-7"),
  promptFile: ".sandcastle/implement.md",
  maxIterations: 5,
});

// Step 2: review on the same branch, same container
const reviewResult = await sandbox.run({
  agent: claudeCode("claude-sonnet-4-6"),
  prompt: "Review the changes and fix any issues.",
});
```

所有 `run()` 调用的提交都会累积在同一个分支上。沙箱容器在运行之间保持存活，因此安装的依赖项和构建产物会保留下来。

#### 使用 `await using` 进行自动清理

当代码块退出时，`await using` 会自动调用 `sandbox.close()`。如果沙箱有未提交的更改，worktree 会在磁盘上保留；如果是干净的，则容器和 worktree 都会被移除。

#### 手动 `close()` 与 `CloseResult`

```typescript
const sandbox = await createSandbox({
  branch: "agent/fix-42",
  sandbox: docker(),
});
// ... run agents ...
const closeResult = await sandbox.close();
if (closeResult.preservedWorktreePath) {
  console.log(`Worktree preserved at ${closeResult.preservedWorktreePath}`);
}
```

#### `CreateSandboxOptions`

| Option           | Type            | Default         | Description                                                                                                         |
| ---------------- | --------------- | --------------- | ------------------------------------------------------------------------------------------------------------------- |
| `branch`         | string          | —               | **必填。** 沙箱的显式分支                                                                                           |
| `sandbox`        | SandboxProvider | —               | **必填。** 沙箱提供商（例如 `docker()`，`podman()`）                                                                |
| `cwd`            | string          | `process.cwd()` | 主机仓库目录 —— 相对路径相对于 `process.cwd()` 解析                                                                  |
| `hooks`          | SandboxHooks    | —               | 生命周期钩子 (`host.*`, `sandbox.*`) —— 在创建时运行一次                                                              |
| `copyToWorktree` | string[]        | —               | 在创建时将主机相对文件路径复制到沙箱中                                                                               |
| `timeouts`       | Timeouts        | —               | 覆盖内置生命周期步骤的超时时间 (`copyToWorktreeMs`, `gitSetupMs`, `commitCollectionMs`, `mergeToHostMs`)             |

#### `Sandbox`

| Property / Method       | Type                                                               | Description                                  |
| ----------------------- | ------------------------------------------------------------------ | -------------------------------------------- |
| `branch`                | string                                                             | 沙箱所在的分支                               |
| `worktreePath`          | string                                                             | Worktree 的主机路径                          |
| `run(options)`          | `(SandboxRunOptions) => Promise<SandboxRunResult>`                 | 在现有沙箱中调用代理                         |
| `interactive(options)`  | `(SandboxInteractiveOptions) => Promise<SandboxInteractiveResult>` | 在沙箱中启动交互式会话                       |
| `close()`               | `() => Promise<CloseResult>`                                       | 销毁容器和沙箱                               |
| `[Symbol.asyncDispose]` | `() => Promise<void>`                                              | 通过 `await using` 自动销毁                  |

#### `SandboxRunOptions`

| Option                     | Type               | Default                       | Description                                                                          |
| -------------------------- | ------------------ | ----------------------------- | ------------------------------------------------------------------------------------ |
| `agent`                    | AgentProvider      | —                             | **必填。** 代理提供商（例如 `claudeCode("claude-opus-4-7")`)                         |
| `prompt`                   | string             | —                             | 内联提示词（与 `promptFile` 互斥）                                                   |
| `promptFile`               | string             | —                             | 提示词文件路径（与 `prompt` 互斥）                                                   |
| `promptArgs`               | PromptArgs         | —                             | 用于 `{{KEY}}` 占位符替换的键值映射                                                  |
| `maxIterations`            | number             | `1`                           | 运行的最大迭代次数                                                                   |
| `completionSignal`         | string \| string[] | `<promise>COMPLETE</promise>` | 代理发出以提前停止迭代循环的字符串                                                   |
| `idleTimeoutSeconds`       | number             | `600`                         | 空闲超时时间（秒） —— 每次代理输出事件时重置                                         |
| `completionTimeoutSeconds` | number             | `60`                          | 看到完成信号但代理进程尚未退出后的宽限窗口                                           |
| `name`                     | string             | —                             | 运行的显示名称                                                                       |
| `logging`                  | object             | file (auto-generated)         | `{ type: 'file', path }` 或 `{ type: 'stdout' }`                                    |
| `signal`                   | AbortSignal        | —                             | 中止时取消运行；句柄在之后仍可使用                                                   |

#### `SandboxRunResult`

| Field              | Type                | Description                                                        |
| ------------------ | ------------------- | ------------------------------------------------------------------ |
| `iterations`       | `IterationResult[]` | 每次迭代的结果（使用 `.length` 获取计数）                          |
| `completionSignal` | string?             | 匹配的完成信号字符串，如果未触发则为 `undefined`                   |
| `stdout`           | string              | 所有迭代的合并代理输出                                             |
| `commits`          | `{ sha }[]`         | 运行期间创建的提交                                                 |
| `logFilePath`      | string?             | 日志文件路径（仅在记录到文件时）                                   |

#### `CloseResult`

| Field                   | Type    | Description                                                              |
| ----------------------- | ------- | ------------------------------------------------------------------------ |
| `preservedWorktreePath` | string? | 保留的 worktree 的主机路径，当存在未提交的更改时设置                     |

### `createWorktree()` —— 独立的 worktree 生命周期

当你需要一个作为独立、一等公民概念的 worktree（git worktree）——与任何沙箱分离时使用。这适用于你想先运行交互式会话，然后将同一个 worktree 交给一个离线的 AFK 代理的情况。

只接受 `branch` 和 `merge-to-head` 策略；`head` 是编译时类型错误，因为它意味着没有 worktree。

传递 `cwd` 以指向除 `process.cwd()` 之外的其他仓库。相对路径相对于 `process.cwd()` 解析；绝对路径直接通过。如果路径不存在或不是目录，将抛出 `CwdError`。

```typescript
import { createWorktree } from "@ai-hero/sandcastle";

await using wt = await createWorktree({
  branchStrategy: { type: "branch", branch: "agent/fix-42" },
  copyToWorktree: ["node_modules"],
  cwd: "/path/to/other-repo", // optional — defaults to process.cwd()
});

console.log(wt.worktreePath); // host path to the worktree
console.log(wt.branch); // "agent/fix-42"

// Run an interactive session in the worktree (defaults to noSandbox)
await wt.interactive({
  agent: claudeCode("claude-opus-4-7"),
  prompt: "Explore the codebase and understand the bug.",
});

// Run an AFK agent in the worktree (sandbox is required)
const result = await wt.run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker({ imageName: "sandcastle:myrepo" }),
  prompt: "Fix issue #42.",
  maxIterations: 3,
});
console.log(result.commits); // commits made during the run

// Create a long-lived sandbox from the worktree
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

await using sandbox = await wt.createSandbox({
  sandbox: docker(),
  hooks: { sandbox: { onSandboxReady: [{ command: "npm install" }] } },
});

// sandbox.close() tears down the container only — the worktree stays
await sandbox.close();

// wt.close() cleans up the worktree
```

`wt.close()` 检查是否有未提交的更改：如果 worktree 是脏的（有修改），它会在磁盘上保留；如果是干净的，则会被移除。`await using` 会自动调用 `close()`。Worktree 在 `run()`、`interactive()` 和 `createSandbox()` 完成后会持续存在，因此你可以将其交给另一个代理或进行检查。

**所有权分离**：当通过 `wt.createSandbox()` 创建沙箱时，`sandbox.close()` 仅销毁容器 —— worktree 保持不变。`wt.close()` 负责清理 worktree。这与顶层的 `createSandbox()` 不同，在后者中，`sandbox.close()` 拥有对容器和 worktree 的所有权。

#### `CreateWorktreeOptions`

| Option           | Type                   | Default | Description                                                                                                         |
| ---------------- | ---------------------- | ------- | ------------------------------------------------------------------------------------------------------------------- |
| `branchStrategy` | WorktreeBranchStrategy | —       | **必填。** `{ type: "branch", branch }` 或 `{ type: "merge-to-head" }`                                              |
| `copyToWorktree` | string[]               | —       | 在创建时将主机相对文件路径复制到 worktree 中                                                                        |
| `timeouts`       | Timeouts               | —       | 覆盖内置生命周期步骤的超时时间 (`copyToWorktreeMs`, `gitSetupMs`, `commitCollectionMs`, `mergeToHostMs`)            |

#### `Worktree`

| Property / Method        | Type                                                                  | Description                                         |
| ------------------------ | --------------------------------------------------------------------- | --------------------------------------------------- |
| `branch`                 | string                                                                | Worktree 所在的分支                                 |
| `worktreePath`           | string                                                                | Worktree 的主机路径                                 |
| `run(options)`           | `(options: WorktreeRunOptions) => Promise<WorktreeRunResult>`         | 在 worktree 中运行 AFK 代理（需要沙箱）             |
| `interactive(options)`   | `(options: WorktreeInteractiveOptions) => Promise<InteractiveResult>` | 在 worktree 中运行交互式代理会话                    |
| `createSandbox(options)` | `(options: WorktreeCreateSandboxOptions) => Promise<Sandbox>`         | 基于此 worktree 创建一个长期存在的沙箱              |
| `close()`                | `() => Promise<CloseResult>`                                          | 清理 worktree（如果是脏的则保留）                   |
| `[Symbol.asyncDispose]`  | `() => Promise<void>`                                                 | 通过 `await using` 自动清理                         |

#### `WorktreeInteractiveOptions`

| Option       | Type                   | Default       | Description                                                                                       |
| ------------ | ---------------------- | ------------- | ------------------------------------------------------------------------------------------------- |
| `agent`      | AgentProvider          | —             | **必填。** 代理提供商                                                                             |
| `sandbox`    | AnySandboxProvider     | `noSandbox()` | 沙箱提供商（默认为无沙箱）                                                                        |
| `prompt`     | string                 | —             | 内联提示词（与 `promptFile` 互斥）                                                                |
| `promptFile` | string                 | —             | 提示词文件路径                                                                                    |
| `name`       | string                 | —             | 可选的会话名称                                                                                    |
| `hooks`      | SandboxHooks           | —             | 生命周期钩子 (`host.*`, `sandbox.*`)                                                              |
| `promptArgs` | PromptArgs             | —             | 用于 `{{KEY}}` 占位符替换的键值映射                                                               |
| `env`        | Record<string, string> | —             | 注入到沙箱中的环境变量                                                                            |
| `signal`     | AbortSignal            | —             | 中止时取消会话。Worktree 会在磁盘上保留。使用 `signal.reason` 拒绝。                                |

#### `WorktreeRunOptions`

| Option                     | Type                   | Default | Description                                                                                                                          |
| -------------------------- | ---------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `agent`                    | AgentProvider          | —       | **必填。** 代理提供商                                                                                                                |
| `sandbox`                  | SandboxProvider        | —       | **必填。** 沙箱提供商（AFK 代理必须进行沙箱化）                                                                                        |
| `prompt`                   | string                 | —       | 内联提示词（与 `promptFile` 互斥）                                                                                                   |
| `promptFile`               | string                 | —       | 提示词文件路径                                                                                                                       |
| `maxIterations`            | number                 | 1       | 运行的最大迭代次数                                                                                                                   |
| `completionSignal`         | string \| string[]     | —       | 用于提前停止迭代循环的子字符串                                                                                                       |
| `idleTimeoutSeconds`       | number                 | 600     | 空闲超时时间（秒）                                                                                                                   |
| `completionTimeoutSeconds` | number                 | 60      | 看到完成信号但代理进程尚未退出后的宽限窗口                                                                                           |
| `name`                     | string                 | —       | 可选的运行名称                                                                                                                       |
| `logging`                  | LoggingOption          | file    | 日志模式                                                                                                                             |
| `hooks`                    | SandboxHooks           | —       | 生命周期钩子 (`host.*`, `sandbox.*`)                                                                                                 |
| `promptArgs`               | PromptArgs             | —       | 用于 `{{KEY}}` 占位符替换的键值映射                                                                                                  |
| `env`                      | Record<string, string> | —       | 注入到沙箱中的环境变量                                                                                                               |
| `resumeSession`            | string                 | —       | 通过 ID 恢复之前的会话（针对支持恢复的代理）。与 `maxIterations > 1` 不兼容。主机上必须存在会话文件。                                |
| `signal`                   | AbortSignal            | —       | 中止时取消运行。杀死正在进行的代理子进程；worktree 会在磁盘上保留。使用 `signal.reason` 拒绝。                                        |

#### `WorktreeRunResult`

| Property           | Type                | Description                                            |
| ------------------ | ------------------- | ------------------------------------------------------ |
| `iterations`       | `IterationResult[]` | 每次迭代的结果（使用 `.length` 获取计数）              |
| `completionSignal` | string              | 匹配的完成信号，或 undefined                           |
| `stdout`           | string              | 所有代理迭代的合并 stdout 输出                         |
| `commits`          | { sha: string }[]   | 运行期间代理做出的提交列表                             |
| `branch`           | string              | 代理工作的分支名称                                     |
| `logFilePath`      | string              | 日志文件路径（如果记录到了文件中）                     |

#### `WorktreeCreateSandboxOptions`

| Option           | Type            | Default | Description                                                                                                         |
| ---------------- | --------------- | ------- | ------------------------------------------------------------------------------------------------------------------- |
| `sandbox`        | SandboxProvider | —       | **必填。** 沙箱提供商（例如 `docker()`）                                                                            |
| `hooks`          | SandboxHooks    | —       | 生命周期钩子 (`host.*`, `sandbox.*`)                                                                                |
| `copyToWorktree` | string[]        | —       | 在创建时将主机相对文件路径复制到 worktree 中                                                                        |
| `timeouts`       | Timeouts        | —       | 覆盖内置生命周期步骤的超时时间 (`copyToWorktreeMs`, `gitSetupMs`, `commitCollectionMs`, `mergeToHostMs`)            |

## 工作原理 (How it works)

Sandcastle 使用沙箱提供商上配置的**分支策略**来控制代理的更改与分支的关系。有三种策略：

- **Head** (`{ type: "head" }`) —— 代理直接写入主机工作目录。没有 worktree，没有分支间接层。这是 `docker()` 等绑定挂载提供商的默认设置。
- **Merge-to-head** (`{ type: "merge-to-head" }`) —— Sandcastle 在 git worktree 中创建一个临时分支。代理在该临时分支上工作，完成后更改会被合并回 HEAD。合并后清理临时分支。
- **Branch** (`{ type: "branch", branch: "foo" }`) —— 提交落在 git worktree 中的显式命名分支上。使用相同的分支重新运行会重用现有的 worktree，并在安全时从 `origin` 快进它 —— 参见 [ADR 0003](docs/adr/0003-reuse-worktree-by-default.md)。

对于绑定挂载提供商（如 Docker），worktree 目录会被绑定挂载到容器中 —— 代理通过挂载直接写入主机文件系统，因此不需要同步。

从你的角度来看，你只需在 `run()` 上配置 `branchStrategy: { type: 'branch', branch: 'foo' }`，完成后就会得到一个分支 `foo` 上的提交。全部 100% 本地化。

## 提示词 (Prompts)

Sandcastle 使用灵活的提示词系统。你编写提示词，引擎执行它 —— 不施加关于工作流、任务管理或上下文来源的任何意见。

### 提示词解析

你必须提供以下之一：

1. `prompt: "inline string"` — 通过 `RunOptions` 直接传递内联提示词
2. `promptFile: "./path/to/prompt.md"` — 通过 `RunOptions` 指向特定文件

`prompt` 和 `promptFile` 是互斥的 —— 同时提供两者是错误的。如果未提供其中任何一个，`run()` 会抛出错误要求你提供一个。

**内联提示词 (`prompt: "..."`) 是直接传递给代理的。** 没有 `{{KEY}}` 替换，没有 `` !`command` `` 扩展，也没有内置的 `{{SOURCE_BRANCH}}` / `{{TARGET_BRANCH}}` 注入。如果你需要将值插入到内联提示词中，请在 JavaScript 中构建字符串（`` `Work on ${branch}…` ``）。在内联提示词旁传递 `promptArgs` 是错误的 —— 切换到 `promptFile` 以使用替换功能。

下面提到的替换和扩展功能**仅适用于**源自 `promptFile` 的提示词。

> **约定**：`sandcastle init` 会生成 `.sandcastle/prompt.md`，所有模板都通过 `promptFile: ".sandcastle/prompt.md"` 显式引用它。这只是一个约定，不是自动回退 —— 除非你将 `.sandcastle/prompt.md` 作为 `promptFile` 传递，否则 Sandcastle 不会读取它。

### 使用 `` !`command` `` 进行动态上下文

在你的提示词中使用 `` !`command` `` 表达式来拉取动态上下文。每个表达式在将提示词发送给代理之前都会被替换为命令的 stdout。提示词中的所有表达式**并行运行**以实现更快的扩展。

命令在 `sandbox.onSandboxReady` 钩子完成后，在沙箱内部运行，因此它们看到的仓库状态与代理看到的一样（包括已安装的依赖项）。

```markdown
# Open issues

!`gh issue list --state open --label Sandcastle --json number,title,body,comments,labels --limit 100`

# Recent commits

!`git log --oneline -10`
```

如果任何命令以非零代码退出，运行将立即失败并报错。

### 使用 `{{KEY}}` 的提示词参数

在你的提示词中使用 `{{KEY}}` 占位符来注入来自 `promptArgs` 选项的值。这对于在具有不同参数的多次运行中重用相同的提示词文件非常有用。

```typescript
import { run } from "@ai-hero/sandcastle";

await run({
  promptFile: "./my-prompt.md",
  promptArgs: { ISSUE_NUMBER: 42, PRIORITY: "high" },
});
```

在提示词文件中：

```markdown
Work on issue #{{ISSUE_NUMBER}} (priority: {{PRIORITY}}).
```

提示词参数替换在 shell 表达式扩展之前在主机关上运行，因此 `` !`command` `` 表达式内的 `{{KEY}}` 占位符会首先被替换：

```markdown
!`gh issue view {{ISSUE_NUMBER}} --json body -q .body`
```

没有匹配提示词参数的 `{{KEY}}` 占位符是一个错误。未使用的提示词参数会产生警告。

`` !`command` `` 扩展仅在提示词文件本身中编写的 shell 块上运行。任何出现在参数值内的 `` !`…` `` 模式都被视为惰性文本 —— 它不会针对主机 shell 执行。这使得通过 `promptArgs` 传递用户编写的内容（问题标题、PR 描述、文档摘录）变得安全。

### 内置提示词参数

Sandcastle 会自动向每个提示词注入两个内置提示词参数：

| Placeholder         | Value                                                             |
| ------------------- | ----------------------------------------------------------------- |
| `{{SOURCE_BRANCH}}` | 代理工作的分支（由分支策略决定）                                    |
| `{{TARGET_BRANCH}}` | `run()` 时主机上的活动分支                                        |

在你的提示词中使用它们，无需通过 `promptArgs` 传递：

```markdown
You are working on {{SOURCE_BRANCH}}. When diffing, compare against {{TARGET_BRANCH}}.
```

在 `promptArgs` 中传递 `SOURCE_BRANCH` 或 `TARGET_BRANCH` 是一个错误 —— 内置提示词参数不能被覆盖。

### 使用 `<promise>COMPLETE</promise>` 提前终止

当代理输出 `<promise>COMPLETE</promise>` 时，编排器会提前停止迭代循环。这是你在提示词中记录给代理遵循的一种约定 —— 引擎从不注入它。

这对于基于任务的工作流非常有用，即代理在完成时应停止运行，而不是运行所有剩余的迭代。

你可以通过向 `run()` 传递 `completionSignal` 来覆盖默认信号。它接受单个字符串或字符串数组：

```ts
await run({
  // ...
  completionSignal: "DONE",
});

// Or pass multiple signals — the loop stops on the first match:
await run({
  // ...
  completionSignal: ["TASK_COMPLETE", "TASK_ABORTED"],
});
```

在提示词中告诉代理输出你选择的字符串，编排器检测到其中任何一个时都会停止。匹配的信号将作为 `result.completionSignal` 返回。

#### 完成信号后的挂起进程 (Hanging processes)

代理进程预计会在发出完成信号后不久退出。当它派生的子进程 —— 一个 `gh`/git 子进程、一个长期存在的 MCP 服务器等 —— 继承了代理的 stdout 管道并保持其打开状态时，父进程可能会在其逻辑结束之后徘徊很久。否则 Sandcastle 会等待完整的 `idleTimeoutSeconds` 并以 `AgentIdleTimeoutError` 失败，从而丢弃代理已经做出的提交。

相反，一旦在输出缓冲区中观察到完成信号，Sandcastle 就会切换到一个短的**完成超时**（默认 60 秒）。当它过期时，运行将成功解决并发出进程挂起的警告；`result.commits` 和 `result.completionSignal` 将被填充，就像进程已干净退出一样。计时器会在随后的每一行输出上重置，因此信号后发出的尾随数据 —— token 使用事件、终端 `result` 事件、结构化输出 `<tag>` —— 仍会被捕获。

干净的进程退出总是赢得比赛，所以健康的运行不会增加额外的延迟。完成超时仅在进程挂起时才重要。

使用 `completionTimeoutSeconds` 调整窗口：

```ts
await run({
  // ...
  completionTimeoutSeconds: 30, // shorter grace window
});
```

这独立于 `idleTimeoutSeconds`。它们覆盖不同的阶段：`idleTimeoutSeconds` 在**看到任何信号之前**运行（真正卡住的代理 -> 失败）；`completionTimeoutSeconds` 在**看到信号后**运行（挂起的进程 -> 成功并发出警告）。参见 [ADR 0019](docs/adr/0019-completion-timeout-for-hanging-process.md)。

### 结构化输出 (Structured output)

使用 `Output.object()` 从代理的 stdout 中提取类型化、模式验证的 JSON 负载。代理在你指定的 XML 标签内发出其答案，Sandcastle 解析、验证并在 `result.output` 上返回它。该模式可以是任何 [Standard Schema](https://standardschema.dev) 验证器 —— 下面的示例使用 [Zod](https://zod.dev)，但 Valibot、ArkType 和其他库的工作方式完全相同。参见 [ADR 0010](docs/adr/0010-structured-output.md) 了解设计原理。

```ts
import { run, Output, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";
import { z } from "zod";

const result = await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  prompt: `Analyze the code, and output the result as JSON inside <result> tags.
    The result must match this schema:
    { summary: string; score: string }
  `,
  output: Output.object({
    tag: "result",
    schema: z.object({ summary: z.string(), score: z.number() }),
  }),
});

console.log(result.output.summary); // typed as string
console.log(result.output.score); // typed as number
```

`Output.string({ tag })` 将标签内容提取为纯字符串（已修剪，无 JSON 解析）。这两个助手都要求 `maxIterations` 为 `1`（默认值）。解析后的提示词必须包含配置的打开标签字面量。

当提取或验证失败时，`run()` 会抛出 `StructuredOutputError`。除了 `tag`、`rawMatched`、`cause`、`commits`、`branch` 和 `preservedWorktreePath` 之外，该错误还携带产生不良输出的运行的 `sessionId`（以及捕获会话时的 `sessionFilePath`）。你可以恢复该会话以要求代理重新发出更正后的输出，而无需重复工作：

```ts
import { run, Output, StructuredOutputError } from "@ai-hero/sandcastle";

try {
  return await run({ ...opts, output });
} catch (e) {
  if (e instanceof StructuredOutputError && e.sessionId) {
    return await run({
      ...opts,
      output,
      resumeSession: e.sessionId,
      prompt: `Your previous output failed: ${e.message}. Re-emit it inside <${e.tag}> tags.`,
    });
  }
  throw e;
}
```

### 模板 (Templates)

`sandcastle init` 会提示你选择沙箱提供商（Docker 或 Podman）、问题跟踪器（GitHub Issues、Beads 或 Custom）和模板，这将生成一个现成的提示词和 `main.mts`，适用于特定的工作流。如果你的项目的 `package.json` 有 `"type": "module"`，文件名将改为 `main.ts`。选择 **Custom** 将以故意未配置的状态生成项目，以及一个 `.sandcastle/SETUP_ISSUE_TRACKER.md` 提示词，你将其喂给你的编码代理，它将通过就地编辑生成的文件来设置你自己的跟踪器。有五种模板可用：

| Template                       | Description                                                               |
| ------------------------------ | ------------------------------------------------------------------------- |
| `blank`                        | 裸骨架 —— 编写你自己的提示词和编排                                        |
| `simple-loop`                  | 逐个选择并关闭问题                                                        |
| `sequential-reviewer`          | 逐个实现问题，每个问题后都有一个代码审查步骤                                |
| `parallel-planner`             | 规划可并行处理的问题，在单独的分支上执行，然后合并                          |
| `parallel-planner-with-review` | 规划可并行处理的问题，在每个分支上进行审查后执行，然后合并                  |

当提示时选择模板进行 `sandcastle init`，或者在新仓库中重新运行 init 以尝试不同的模板。

## CLI 命令

### `sandcastle init`

生成 `.sandcastle/` 配置目录并构建容器镜像。这是你在一个新仓库中运行的第一个命令。在初始化期间你选择一个沙箱提供商（Docker 或 Podman）—— 选择 Podman 会写入 `Containerfile` 而不是 `Dockerfile`，并在构建步骤中使用 `sandcastle podman build-image`。

Init 从 `packageManager` 字段或锁文件中检测你的主机包管理器（npm、pnpm、yarn 或 bun），默认为 npm。其 `main` 文件导入主机依赖项的模板 —— 规划器模板为它们的 `<plan>` 输出模式导入了 [Zod](https://zod.dev) —— 如果它尚未在你的 `package.json` 中，则会提示你使用该包管理器安装它，因此第一次运行 `npx tsx .sandcastle/main.ts` 不会因 `ERR_MODULE_NOT_FOUND` 而失败。

每个交互式提示都有一个配对的 `--flag`，以便整个 init 可以非交互方式运行（例如在 CI 或脚本化设置中）。当 stdin 不是 TTY 且缺少必需的 flag 时，init 会快速失败并显示清晰的错误信息，而不是卡在提示上。

| Option                    | Required | Default                      | Description                                                                                                    |
| ------------------------- | -------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `--image-name`            | No       | `sandcastle:<repo-dir-name>` | Docker 镜像名称                                                                                                |
| `--agent`                 | No       | Interactive prompt           | 要使用的代理 (`claude-code`, `pi`, `codex`, `cursor`, `opencode`, `copilot`)                                   |
| `--model`                 | No       | Agent's default model        | 要使用的模型（例如 `claude-sonnet-4-6`）。默认为代理的默认值                                                   |
| `--sandbox`               | No       | Interactive prompt           | 要使用的沙箱提供商 (`docker`, `podman`)                                                                        |
| `--template`              | No       | Interactive prompt           | 要生成的模板（例如 `blank`, `simple-loop`）                                                                    |
| `--issue-tracker`         | No       | Interactive prompt           | 要使用的问题跟踪器 (`github-issues`, `beads`, `custom`)                                                        |
| `--create-label`          | No       | Interactive prompt           | `true` / `false` —— 是否创建 `Sandcastle` GitHub label（仅与 `--issue-tracker github-issues`）                |
| `--build-image`           | No       | Interactive prompt           | `true` / `false` —— 是否现在构建沙箱镜像（使用 `--issue-tracker custom` 时静默忽略）                           |
| `--install-template-deps` | No       | Interactive prompt           | `true` / `false` —— 是否安装模板主机依赖项（例如规划器模板的 `zod`）                                           |

创建以下文件：

```
.sandcastle/
├── Dockerfile      # Sandbox environment (customize as needed)
├── prompt.md       # Agent instructions
├── .env.example    # Token placeholders
└── .gitignore      # Ignores .env, logs/
```

如果 `.sandcastle/` 已存在则报错，以防止覆盖自定义设置。

### `sandcastle docker build-image`

从现有的 `.sandcastle/` 目录重建 Docker 镜像。在修改 Dockerfile 后使用此命令。在 Linux/macOS 上，构建会自动传递 `--build-arg AGENT_UID=$(id -u)` 和 `AGENT_GID=$(id -g)`，以便图像的 `agent` 用户与主机 UID 匹配 —— 这防止了图像构建文件的权限错误，而无需运行时 chown。

| Option         | Required | Default                      | Description                                                                       |
| -------------- | -------- | ---------------------------- | --------------------------------------------------------------------------------- |
| `--image-name` | No       | `sandcastle:<repo-dir-name>` | Docker 镜像名称                                                                   |
| `--dockerfile` | No       | —                            | 自定义 Dockerfile 的路径（构建上下文将是当前工作目录）                              |

### `sandcastle docker remove-image`

移除 Docker 镜像。

| Option         | Required | Default                      | Description       |
| -------------- | -------- | ---------------------------- | ----------------- |
| `--image-name` | No       | `sandcastle:<repo-dir-name>` | Docker 镜像名称   |

### `sandcastle podman build-image`

从现有的 `.sandcastle/` 目录构建 Podman 镜像。在修改 Containerfile 后使用此命令。

| Option            | Required | Default                      | Description                                                                          |
| ----------------- | -------- | ---------------------------- | ------------------------------------------------------------------------------------ |
| `--image-name`    | No       | `sandcastle:<repo-dir-name>` | Podman 镜像名称                                                                      |
| `--containerfile` | No       | —                            | 自定义 Containerfile 的路径（构建上下文将是当前工作目录）                              |

### `sandcastle podman remove-image`

移除 Podman 镜像。

| Option         | Required | Default                      | Description       |
| -------------- | -------- | ---------------------------- | ----------------- |
| `--image-name` | No       | `sandcastle:<repo-dir-name>` | Podman 镜像名称   |

### `RunOptions`

| Option                     | Type               | Default                       | Description                                                                                                                                                                                                                  |
| -------------------------- | ------------------ | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `agent`                    | AgentProvider      | —                             | **必填。** 代理提供商（例如 `claudeCode("claude-opus-4-7")`, `pi("claude-sonnet-4-6")`, `codex("gpt-5.4-mini")`, `cursor("composer-2")`, `opencode("opencode/big-pickle")`, `copilot("claude-sonnet-4.5")`)           |
| `sandbox`                  | SandboxProvider    | —                             | **必填。** 沙箱提供商（例如 `docker()`, `podman()`, `docker({ imageName: "sandcastle:local" })`)                                                                                                                    |
| `cwd`                      | string             | `process.cwd()`               | 主机仓库目录 —— `.sandcastle/` 工件和 git 操作的锚点。相对路径相对于 `process.cwd()` 解析。                                                                                                |
| `prompt`                   | string             | —                             | 内联提示词（与 `promptFile` 互斥）                                                                                                                                                                         |
| `promptFile`               | string             | —                             | 提示词文件路径（与 `prompt` 互斥）。相对于 `process.cwd()` 解析，**不是** `cwd`。                                                                                                                     |
| `maxIterations`            | number             | `1`                           | 运行的最大迭代次数                                                                                                                                                                                                    |
| `hooks`                    | SandboxHooks       | —                             | 生命周期钩子 (`host.*`, `sandbox.*`)                                                                                                                                                                                      |
| `name`                     | string             | —                             | 运行的显示名称，在日志输出中作为前缀显示                                                                                                                                                                    |
| `promptArgs`               | PromptArgs         | —                             | 用于 `{{KEY}}` 占位符替换的键值映射                                                                                                                                                                         |
| `branchStrategy`           | BranchStrategy     | per-provider default          | 分支策略：`{ type: 'head' }`, `{ type: 'merge-to-head' }`, 或 `{ type: 'branch', branch: '…' }`                                                                                                                       |
| `copyToWorktree`           | string[]           | —                             | 启动前复制到沙箱中的主机相对文件路径（不支持与 `branchStrategy: { type: 'head' }`）                                                                                                       |
| `logging`                  | object             | file (auto-generated)         | `{ type: 'file', path }` 或 `{ type: 'stdout' }`                                                                                                                                                                             |
| `completionSignal`         | string \| string[] | `<promise>COMPLETE</promise>` | 代理发出以提前停止迭代循环的字符串或字符串数组                                                                                                                                                  |
| `idleTimeoutSeconds`       | number             | `600`                         | 空闲超时时间（秒） —— 每次代理输出事件时重置                                                                                                                                                                  |
| `completionTimeoutSeconds` | number             | `60`                          | 观察到完成信号但代理进程尚未退出后的宽限窗口（挂起进程）。参见 [完成信号后的挂起进程](#hanging-processes-after-the-completion-signal)。 |
| `resumeSession`            | string             | —                             | 通过 ID 恢复之前的会话（针对支持恢复的代理）。与 `maxIterations > 1` 不兼容。主机上必须存在会话文件。                                                                                         |
| `signal`                   | AbortSignal        | —                             | 中止时取消运行。杀死正在进行的代理子进程并取消生命周期钩子；worktree 会在磁盘上保留。使用 `signal.reason` 拒绝。                                                              |
| `timeouts`                 | Timeouts           | —                             | 覆盖内置生命周期步骤的默认超时时间：`copyToWorktreeMs` (60,000), `gitSetupMs` (10,000), `commitCollectionMs` (30,000), `mergeToHostMs` (30,000)。                                                         |
| `output`                   | OutputDefinition   | —                             | 结构化输出定义 (`Output.object(…)` 或 `Output.string(…)`)。需要 `maxIterations === 1`。参见 [结构化输出](#structured-output)。                                                                        |

### `RunResult`

| Field              | Type                | Description                                                        |
| ------------------ | ------------------- | ------------------------------------------------------------------ |
| `iterations`       | `IterationResult[]` | 每次迭代的结果（使用 `.length` 获取计数）                          |
| `completionSignal` | string?             | 匹配的完成信号字符串，如果未触发则为 `undefined`                   |
| `stdout`           | string              | 代理输出                                                           |
| `commits`          | `{ sha }[]`         | 运行期间创建的提交                                                 |
| `branch`           | string              | 目标分支名称                                                       |
| `logFilePath`      | string?             | 日志文件路径（仅在记录到文件时）                                   |
| `output`           | T?                  | 类型化的结构化输出（仅当设置了 `output` 选项时存在）               |

### `IterationResult`

| Field             | Type              | Description                                                                                                                         |
| ----------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`       | string?           | 提供商流中的代理会话 ID，如果提供商不发出则为 `undefined`                                           |
| `sessionFilePath` | string?           | 捕获的会话 JSONL 的主机绝对路径，当关闭捕获时为 `undefined`                                                |
| `usage`           | `IterationUsage`? | 最后一条助手消息的 token 使用快照，当关闭捕获或提供商不支持使用时为 `undefined` |

### `IterationUsage`

| Field                      | Type   | Description                                |
| -------------------------- | ------ | ------------------------------------------ |
| `inputTokens`              | number | 消耗的输入 tokens                          |
| `cacheCreationInputTokens` | number | 用于创建提示缓存条目的 tokens              |
| `cacheReadInputTokens`     | number | 从提示缓存中读取的 tokens                  |
| `outputTokens`             | number | 生成的输出 tokens                          |

### 会话捕获 (Session capture)

在每次可恢复提供商迭代之后，Sandcastle 会自动将代理的会话文件从沙箱捕获到主机。Claude Code 会话存储在 `~/.claude/projects/<encoded-path>/<session-id>.jsonl` 下；Codex 会话存储在 `~/.codex/sessions/YYYY/MM/DD/rollout-*-<session-id>.jsonl` 下；Pi 会话存储在 `~/.pi/agent/sessions/--<encoded-cwd>--/<timestamp>_<session-id>.jsonl` 下。任何提供商特定的 `cwd` 字段都会被重写以匹配主机仓库根，以便提供商的原生恢复命令起作用。

默认情况下启用 `claudeCode()`、`codex()` 和 `pi()` 的会话捕获，可以通过 `captureSessions: false` 选择退出。没有 `sessionStorage` 的提供商不会尝试捕获。捕获失败会导致运行失败。

### 会话恢复 (Session resume)

向 `run()` 传递 `resumeSession` 以在新的沙箱中继续之前的 Claude Code、Codex 或 Pi 对话：

```typescript
const result = await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  prompt: "Continue where you left off",
  resumeSession: "abc-123-def",
});
```

你也可以从结果中继续最后捕获的会话：

```typescript
const first = await run({
  agent: codex("gpt-5.4-mini"),
  sandbox: docker(),
  prompt: "Draft a plan",
});

const second = await first.resume?.("Now implement the plan");
```

`resume` 仅存在于来自可恢复提供商（Claude Code、Codex、Pi）的结果上 —— 因此是可选链调用。

在沙箱启动之前，Sandcastle 验证会话文件是否存在于主机上，并使用重写的 `cwd` 字段将其传输到沙箱以匹配沙箱端路径。Claude Code 接收 `--resume <id>`；Codex 接收 `codex exec resume <id>` 并通过 stdin 管道传递提示词；Pi 接收 `--session <id>`。

约束：

- `resumeSession` 与 `maxIterations > 1` 不兼容（在沙箱创建之前抛出）。
- 提供商的主机会话文件必须存在（在沙箱创建之前抛出）。
- 只有第 1 次迭代接收恢复标志；后续迭代（如果有）从头开始。
- 不支持恢复的提供商拒绝 `resumeSession`。

### 会话分叉 (Session fork)

`RunResult.fork(prompt, options?)` 是 `.resume()` 的兄弟方法：它从最后捕获的会话继续，但保留父会话 JSONL 不变，并在新的会话 ID 下写入子会话。机制是代理的原生分叉标志 —— `claude --resume <id> --fork-session` 用于 Claude Code，`codex exec fork <id>` 用于 Codex。

Fork 启发了扇出工作流，其中单个父运行是几个独立子运行的起点：

```typescript
const parent = await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  prompt: "Read the codebase and summarise the data model",
});

const [reviewA, reviewB] = await Promise.all([
  parent.fork?.("Review the migration plan", {
    branchStrategy: { type: "branch", branch: "review-a" },
  }),
  parent.fork?.("Audit the auth layer", {
    branchStrategy: { type: "branch", branch: "review-b" },
  }),
]);
```

**Fork 仅针对会话。** `--fork-session` 和 `codex exec fork` 隔离代理会话 JSONL —— 它们**不**隔离分支、worktree 或沙箱。安全的并发扇出 (`Promise.all([r.fork(a), r.fork(b)])`) 要求调用者通过 `branchStrategy: { type: "branch", branch: "..." }` 为每个子项提供不同的 `branch`。默认的 `head` 和 `merge-to-head` 策略对于并发分叉**不安全**：`head` 在所有子项之间共享主机工作目录，而 `merge-to-head` 针对相同的 HEAD 竞争 `git merge`。参见 [ADR 0018](docs/adr/0018-fork-is-session-only.md)。

`fork` 仅存在于具有 `sessionStorage` 的提供商的结果上（Claude Code、Codex）—— 因此是可选链调用。与 `.resume()` 相同的单迭代和会话文件约束适用。

### `ClaudeCodeOptions`

`claudeCode()` 工厂接受一个可选的第二个参数用于提供商特定的选项：

```typescript
agent: claudeCode("claude-opus-4-7", { effort: "high" });
```

| Option            | Type                                                      | Default | Description                                               |
| ----------------- | --------------------------------------------------------- | ------- | --------------------------------------------------------- |
| `effort`          | `"low"` \| `"medium"` \| `"high"` \| `"xhigh"` \| `"max"` | —       | Claude Code 推理努力级别 (`max` 仅限 Opus)   |
| `env`             | `Record<string, string>`                                  | `{}`    | 此代理提供商注入的环境变量     |
| `captureSessions` | `boolean`                                                 | `true`  | 捕获代理会话 JSONL 到主机以用于 `claude --resume` |

### `CodexOptions`

`codex()` 工厂接受一个可选的第二个参数用于提供商特定的选项：

```typescript
agent: codex("gpt-5.4", { effort: "high" });
```

| Option            | Type                                           | Default | Description                                               |
| ----------------- | ---------------------------------------------- | ------- | --------------------------------------------------------- |
| `effort`          | `"low"` \| `"medium"` \| `"high"` \| `"xhigh"` | —       | 通过 `model_reasoning_effort` 的 Codex 推理努力级别 |
| `env`             | `Record<string, string>`                       | `{}`    | 此代理提供商注入的环境变量     |
| `captureSessions` | `boolean`                                      | `true`  | 捕获 Codex rollout JSONL 到主机以用于恢复            |

### `PiOptions`

`pi()` 工厂接受一个可选的第二个参数用于提供商特定的选项：

```typescript
agent: pi("claude-sonnet-4-6", { thinking: "high" });
```

| Option            | Type                                                                     | Default | Description                                              |
| ----------------- | ------------------------------------------------------------------------ | ------- | -------------------------------------------------------- |
| `thinking`        | `"off"` \| `"minimal"` \| `"low"` \| `"medium"` \| `"high"` \| `"xhigh"` | —       | 通过 `--thinking` flag 的 Pi 推理努力级别      |
| `env`             | `Record<string, string>`                                                 | `{}`    | 此代理提供商注入的环境变量     |
| `captureSessions` | `boolean`                                                                | `true`  | 捕获 pi 会话 JSONL 到主机以用于 `pi --session <id>` |

### 提供商 `env`

**代理提供商**和**沙箱提供商**都接受其选项中的可选 `env: Record<string, string>`。这些环境变量在启动时与 `.sandcastle/.env` 解析器输出合并：

```typescript
await run({
  agent: claudeCode("claude-opus-4-7", {
    env: { ANTHROPIC_API_KEY: "sk-ant-..." },
  }),
  sandbox: docker({
    env: { DOCKER_SPECIFIC_VAR: "value" },
  }),
  prompt: "Fix issue #42",
});
```

**合并规则：**

- 提供商环境（代理 + 沙箱）覆盖共享键的 `.sandcastle/.env` 解析器输出
- 代理提供商环境和沙箱提供商环境**不得重叠** —— 如果它们共享任何键，`run()` 将抛出错误
- 当未提供 `env` 时，默认为 `{}`

环境变量也从 `.sandcastle/.env` 和 `process.env` 自动解析 —— 无需将它们传递给 API。所需的变量取决于**代理提供商**（有关详细信息，参见 `sandcastle init` 输出）。

## 自定义沙箱提供商 (Custom Sandbox Providers)

Sandcastle 随附了 Docker、Podman 和 Vercel 的内置提供商，但你可以创建自己的提供商。沙箱提供商告诉 Sandcastle 如何在隔离环境中执行命令。有两种类型：

- **Bind-mount** —— 沙箱可以挂载主机目录。Sandcastle 在主机上创建一个 worktree，提供商将其挂载进去。不需要文件同步。用于 Docker、Podman 或任何本地容器运行时。
- **Isolated** —— 沙箱拥有自己的文件系统（例如云 VM）。提供商通过 `copyIn` 和 `copyFileOut` 处理代码的进出同步。当沙箱无法访问主机文件系统时使用此选项。

### 沙箱句柄契约 (The sandbox handle contract)

两种类型的提供商都从其 `create()` 函数返回一个**沙箱句柄**。该句柄公开：

| Method         | Required   | Description                                                                  |
| -------------- | ---------- | ---------------------------------------------------------------------------- |
| `exec`         | Both       | 运行命令，可选择通过 `options.onLine` 逐行流式传输 stdout |
| `close`        | Both       | 销毁沙箱                                                        |
| `copyFileIn`   | Bind-mount | 将单个文件从主机复制到沙箱中                            |
| `copyFileOut`  | Both       | 将单个文件从沙箱复制到主机                              |
| `copyIn`       | Isolated   | 将文件或目录从主机复制到沙箱                      |
| `worktreePath` | Both       | 沙箱内仓库目录的绝对路径                       |

### `ExecResult`

每个 `exec` 调用都返回一个 `ExecResult`：

```typescript
interface ExecResult {
  readonly stdout: string;
  readonly stderr: string;
  readonly exitCode: number;
}
```

### Bind-mount 提供商示例

一个最小化的绑定挂载提供商，外壳到本地进程（无容器）：

```typescript
import {
  createBindMountSandboxProvider,
  type BindMountCreateOptions,
  type BindMountSandboxHandle,
  type ExecResult,
} from "@ai-hero/sandcastle";
import { execFile, spawn } from "node:child_process";
import { copyFile as fsCopyFile, mkdir as fsMkdir } from "node:fs/promises";
import { dirname } from "node:path";
import { createInterface } from "node:readline";

const localProcess = () =>
  createBindMountSandboxProvider({
    name: "local-process",
    create: async (
      options: BindMountCreateOptions,
    ): Promise<BindMountSandboxHandle> => {
      const worktreePath = options.worktreePath;

      return {
        worktreePath,

        exec: (
          command: string,
          opts?: { onLine?: (line: string) => void; cwd?: string },
        ): Promise<ExecResult> => {
          if (opts?.onLine) {
            const onLine = opts.onLine;
            return new Promise((resolve, reject) => {
              const proc = spawn("sh", ["-c", command], {
                cwd: opts?.cwd ?? worktreePath,
                stdio: ["ignore", "pipe", "pipe"],
              });

              const stdoutChunks: string[] = [];
              const stderrChunks: string[] = [];

              const rl = createInterface({ input: proc.stdout! });
              rl.on("line", (line) => {
                stdoutChunks.push(line);
                onLine(line); // forward each line to Sandcastle
              });

              proc.stderr!.on("data", (chunk: Buffer) => {
                stderrChunks.push(chunk.toString());
              });

              proc.on("error", (err) => reject(err));
              proc.on("close", (code) => {
                resolve({
                  stdout: stdoutChunks.join("\n"),
                  stderr: stderrChunks.join(""),
                  exitCode: code ?? 0,
                });
              });
            });
          }

          return new Promise((resolve, reject) => {
            execFile(
              "sh",
              ["-c", command],
              { cwd: opts?.cwd ?? worktreePath, maxBuffer: 10 * 1024 * 1024 },
              (error, stdout, stderr) => {
                if (error && error.code === undefined) {
                  reject(new Error(`exec failed: ${error.message}`));
                } else {
                  resolve({
                    stdout: stdout.toString(),
                    stderr: stderr.toString(),
                    exitCode: typeof error?.code === "number" ? error.code : 0,
                  });
                }
              },
            );
          });
        },

        copyFileIn: async (hostPath: string, sandboxPath: string) => {
          await fsMkdir(dirname(sandboxPath), { recursive: true });
          await fsCopyFile(hostPath, sandboxPath);
        },

        copyFileOut: async (sandboxPath: string, hostPath: string) => {
          await fsMkdir(dirname(hostPath), { recursive: true });
          await fsCopyFile(sandboxPath, hostPath);
        },

        close: async () => {
          // nothing to tear down for a local process
        },
      };
    },
  });
```

### Isolated 提供商示例

一个使用临时目录的最小化隔离提供商：

```typescript
import {
  createIsolatedSandboxProvider,
  type IsolatedSandboxHandle,
  type ExecResult,
} from "@ai-hero/sandcastle";
import { execFile, spawn } from "node:child_process";
import { copyFile, mkdir, mkdtemp, rm } from "node:fs/promises";
import { tmpdir } from "node:os";
import { dirname, join } from "node:path";
import { createInterface } from "node:readline";

const tempDir = () =>
  createIsolatedSandboxProvider({
    name: "temp-dir",
    create: async (): Promise<IsolatedSandboxHandle> => {
      const root = await mkdtemp(join(tmpdir(), "sandbox-"));
      const worktreePath = join(root, "workspace");
      await mkdir(worktreePath, { recursive: true });

      return {
        worktreePath,

        exec: (
          command: string,
          opts?: { onLine?: (line: string) => void; cwd?: string },
        ): Promise<ExecResult> => {
          if (opts?.onLine) {
            const onLine = opts.onLine;
            return new Promise((resolve, reject) => {
              const proc = spawn("sh", ["-c", command], {
                cwd: opts?.cwd ?? worktreePath,
                stdio: ["ignore", "pipe", "pipe"],
              });

              const stdoutChunks: string[] = [];
              const stderrChunks: string[] = [];

              const rl = createInterface({ input: proc.stdout! });
              rl.on("line", (line) => {
                stdoutChunks.push(line);
                onLine(line);
              });

              proc.stderr!.on("data", (chunk: Buffer) => {
                stderrChunks.push(chunk.toString());
              });

              proc.on("error", (err) => reject(err));
              proc.on("close", (code) => {
                resolve({
                  stdout: stdoutChunks.join("\n"),
                  stderr: stderrChunks.join(""),
                  exitCode: code ?? 0,
                });
              });
            });
          }

          return new Promise((resolve, reject) => {
            execFile(
              "sh",
              ["-c", command],
              { cwd: opts?.cwd ?? worktreePath, maxBuffer: 10 * 1024 * 1024 },
              (error, stdout, stderr) => {
                if (error && error.code === undefined) {
                  reject(new Error(`exec failed: ${error.message}`));
                } else {
                  resolve({
                    stdout: stdout.toString(),
                    stderr: stderr.toString(),
                    exitCode: typeof error?.code === "number" ? error.code : 0,
                  });
                }
              },
            );
          });
        },

        copyIn: async (hostPath: string, sandboxPath: string) => {
          const info = await stat(hostPath);
          if (info.isDirectory()) {
            await cp(hostPath, sandboxPath, { recursive: true });
          } else {
            await mkdir(dirname(sandboxPath), { recursive: true });
            await copyFile(hostPath, sandboxPath);
          }
        },

        copyFileOut: async (sandboxPath: string, hostPath: string) => {
          await mkdir(dirname(hostPath), { recursive: true });
          await copyFile(sandboxPath, hostPath);
        },

        close: async () => {
          await rm(root, { recursive: true, force: true });
        },
      };
    },
  });
```

### 分支策略 (Branch strategies)

分支策略控制代理的提交落在哪里。在构建提供商时配置它：

| Strategy        | Behavior                                                                 | Bind-mount | Isolated  |
| --------------- | ------------------------------------------------------------------------ | ---------- | --------- |
| `head`          | 代理直接写入主机工作目录。不创建 worktree | Default    | N/A       |
| `merge-to-head` | Sandcastle 创建一个临时分支，完成后合并回 HEAD          | Supported  | Default   |
| `branch`        | 提交落在你提供的显式命名分支上                     | Supported  | Supported |

**何时使用每个策略：**

- **`head`** —— 开发期间的快速迭代。没有分支间接层，没有合并步骤。仅适用于绑定挂载提供商，因为代理需要直接访问主机文件系统。
- **`merge-to-head`** —— 自动化的安全默认值。代理在一个一次性分支上工作；如果出现问题，HEAD 保持不变。用于 CI 或无人值守运行。
- **`branch`** —— 当你想要在特定分支上进行提交时（例如用于 PR）。传递 `{ type: "branch", branch: "agent/fix-42" }`。

现在在 `run()` 上配置分支策略，而不是在提供商上：

```typescript
import { run, claudeCode } from "@ai-hero/sandcastle";
import { docker } from "@ai-hero/sandcastle/sandboxes/docker";

// head — direct write, bind-mount only (default for bind-mount providers)
await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  prompt: "…",
});
// merge-to-head — temp branch, merge back (default for isolated providers)
await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: tempDir(),
  prompt: "…",
});
// branch — explicit named branch
await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: docker(),
  branchStrategy: { type: "branch", branch: "agent/fix-42" },
  prompt: "…",
});
```

### 传递给 `run()`

通过 `sandbox` 选项传递你的自定义提供商 —— 它与内置的 `docker()` 提供商工作方式相同：

```typescript
import { run, claudeCode } from "@ai-hero/sandcastle";

const result = await run({
  agent: claudeCode("claude-opus-4-7"),
  sandbox: localProcess(), // your custom provider
  prompt: "Fix issue #42 in this repo.",
});
```

### 引用实现 (Reference implementations)

有关实际示例，请参阅：

- [`src/sandboxes/docker.ts`](src/sandboxes/docker.ts) —— 使用 Docker 容器的绑定挂载提供商（支持 SELinux 标签）
- [`src/sandboxes/vercel.ts`](src/sandboxes/vercel.ts) —— 通过 `@vercel/sandbox` 使用 Vercel Firecracker microVMs 的隔离提供商
- [`src/sandboxes/podman.ts`](src/sandboxes/podman.ts) —— 使用 Podman 容器的绑定挂载提供商（支持 SELinux 标签）
- [`src/sandboxes/test-isolated.ts`](src/sandboxes/test-isolated.ts) —— 使用临时目录的隔离提供商（在测试中使用）

## 配置 (Configuration)

### 配置目录 (`.sandcastle/`)

所有每个仓库的沙箱配置都位于 `.sandcastle/` 中。运行 `sandcastle init` 以创建它。

### 自定义 Dockerfile

`.sandcastle/Dockerfile` 控制沙箱环境。默认模板安装：

- **Node.js 22** (基础镜像)
- **git**, **curl**, **jq** (系统依赖项)
- **GitHub CLI** (`gh`)
- **Claude Code CLI**
- 一个非根 `agent` 用户（必需 —— Claude 作为该用户运行）

在自定义 Dockerfile 时，请确保保留：

- 一个非根用户（默认的 `agent` 用户），供 Claude 运行
- `git`（提交和分支操作所需）
- `gh`（获取问题所需）
- 已安装并位于 PATH 上的 Claude Code CLI

根据需要向 Dockerfile 添加你的项目特定依赖项（例如，语言运行时、构建工具）。

### 钩子 (Hooks)

钩子按**运行位置**分组 —— `host`（在开发人员的机器上）或 `sandbox`（在容器内）：

```ts
hooks: {
  host: {
    onWorktreeReady: [{ command: "cp .env.example .env" }],
    onSandboxReady:  [{ command: "echo sandbox is up" }],
  },
  sandbox: {
    onSandboxReady: [
      { command: "npm install", timeoutMs: 300_000 },
      { command: "apt-get install -y ffmpeg", sudo: true },
    ],
  },
}
```

| Hook                     | Runs on | When                                         | Working directory                           |
| ------------------------ | ------- | -------------------------------------------- | ------------------------------------------- |
| `host.onWorktreeReady`   | Host    | After `copyToWorktree`, before sandbox start | Worktree path (host repo root under `head`) |
| `host.onSandboxReady`    | Host    | After sandbox is up                          | Worktree path (host repo root under `head`) |
| `sandbox.onSandboxReady` | Sandbox | After sandbox is up                          | Sandbox repo directory                      |

**排序：** `copyToWorktree` -> `host.onWorktreeReady`（顺序）-> 沙箱创建 -> `host.onSandboxReady` + `sandbox.onSandboxReady`（并行）。

- **主机钩子**接受 `{ command: string; timeoutMs?: number }` —— 没有 `sudo`，没有 `cwd`。在命令字符串中使用 `cd` 或内联 env。
- **沙箱钩子**接受 `{ command: string; sudo?: boolean; timeoutMs?: number }` —— 设置 `sudo: true` 以获得提升的权限。
- **`timeoutMs`** 覆盖默认的每个钩子 60 秒超时。对于长时间运行的安装命令（如依赖项安装）非常有用（例如，5 分钟的 `timeoutMs: 300_000`）。
- 在每个钩子点内，沙箱钩子并行运行；`onSandboxReady` 内的主机钩子也与沙箱钩子并行运行。`host.onWorktreeReady` 钩子按声明顺序顺序运行。
- 如果任何钩子以非零退出，设置将快速失败。
- 当向 `run()` 传递 `signal` 时，它会传递给所有钩子 —— 中止信号会取消任何进行中的钩子命令。

## 开发 (Development)

```bash
npm install
npm run build    # Bundle with tsup
npm test         # Run tests with vitest
npm run typecheck # Type-check
```

## License

MIT