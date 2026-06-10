# <img src="https://github.com/aidenybai/react-grab/blob/main/.github/public/logo.png?raw=true" width="60" align="center" /> React Grab

[![version](https://img.shields.io/npm/v/react-grab?style=flat&colorA=000000&colorB=000000)](https://npmjs.com/package/react-grab)
[![downloads](https://img.shields.io/npm/dt/react-grab.svg?style=flat&colorA=000000&colorB=000000)](https://npmjs.com/package/react-grab)

将任意 UI 元素复制给你的 Agent。

React Grab 会将 Agent 指向每次选中内容背后的实际源代码。使用 React Grab 时，Agent 的运行速度可提升 **2倍**，且准确性更高。

[**官方网站 →**](https://react-grab.com)

## 快速开始

在项目根目录运行以下命令：

```bash
npx grab@latest init
```

## 工作原理

React Grab 将浏览器中的选中内容转换为你 Agent 可使用的源代码上下文：

1. 在应用中悬停任意 UI 元素。
2. 按下 **⌘C** 或 **Ctrl+C**。
3. 将复制的上下文粘贴到你的 Agent 中。

复制的内容包含选中的元素及其组件堆栈与源代码位置信息：

```txt
[<a class="ml-auto inline-block text-sm" href="#">Forgot your password?</a> in LoginForm (at components/login-form.tsx:46:19)]
```

## 手动安装

如果你无法使用 CLI，请根据你的框架手动安装 React Grab：

#### Next.js（App Router）

将其添加到你的 `app/layout.tsx` 中：

```jsx
import Script from "next/script";

export default function RootLayout({ children }) {
  return (
    <html>
      <head>
        {process.env.NODE_ENV === "development" && (
          <Script
            src="//unpkg.com/react-grab/dist/index.global.js"
            crossOrigin="anonymous"
            strategy="beforeInteractive"
          />
        )}
      </head>
      <body>{children}</body>
    </html>
  );
}
```

#### Next.js（Pages Router）

将其添加到你的 `pages/_document.tsx` 中：

```jsx
import { Html, Head, Main, NextScript } from "next/document";

export default function Document() {
  return (
    <Html lang="en">
      <Head>
        {process.env.NODE_ENV === "development" && (
          <Script
            src="//unpkg.com/react-grab/dist/index.global.js"
            crossOrigin="anonymous"
            strategy="beforeInteractive"
          />
        )}
      </Head>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  );
}
```

#### Vite

将其添加到你主入口文件的顶部（例如 `src/main.tsx`）：

```tsx
if (import.meta.env.DEV) {
  import("react-grab");
}
```

#### Webpack

首先，安装 React Grab：

```bash
npm install react-grab
```

然后将其添加到你主入口文件的顶部（例如 `src/index.tsx` 或 `src/main.tsx`）：

```tsx
if (process.env.NODE_ENV === "development") {
  import("react-grab");
}
```

## 插件扩展

使用插件可为 React Grab 的内置 UI 添加右键菜单操作、工具栏菜单项、生命周期钩子以及主题覆盖等功能。

通过导出函数 `registerPlugin` 注册插件：

```js
import { registerPlugin } from "react-grab";

registerPlugin({
  name: "my-plugin",
  hooks: {
    onElementSelect: (element) => {
      console.log("Selected:", element.tagName);
    },
  },
});
```

如果在 React 中编写，请在 `useEffect` 内部进行注册：

```jsx
import { registerPlugin, unregisterPlugin } from "react-grab";

useEffect(() => {
  registerPlugin({
    name: "my-plugin",
    actions: [
      {
        id: "my-action",
        label: "My Action",
        shortcut: "M",
        onAction: (context) => {
          console.log("Action on:", context.element);
          context.hideContextMenu();
        },
      },
    ],
  });

  return () => unregisterPlugin("my-plugin");
}, []);
```

操作项使用 `target` 字段控制其显示位置。省略 `target`（或设置为 `"context-menu"`）表示显示在右键菜单中，设置为 `"toolbar"` 则显示在工具栏下拉菜单中：

```js
actions: [
  {
    id: "inspect",
    label: "Inspect",
    shortcut: "I",
    onAction: (ctx) => console.dir(ctx.element),
  },
  {
    id: "toggle-freeze",
    label: "Freeze",
    // Only show in the toolbar
    target: "toolbar",
    isActive: () => isFrozen,
    onAction: () => toggleFreeze(),
  },
];
```

完整接口定义请参见 [`packages/react-grab/src/types.ts`](https://github.com/aidenybai/react-grab/blob/main/packages/react-grab/src/types.ts)，包含 `Plugin`、`PluginHooks` 和 `PluginConfig`。

## 资源与贡献指南

想先体验一下？请查看[我们的演示页面](https://react-grab.com)。

想要参与贡献？请参阅[贡献指南](https://github.com/aidenybai/react-grab/blob/main/CONTRIBUTING.md)。

想与社区交流？欢迎加入我们的 [Discord](https://discord.com/invite/G7zxfUzkm7)，分享你的想法以及使用 React Grab 构建的项目。

发现 Bug？请前往我们的[问题追踪器](https://github.com/aidenybai/react-grab/issues)，我们将尽力协助解决。我们也热烈欢迎 Pull Request！

我们期望所有贡献者遵守我们的[行为准则](https://github.com/aidenybai/react-grab/blob/main/.github/CODE_OF_CONDUCT.md)。

[**在 GitHub 上开始贡献**](https://github.com/aidenybai/react-grab/blob/main/CONTRIBUTING.md)

### 许可证

React Grab 是基于 MIT 许可证的开源软件。

_感谢 [Andrew Luetgers](https://github.com/andrewluetgers) 捐赠 `grab` npm 包名。_