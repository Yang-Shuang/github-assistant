# 与 Figma MCP 对话

本项目实现了人工智能代理（如 Cursor、Claude Code）与 Figma 之间的模型上下文协议（Model Context Protocol, MCP）集成，使 AI 代理能够与 Figma 通信，以读取设计稿并通过编程方式修改它们。

https://github.com/user-attachments/assets/129a14d2-ed73-470f-9a4c-2240b2a4885c

## 项目结构

- `src/talk_to_figma_mcp/` - 用于 Figma 集成的 TypeScript MCP 服务器
- `src/cursor_mcp_plugin/` - 与 Cursor 通信的 Figma 插件
- `src/socket.ts` - WebSocket 服务器，负责促进 MCP 服务器与 Figma 插件之间的通信

## 使用方法

1. 如果你尚未安装 Bun：

```bash
curl -fsSL https://bun.sh/install | bash
```

2. 运行设置脚本，这还会在你的 Cursor 活动项目中安装 MCP：

```bash
bun setup
```

3. 启动 WebSocket 服务器：

```bash
bun socket
```

4. **新增** 从 [Figma 社区页面](https://www.figma.com/community/plugin/1485687494525374295/cursor-talk-to-figma-mcp-plugin) 安装 Figma 插件，或[本地安装](#figma-plugin)

## 快速视频教程

[Video Link](https://www.linkedin.com/posts/sonnylazuardi_just-wanted-to-share-my-latest-experiment-activity-7307821553654657024-yrh8)

## 设计自动化示例

**批量文本内容替换**

感谢 [@dusskapark](https://github.com/dusskapark) 贡献了批量文本替换功能。这里是[演示视频](https://www.youtube.com/watch?v=j05gGT3xfCs)。

**实例覆盖属性传播**
来自 [@dusskapark](https://github.com/dusskapark) 的另一项贡献。
通过一条命令将组件实例的覆盖属性从源实例传播到多个目标实例。当处理需要类似自定义设置的组件实例时，此功能可大幅减少重复性的设计工作。查看我们的[演示视频](https://youtu.be/uvuT8LByroI)。

## 手动设置与安装

### MCP 服务器：与 Cursor 集成

将以下配置添加到你的 Cursor MCP 配置文件 `~/.cursor/mcp.json` 中：

```json
{
  "mcpServers": {
    "TalkToFigma": {
      "command": "bunx",
      "args": ["cursor-talk-to-figma-mcp@latest"]
    }
  }
}
```

### WebSocket 服务器

启动 WebSocket 服务器：

```bash
bun socket
```

### Figma 插件

1. 在 Figma 中，依次点击 `Plugins`（插件）> `Development`（开发）> `New Plugin`（新建插件）
2. 选择“链接现有插件”（Link existing plugin）
3. 选择 `src/cursor_mcp_plugin/manifest.json` 文件
4. 该插件现在应出现在你的 Figma 开发插件列表中

## Windows + WSL 指南

1. 通过 PowerShell 安装 Bun：

```bash
powershell -c "irm bun.sh/install.ps1|iex"
```

2. 在 `src/socket.ts` 中取消对主机名 `0.0.0.0` 的注释：

```typescript
// uncomment this to allow connections in windows wsl
hostname: "0.0.0.0",
```

3. 启动 WebSocket：

```bash
bun socket
```

## 使用流程

1. 启动 WebSocket 服务器
2. 在 Cursor 中安装 MCP 服务器
3. 打开 Figma 并运行 Cursor MCP 插件
4. 使用 `join_channel` 加入频道，将插件连接到 WebSocket 服务器
5. 在 Cursor 中使用 MCP 工具与 Figma 进行交互

## 本地开发设置

如需进行本地开发，请将你的 MCP 配置指向本地目录：

```json
{
  "mcpServers": {
    "TalkToFigma": {
      "command": "bun",
      "args": ["/path-to-repo/src/talk_to_figma_mcp/server.ts"]
    }
  }
}
```

## MCP 工具

MCP 服务器提供以下用于与 Figma 交互的工具：

### 文档与选区

- `get_document_info` - 获取当前 Figma 文档的信息
- `get_selection` - 获取当前选中内容的信息
- `read_my_design` - 无需参数即可获取当前选中项的详细节点信息
- `get_node_info` - 获取特定节点的详细信息
- `get_nodes_info` - 通过提供节点 ID 数组，获取多个节点的详细信息
- `set_focus` - 选中特定节点并将视口滚动至该位置以聚焦
- `set_selections` - 设置多个节点的选区，并滚动视口以显示它们

### 注释（Annotations）

- `get_annotations` - 获取当前文档或特定节点中的所有注释
- `set_annotation` - 创建或更新支持 Markdown 的注释
- `set_multiple_annotations` - 批量高效创建/更新多个注释
- `scan_nodes_by_types` - 扫描具有特定类型的节点（可用于查找注释目标）

### 原型与连接

- `get_reactions` - 获取带有视觉高亮动画的所有节点原型交互反应
- `set_default_connector` - 将复制的 FigJam 连接线设为创建连接时的默认样式（必须在创建连接前设置）
- `create_connections` - 基于原型流程或自定义映射，在节点间创建 FigJam 连接线

### 创建元素

- `create_rectangle` - 创建带有位置、尺寸和可选名称的新矩形
- `create_frame` - 创建带有位置、尺寸和可选名称的新画框（Frame）
- `create_text` - 创建具有可自定义字体属性的新文本节点

### 修改文本内容

- `scan_text_nodes` - 针对大型设计稿使用智能分块扫描文本节点
- `set_text_content` - 设置单个文本节点的文本内容
- `set_multiple_text_contents` - 批量高效更新多个文本节点

### 自动布局与间距

- `set_layout_mode` - 设置画框的布局模式及换行行为（无、水平、垂直）
- `set_padding` - 设置自动布局画框的内边距值（上、右、下、左）
- `set_axis_align` - 设置自动布局画框的主轴与交叉轴对齐方式
- `set_layout_sizing` - 设置自动布局画框的水平与垂直尺寸模式（固定、自适应内容、填充）
- `set_item_spacing` - 设置自动布局画框中子元素之间的间距

### 样式

- `set_fill_color` - 设置节点的填充颜色（RGBA）
- `set_stroke_color` - 设置节点的描边颜色与粗细
- `set_corner_radius` - 设置节点圆角半径，支持按角单独控制

### 布局与组织

- `move_node` - 将节点移动到新位置
- `resize_node` - 按新尺寸调整节点大小
- `delete_node` - 删除单个节点
- `delete_multiple_nodes` - 批量高效删除多个节点
- `clone_node` - 创建现有节点的副本，支持可选的位置偏移

### 组件与样式

- `get_styles` - 获取本地样式信息
- `get_local_components` - 获取本地组件信息
- `create_component_instance` - 创建组件实例
- `get_instance_overrides` - 提取已选中组件实例的覆盖属性
- `set_instance_overrides` - 将提取的覆盖属性应用到目标实例

### 导出与高级功能

- `export_node_as_image` - 将节点导出为图像（PNG、JPG、SVG 或 PDF）- 目前对图片的支持有限，返回 base64 文本格式

### 连接管理

- `join_channel` - 加入特定频道以与 Figma 通信

### MCP 提示词（Prompts）

MCP 服务器内置了多个辅助提示词，引导你完成复杂的设计任务：

- `design_strategy` - 操作 Figma 设计稿的最佳实践
- `read_design_strategy` - 读取 Figma 设计稿的最佳实践
- `text_replacement_strategy` - 在 Figma 设计中替换文本的系统化方法
- `annotation_conversion_strategy` - 将手动注释转换为 Figma 原生注释的策略
- `swap_overrides_instances` - 在 Figma 组件实例间转移覆盖属性的策略
- `reaction_to_connector_strategy` - 利用 `get_reactions` 的输出，将 Figma 原型交互反应（noodles）转换为连接线的策略，并引导依次使用 `create_connections`

## 开发指南

### 构建 Figma 插件

1. 进入 Figma 插件目录：

   ```
   cd src/cursor_mcp_plugin
   ```

2. 编辑 `code.js` 和 `ui.html`

## 最佳实践

在使用 Figma MCP 时，请遵循以下建议：

1. 发送命令前务必先加入频道
2. 首先使用 `get_document_info` 获取文档概览
3. 修改前先通过 `get_selection` 检查当前选区
4. 根据需求选择合适的创建工具：
   - 使用 `create_frame` 创建容器
   - 使用 `create_rectangle` 创建基础形状
   - 使用 `create_text` 创建文本元素
5. 使用 `get_node_info` 验证更改结果
6. 尽可能使用组件实例以保持设计一致性
7. 妥善处理错误，因为所有命令均可能抛出异常
8. 针对大型设计稿：
   - 在 `scan_text_nodes` 中使用分块参数
   - 通过 WebSocket 更新监控进度
   - 实现适当的错误处理机制
9. 针对文本操作：
   - 尽可能使用批量操作
   - 考虑结构层级关系
   - 通过定向导出验证更改结果
10. 针对转换旧版注释：
    - 扫描文本节点以识别编号标记和描述内容
    - 使用 `scan_nodes_by_types` 查找注释所指向的 UI 元素
    - 通过路径、名称或空间位置将标记与目标元素进行匹配
    - 利用 `get_annotations` 对注释进行合理分类
    - 批量创建原生注释（使用 `set_multiple_annotations`）
    - 验证所有注释是否已正确链接至目标元素
    - 转换成功后删除旧版注释节点
11. 将原型连线（noodles）可视化为 FigJam 连接线：

- 使用 `get_reactions` 提取原型流程，
- 通过 `set_default_connector` 设置默认连接器样式，
- 并使用 `create_connections` 生成连接线，以实现清晰的视觉流向映射。

## 许可证

MIT