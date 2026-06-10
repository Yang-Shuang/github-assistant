<!-- omit in toc -->
<div align="center">
<img src="./logo.png" alt="MCP Go Logo">

[![Build](https://github.com/mark3labs/mcp-go/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/mark3labs/mcp-go/actions/workflows/ci.yml)
[![Go Report Card](https://goreportcard.com/badge/github.com/mark3labs/mcp-go?cache)](https://goreportcard.com/report/github.com/mark3labs/mcp-go)
[![GoDoc](https://pkg.go.dev/badge/github.com/mark3labs/mcp-go.svg)](https://pkg.go.dev/github.com/mark3labs/mcp-go)

[![AgentRank](https://agentrank-ai.com/api/badge/tool/mark3labs--mcp-go)](https://agentrank-ai.com/tool/mark3labs--mcp-go/)
<strong>一个基于 Go 语言实现的模型上下文协议（Model Context Protocol, MCP）库，旨在实现大语言模型（LLM）应用与外部数据源及工具之间的无缝集成。</strong>

<br>

[![Tutorial](http://img.youtube.com/vi/qoaeYMrXJH0/0.jpg)](http://www.youtube.com/watch?v=qoaeYMrXJH0 "Tutorial")

<br>

在 [Discord](https://discord.gg/RqSS2NQVsY) 上讨论该 SDK

</div>


```go
package main

import (
    "context"
    "fmt"

    "github.com/mark3labs/mcp-go/mcp"
    "github.com/mark3labs/mcp-go/server"
)

func main() {
    // Create a new MCP server
    s := server.NewMCPServer(
        "Demo 🚀",
        "1.0.0",
        server.WithToolCapabilities(false),
    )

    // Add tool
    tool := mcp.NewTool("hello_world",
        mcp.WithDescription("Say hello to someone"),
        mcp.WithString("name",
            mcp.Required(),
            mcp.Description("Name of the person to greet"),
        ),
    )

    // Add tool handler
    s.AddTool(tool, helloHandler)

    // Start the stdio server
    if err := server.ServeStdio(s); err != nil {
        fmt.Printf("Server error: %v\n", err)
    }
}

func helloHandler(ctx context.Context, request mcp.CallToolRequest) (*mcp.CallToolResult, error) {
    name, err := request.RequireString("name")
    if err != nil {
        return mcp.NewToolResultError(err.Error()), nil
    }

    return mcp.NewToolResultText(fmt.Sprintf("Hello, %s!", name)), nil
}
```

就是这样！

MCP Go 处理了所有复杂的协议细节和服务器管理，让你可以专注于构建优秀的工具。它力求提供高级且易用的接口。

### 核心特性：
* **快速**：高级接口意味着更少的代码和更快的开发速度
* **简洁**：以最少的样板代码构建 MCP 服务器
* **完整\***：MCP Go 力求提供对核心 MCP 规范的完整实现

（\*强调“力求”）

🚨 🚧 🏗️ *MCP Go 与 MCP 规范本身均处于积极开发中。核心功能已正常运行，但部分高级特性仍在完善中。* 


<!-- omit in toc -->
## 目录

- [安装](#installation)
- [快速开始](#quickstart)
- [什么是 MCP？](#what-is-mcp)
- [核心概念](#core-concepts)
  - [服务器（Server）](#server)
  - [资源（Resource）](#resources)
  - [工具（Tool）](#tools)
  - [提示词模板（Prompt）](#prompts)
- [示例](#examples)
- [扩展特性](#extras)
  - [传输层（Transport）](#transports)
  - [OAuth 受保护资源元数据](#oauth-protected-resource-metadata)
  - [会话管理](#session-management)
    - [基础会话处理](#basic-session-handling)
    - [按会话配置的工具](#per-session-tools)
    - [工具过滤](#tool-filtering)
    - [使用上下文（Context）](#working-with-context)
  - [请求钩子（Hooks）](#request-hooks)
  - [工具处理器中间件](#tool-handler-middleware)
  - [重新生成服务器代码](#regenerating-server-code)

## 安装

```bash
go get github.com/mark3labs/mcp-go
```

## 快速开始

让我们创建一个简单的 MCP 服务器，它暴露一个计算器工具和部分数据：

```go
package main

import (
    "context"
    "fmt"

    "github.com/mark3labs/mcp-go/mcp"
    "github.com/mark3labs/mcp-go/server"
)

func main() {
    // Create a new MCP server
    s := server.NewMCPServer(
        "Calculator Demo",
        "1.0.0",
        server.WithToolCapabilities(false),
        server.WithRecovery(),
    )

    // Add a calculator tool
    calculatorTool := mcp.NewTool("calculate",
        mcp.WithDescription("Perform basic arithmetic operations"),
        mcp.WithString("operation",
            mcp.Required(),
            mcp.Description("The operation to perform (add, subtract, multiply, divide)"),
            mcp.Enum("add", "subtract", "multiply", "divide"),
        ),
        mcp.WithNumber("x",
            mcp.Required(),
            mcp.Description("First number"),
        ),
        mcp.WithNumber("y",
            mcp.Required(),
            mcp.Description("Second number"),
        ),
    )

    // Add the calculator handler
    s.AddTool(calculatorTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CallToolResult, error) {
        // Using helper functions for type-safe argument access
        op, err := request.RequireString("operation")
        if err != nil {
            return mcp.NewToolResultError(err.Error()), nil
        }
        
        x, err := request.RequireFloat("x")
        if err != nil {
            return mcp.NewToolResultError(err.Error()), nil
        }
        
        y, err := request.RequireFloat("y")
        if err != nil {
            return mcp.NewToolResultError(err.Error()), nil
        }

        var result float64
        switch op {
        case "add":
            result = x + y
        case "subtract":
            result = x - y
        case "multiply":
            result = x * y
        case "divide":
            if y == 0 {
                return mcp.NewToolResultError("cannot divide by zero"), nil
            }
            result = x / y
        }

        return mcp.NewToolResultText(fmt.Sprintf("%.2f", result)), nil
    })

    // Start the server
    if err := server.ServeStdio(s); err != nil {
        fmt.Printf("Server error: %v\n", err)
    }
}
```

## 什么是 MCP？

[模型上下文协议（Model Context Protocol, MCP）](https://modelcontextprotocol.io) 允许你以安全、标准化的方式构建服务器，向大语言模型（LLM）应用暴露数据和功能。可以把它想象成一种 Web API，但它是专门为 LLM 交互设计的。

MCP 服务器能够：
- 通过**资源（Resource）**暴露数据（类似于 GET 端点；用于将信息加载到 LLM 的上下文中）
- 通过**工具（Tool）**提供功能（类似于 POST 端点；用于执行代码或产生其他副作用）
- 通过**提示词模板（Prompt）**定义交互模式（LLM 交互的可复用模板）
- 以及更多！

`mcp-go` 实现了 Model Context Protocol 规范版本 2025-11-25，并兼容 2025-06-18、2025-03-26 和 2024-11-05 版本。

## 核心概念


### 服务器（Server）

<details>
<summary>Show Server Examples</summary>

服务器是你与 MCP 协议交互的核心接口。它负责连接管理、协议合规性和消息路由：

```go
// Create a basic server
s := server.NewMCPServer(
    "My Server",  // Server name
    "1.0.0",     // Version
)

// Start the server using stdio
if err := server.ServeStdio(s); err != nil {
    log.Fatalf("Server error: %v", err)
}
```

</details>

### 资源（Resource）

<details>
<summary>Show Resource Examples</summary>
资源是你向 LLM 暴露数据的方式。它可以是任何内容——文件、API 响应、数据库查询、系统信息等。资源可以是：

- 静态（固定 URI）
- 动态（使用 URI 模板）

以下是一个静态资源的简单示例：

```go
// Static resource example - exposing a README file
resource := mcp.NewResource(
    "docs://readme",
    "Project README",
    mcp.WithResourceDescription("The project's README file"), 
    mcp.WithMIMEType("text/markdown"),
)

// Add resource with its handler
s.AddResource(resource, func(ctx context.Context, request mcp.ReadResourceRequest) ([]mcp.ResourceContents, error) {
    content, err := os.ReadFile("README.md")
    if err != nil {
        return nil, err
    }
    
    return []mcp.ResourceContents{
        mcp.TextResourceContents{
            URI:      "docs://readme",
            MIMEType: "text/markdown",
            Text:     string(content),
        },
    }, nil
})
```

以下是使用模板的动态资源示例：

```go
// Dynamic resource example - user profiles by ID
template := mcp.NewResourceTemplate(
    "users://{id}/profile",
    "User Profile",
    mcp.WithTemplateDescription("Returns user profile information"),
    mcp.WithTemplateMIMEType("application/json"),
)

// Add template with its handler
s.AddResourceTemplate(template, func(ctx context.Context, request mcp.ReadResourceRequest) ([]mcp.ResourceContents, error) {
    // Extract ID from the URI using regex matching
    // The server automatically matches URIs to templates
    userID := extractIDFromURI(request.Params.URI)
    
    profile, err := getUserProfile(userID)  // Your DB/API call here
    if err != nil {
        return nil, err
    }
    
    return []mcp.ResourceContents{
        mcp.TextResourceContents{
            URI:      request.Params.URI,
            MIMEType: "application/json",
            Text:     profile,
        },
    }, nil
})
```

这些示例虽然简单，但展示了核心概念。资源可以更加复杂——例如提供多种内容、集成数据库或外部 API 等。
</details>

### 工具（Tool）

<details>
<summary>Show Tool Examples</summary>

工具允许 LLM 通过你的服务器执行操作。与资源不同，工具预期会执行计算并产生副作用。它们类似于 REST API 中的 POST 端点。

#### 任务增强型工具（Task-Augmented Tools）

任务增强型工具异步执行并通过轮询返回结果。这对于原本可能会阻塞或超时的长时间运行操作非常有用。任务工具支持三种模式：

- **TaskSupportForbidden**（默认）：该工具不能作为任务调用
- **TaskSupportOptional**：该工具可以作为任务或同步方式调用
- **TaskSupportRequired**：该工具必须作为任务调用

```go
// Example: A tool that requires task execution
processBatchTool := mcp.NewTool("process_batch",
    mcp.WithDescription("Process a batch of items asynchronously"),
    mcp.WithTaskSupport(mcp.TaskSupportRequired),
    mcp.WithArray("items",
        mcp.Description("Array of items to process"),
        mcp.WithStringItems(),
        mcp.Required(),
    ),
)

// Task tool handler returns CreateTaskResult instead of CallToolResult
s.AddTaskTool(processBatchTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CreateTaskResult, error) {
    items := request.GetStringSlice("items", []string{})
    
    // Long-running work here
    for i, item := range items {
        select {
        case <-ctx.Done():
            // Task was cancelled
            return nil, ctx.Err()
        default:
            // Process item...
            processItem(item)
        }
    }
    
    // Return result - task ID and metadata are managed by the server
    return &mcp.CreateTaskResult{
        Task: mcp.Task{
            // Task fields (ID, status, etc.) are populated by the server
        },
    }, nil
})

// Enable task capabilities when creating the server
s := server.NewMCPServer(
    "Task Server",
    "1.0.0",
    server.WithTaskCapabilities(
        true, // listTasks: allows clients to list all tasks
        true, // cancel: allows clients to cancel running tasks
        true, // toolCallTasks: enables task augmentation for tools
    ),
    server.WithMaxConcurrentTasks(10), // Optional: limit concurrent running tasks
)
```

任务执行流程：
1. 客户端调用带任务参数的工具
2. 服务器立即返回任务 ID
3. 工具在后台异步执行
4. 客户端轮询 `tasks/result` 以获取结果
5. 完成后服务器发送任务状态通知

对于可选的任务工具，同一工具可以同步调用（不带任务参数）或异步调用（带任务参数）：

```go
// Tool with optional task support
analyzeTool := mcp.NewTool("analyze_data",
    mcp.WithDescription("Analyze data - can run sync or async"),
    mcp.WithTaskSupport(mcp.TaskSupportOptional),
    mcp.WithString("data", mcp.Required()),
)

// Use AddTaskTool for hybrid tools that support both modes
s.AddTaskTool(analyzeTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CreateTaskResult, error) {
    // This handler runs when called as a task
    data := request.GetString("data", "")
    result := analyzeData(data)
    
    return &mcp.CreateTaskResult{
        Task: mcp.Task{},
    }, nil
})

// The server automatically handles both sync and async invocations
// When called without task param: executes handler and returns immediately
// When called with task param: executes handler asynchronously
```

##### 限制并发任务数

为防止资源耗尽，你可以限制同时运行的任务数量：

```go
s := server.NewMCPServer(
    "Task Server",
    "1.0.0",
    server.WithTaskCapabilities(true, true, true),
    server.WithMaxConcurrentTasks(10), // Allow up to 10 concurrent running tasks
)
```

达到限制时，新的任务创建请求将因错误而失败。已完成、失败或已取消的任务不计入限制——只有处于 "working"（运行中）状态的任务才会计数。如果未指定 `WithMaxConcurrentTasks` 或设置为 0，则并发任务无限制。

对于传统同步工具（执行后立即返回结果）：

简单计算示例：
```go
calculatorTool := mcp.NewTool("calculate",
    mcp.WithDescription("Perform basic arithmetic calculations"),
    mcp.WithString("operation",
        mcp.Required(),
        mcp.Description("The arithmetic operation to perform"),
        mcp.Enum("add", "subtract", "multiply", "divide"),
    ),
    mcp.WithNumber("x",
        mcp.Required(),
        mcp.Description("First number"),
    ),
    mcp.WithNumber("y",
        mcp.Required(),
        mcp.Description("Second number"),
    ),
)

s.AddTool(calculatorTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CallToolResult, error) {
    args := request.GetArguments()
    op := args["operation"].(string)
    x := args["x"].(float64)
    y := args["y"].(float64)

    var result float64
    switch op {
    case "add":
        result = x + y
    case "subtract":
        result = x - y
    case "multiply":
        result = x * y
    case "divide":
        if y == 0 {
            return mcp.NewToolResultError("cannot divide by zero"), nil
        }
        result = x / y
    }
    
    return mcp.FormatNumberResult(result), nil
})
```

HTTP 请求示例：
```go
httpTool := mcp.NewTool("http_request",
    mcp.WithDescription("Make HTTP requests to external APIs"),
    mcp.WithString("method",
        mcp.Required(),
        mcp.Description("HTTP method to use"),
        mcp.Enum("GET", "POST", "PUT", "DELETE"),
    ),
    mcp.WithString("url",
        mcp.Required(),
        mcp.Description("URL to send the request to"),
        mcp.Pattern("^https?://.*"),
    ),
    mcp.WithString("body",
        mcp.Description("Request body (for POST/PUT)"),
    ),
)

s.AddTool(httpTool, func(ctx context.Context, request mcp.CallToolRequest) (*mcp.CallToolResult, error) {
    args := request.GetArguments()
    method := args["method"].(string)
    url := args["url"].(string)
    body := ""
    if b, ok := args["body"].(string); ok {
        body = b
    }

    // Create and send request
    var req *http.Request
    var err error
    if body != "" {
        req, err = http.NewRequest(method, url, strings.NewReader(body))
    } else {
        req, err = http.NewRequest(method, url, nil)
    }
    if err != nil {
        return mcp.NewToolResultErrorFromErr("unable to create request", err), nil
    }

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        return mcp.NewToolResultErrorFromErr("unable to execute request", err), nil
    }
    defer resp.Body.Close()

    // Return response
    respBody, err := io.ReadAll(resp.Body)
    if err != nil {
        return mcp.NewToolResultErrorFromErr("unable to read request response", err), nil
    }

    return mcp.NewToolResultText(fmt.Sprintf("Status: %d\nBody: %s", resp.StatusCode, string(respBody))), nil
})
```

工具可用于任何类型的计算或副作用操作：
- 数据库查询
- 文件操作  
- 外部 API 调用
- 数学计算
- 系统操作

每个工具应做到：
- 具有清晰的描述
- 验证输入参数
- 优雅处理错误 
- 返回结构化响应
- 使用适当的返回值类型

</details>

### 提示词模板（Prompt）

<details>
<summary>Show Prompt Examples</summary>

提示词模板是可复用的模板，帮助 LLM 更有效地与你的服务器交互。它们就像编码进你服务器的“最佳实践”。以下是一些示例：

```go
// Simple greeting prompt
s.AddPrompt(mcp.NewPrompt("greeting",
    mcp.WithPromptDescription("A friendly greeting prompt"),
    mcp.WithArgument("name",
        mcp.ArgumentDescription("Name of the person to greet"),
    ),
), func(ctx context.Context, request mcp.GetPromptRequest) (*mcp.GetPromptResult, error) {
    name := request.Params.Arguments["name"]
    if name == "" {
        name = "friend"
    }
    
    return mcp.NewGetPromptResult(
        "A friendly greeting",
        []mcp.PromptMessage{
            mcp.NewPromptMessage(
                mcp.RoleAssistant,
                mcp.NewTextContent(fmt.Sprintf("Hello, %s! How can I help you today?", name)),
            ),
        },
    ), nil
})

// Code review prompt with embedded resource
s.AddPrompt(mcp.NewPrompt("code_review",
    mcp.WithPromptDescription("Code review assistance"),
    mcp.WithArgument("pr_number",
        mcp.ArgumentDescription("Pull request number to review"),
        mcp.RequiredArgument(),
    ),
), func(ctx context.Context, request mcp.GetPromptRequest) (*mcp.GetPromptResult, error) {
    prNumber := request.Params.Arguments["pr_number"]
    if prNumber == "" {
        return nil, fmt.Errorf("pr_number is required")
    }
    
    return mcp.NewGetPromptResult(
        "Code review assistance",
        []mcp.PromptMessage{
            mcp.NewPromptMessage(
                mcp.RoleUser,
                mcp.NewTextContent("Review the changes and provide constructive feedback."),
            ),
            mcp.NewPromptMessage(
                mcp.RoleAssistant,
                mcp.NewEmbeddedResource(mcp.ResourceContents{
                    URI: fmt.Sprintf("git://pulls/%s/diff", prNumber),
                    MIMEType: "text/x-diff",
                }),
            ),
        },
    ), nil
})

// Database query builder prompt
s.AddPrompt(mcp.NewPrompt("query_builder",
    mcp.WithPromptDescription("SQL query builder assistance"),
    mcp.WithArgument("table",
        mcp.ArgumentDescription("Name of the table to query"),
        mcp.RequiredArgument(),
    ),
), func(ctx context.Context, request mcp.GetPromptRequest) (*mcp.GetPromptResult, error) {
    tableName := request.Params.Arguments["table"]
    if tableName == "" {
        return nil, fmt.Errorf("table name is required")
    }
    
    return mcp.NewGetPromptResult(
        "SQL query builder assistance",
        []mcp.PromptMessage{
            mcp.NewPromptMessage(
                mcp.RoleUser,
                mcp.NewTextContent("Help construct efficient and safe queries for the provided schema."),
            ),
            mcp.NewPromptMessage(
                mcp.RoleUser,
                mcp.NewEmbeddedResource(mcp.ResourceContents{
                    URI: fmt.Sprintf("db://schema/%s", tableName),
                    MIMEType: "application/json",
                }),
            ),
        },
    ), nil
})
```

提示词模板可以包含：
- 系统指令
- 必填参数
- 嵌入的资源
- 多条消息
- 不同的内容类型（文本、图片等）
- 自定义 URI 方案

</details>

## 示例

示例请参考 [`examples/`](examples/) 目录。

主要示例包括：
- [`examples/task_tool/`](examples/task_tool/) - 演示具有 TaskSupportRequired 和 TaskSupportOptional 模式的任务增强型工具
- [`examples/structured_input_and_output/`](examples/structured_input_and_output/) - 展示如何结合基于结构体的输入/输出 Schema 使用类型安全的工具处理器
- [`examples/typed_tools/`](examples/typed_tools/) - 演示具有强类型参数的类型安全工具处理器
- [`examples/custom_context/`](examples/custom_context/) - 展示如何在工具处理器中使用自定义上下文
- 目录中还有更多涵盖资源、提示词等内容的示例

## 扩展特性

### 传输层（Transport）

MCP-Go 支持 stdio、SSE 和 Streamable HTTP 传输层。对于 SSE 传输，你可以使用 `SetConnectionLostHandler()` 来检测和处理断连，以实现重连逻辑。

### 在非 net/http 框架中嵌入 StreamableHTTP

`StreamableHTTPServer` 是一个 `http.Handler`，因此可以挂载在任何支持 `net/http` 的路由器中。若要将其嵌入**不经过** `net/http` 的框架（例如 [fasthttp](https://github.com/valyala/fasthttp)
或 [fiber](https://gofiber.io/)）且不通过适配器缓冲响应，请使用传输无关的 `Handle` 入口点：

```go
func (s *StreamableHTTPServer) Handle(w HTTPResponseWriter, r *HTTPRequest)
```

`HTTPRequest` 是一个普通结构体（包含 `Method`, `URL`, `Header`, `Body`,
`Context`），而 `HTTPResponseWriter` 是一个小型接口（包含 `Header`,
`WriteHeader`, `Write`, `Flush`, `CanStream`）。底层传输无法流式传输的实现**必须**从 `CanStream` 返回 `false`；此时服务器将拒绝 GET（SSE 监听）请求并返回 `405 Method Not Allowed`，同时将 POST 响应保持为缓冲的 `application/json` 而非升级为 `text/event-stream`。

有关完整的 fasthttp/fiber 适配器示例，请参阅 [HTTP 传输文档](https://mcp-go.dev/transports/http#embedding-in-non-nethttp-frameworks)。`ServeHTTP` 保持不变，仍是标准的 `net/http` 入口点。

### OAuth 受保护资源元数据

需要 OAuth 的服务器可以通过 [RFC 9728](https://datatracker.ietf.org/doc/html/rfc9728)
定义的 `/.well-known/oauth-protected-resource` 端点来声明其授权要求，该端点由 [MCP 授权规范](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization) 引用。使用 `server.WithProtectedResourceMetadata`（或
`server.WithSSEProtectedResourceMetadata`）自动挂载该端点，或使用
`server.NewProtectedResourceMetadataHandler` 将其接入自定义路由器。示例请参阅 [HTTP 传输文档](https://mcp-go.dev/transports/http#oauth-protected-resource-metadata-rfc-9728)。

```go
httpServer := server.NewStreamableHTTPServer(mcpServer,
    server.WithProtectedResourceMetadata(server.ProtectedResourceMetadataConfig{
        Resource:             "https://my-mcp-server.com",
        AuthorizationServers: []string{"https://auth.example.com"},
        ScopesSupported:      []string{"mcp:read", "mcp:write"},
    }),
)
```

### 面向浏览器客户端的 CORS 支持

暴露给基于浏览器的 MCP 客户端的服务器可以选择在任一 HTTP 传输层启用跨域资源共享（CORS）处理。默认情况下 CORS 处于禁用状态；你可以通过 `server.WithStreamableHTTPCORS` 或
`server.WithSSECORS` 显式配置它：

```go
httpServer := server.NewStreamableHTTPServer(mcpServer,
    server.WithEndpointPath("/mcp"),
    server.WithStreamableHTTPCORS(
        server.WithCORSAllowedOrigins("https://my-ai-app.com", "http://localhost:3000"),
        server.WithCORSAllowCredentials(),
        server.WithCORSMaxAge(300),
    ),
)
```

传输层会直接响应预检（`OPTIONS`）请求，并在简单响应中附加适当的 `Access-Control-Allow-Origin`,
`Access-Control-Allow-Credentials`, `Access-Control-Expose-Headers` 和
`Vary` 头。当省略相应选项时，会使用合理的默认值（方法默认为 `GET, POST, DELETE, OPTIONS`；请求头默认为 `Content-Type, Mcp-Session-Id, Last-Event-ID, Authorization`；暴露的头默认为 `Mcp-Session-Id`）。将 `WithCORSAllowedOrigins("*")` 与 `WithCORSAllowCredentials()` 结合使用时，会回显请求的 `Origin` 以保持符合规范。

### 会话管理

MCP-Go 提供了健壮的会话管理系统，允许你：
- 为每个连接的客户端维护独立的状态
- 注册和跟踪客户端会话
- 向特定客户端发送通知
- 提供按会话定制的工具

<details>
<summary>Show Session Management Examples</summary>

#### 基础会话处理

```go
// Create a server with session capabilities
s := server.NewMCPServer(
    "Session Demo",
    "1.0.0",
    server.WithToolCapabilities(true),
)

// Implement your own ClientSession
type MySession struct {
    id           string
    notifChannel chan mcp.JSONRPCNotification
    isInitialized bool
    // Add custom fields for your application
}

// Implement the ClientSession interface
func (s *MySession) SessionID() string {
    return s.id
}

func (s *MySession) NotificationChannel() chan<- mcp.JSONRPCNotification {
    return s.notifChannel
}

func (s *MySession) Initialize() {
    s.isInitialized = true
}

func (s *MySession) Initialized() bool {
    return s.isInitialized
}

// Register a session
session := &MySession{
    id:           "user-123",
    notifChannel: make(chan mcp.JSONRPCNotification, 10),
}
if err := s.RegisterSession(context.Background(), session); err != nil {
    log.Printf("Failed to register session: %v", err)
}

// Send notification to a specific client
err := s.SendNotificationToSpecificClient(
    session.SessionID(),
    "notification/update",
    map[string]any{"message": "New data available!"},
)
if err != nil {
    log.Printf("Failed to send notification: %v", err)
}

// Unregister session when done
s.UnregisterSession(context.Background(), session.SessionID())
```

#### 按会话配置的工具（Per-Session Tools）

对于更高级的用例，你可以实现 `SessionWithTools` 接口以支持按会话定制工具：

```go
// Implement SessionWithTools interface for per-session tools
type MyAdvancedSession struct {
    MySession  // Embed the basic session
    sessionTools map[string]server.ServerTool
}

// Implement additional methods for SessionWithTools
func (s *MyAdvancedSession) GetSessionTools() map[string]server.ServerTool {
    return s.sessionTools
}

func (s *MyAdvancedSession) SetSessionTools(tools map[string]server.ServerTool) {
    s.sessionTools = tools
}

// Create and register a session with tools support
advSession := &MyAdvancedSession{
    MySession: MySession{
        id:           "user-456",
        notifChannel: make(chan mcp.JSONRPCNotification, 10),
    },
    sessionTools: make(map[string]server.ServerTool),
}
if err := s.RegisterSession(context.Background(), advSession); err != nil {
    log.Printf("Failed to register session: %v", err)
}

// Add session-specific tools
userSpecificTool := mcp.NewTool(
    "user_data",
    mcp.WithDescription("Access user-specific data"),
)
// You can use AddSessionTool (similar to AddTool)
err := s.AddSessionTool(
    advSession.SessionID(),
    userSpecificTool,
    func(ctx context.Context, req mcp.CallToolRequest) (*mcp.CallToolResult, error) {
        // This handler is only available to this specific session
        return mcp.NewToolResultText("User-specific data for " + advSession.SessionID()), nil
    },
)
if err != nil {
    log.Printf("Failed to add session tool: %v", err)
}

// Or use AddSessionTools directly with ServerTool
/*
err := s.AddSessionTools(
    advSession.SessionID(),
    server.ServerTool{
        Tool: userSpecificTool,
        Handler: func(ctx context.Context, req mcp.CallToolRequest) (*mcp.CallToolResult, error) {
            // This handler is only available to this specific session
            return mcp.NewToolResultText("User-specific data for " + advSession.SessionID()), nil
        },
    },
)
if err != nil {
    log.Printf("Failed to add session tool: %v", err)
}
*/

// Delete session-specific tools when no longer needed
err = s.DeleteSessionTools(advSession.SessionID(), "user_data")
if err != nil {
    log.Printf("Failed to delete session tool: %v", err)
}
```

#### 工具过滤

你还可以应用过滤器来控制特定会话可用的工具：

```go
// Add a tool filter that only shows tools with certain prefixes
s := server.NewMCPServer(
    "Tool Filtering Demo",
    "1.0.0",
    server.WithToolCapabilities(true),
    server.WithToolFilter(func(ctx context.Context, tools []mcp.Tool) []mcp.Tool {
        // Get session from context
        session := server.ClientSessionFromContext(ctx)
        if session == nil {
            return tools // Return all tools if no session
        }
        
        // Example: filter tools based on session ID prefix
        if strings.HasPrefix(session.SessionID(), "admin-") {
            // Admin users get all tools
            return tools
        } else {
            // Regular users only get tools with "public-" prefix
            var filteredTools []mcp.Tool
            for _, tool := range tools {
                if strings.HasPrefix(tool.Name, "public-") {
                    filteredTools = append(filteredTools, tool)
                }
            }
            return filteredTools
        }
    }),
)
```

#### 使用上下文（Context）

会话上下文会自动传递给工具和资源处理器：

```go
s.AddTool(mcp.NewTool("session_aware"), func(ctx context.Context, req mcp.CallToolRequest) (*mcp.CallToolResult, error) {
    // Get the current session from context
    session := server.ClientSessionFromContext(ctx)
    if session == nil {
        return mcp.NewToolResultError("No active session"), nil
    }
    
    return mcp.NewToolResultText("Hello, session " + session.SessionID()), nil
})

// When using handlers in HTTP/SSE servers, you need to pass the context with the session
httpHandler := func(w http.ResponseWriter, r *http.Request) {
    // Get session from somewhere (like a cookie or header)
    session := getSessionFromRequest(r)
    
    // Add session to context
    ctx := s.WithContext(r.Context(), session)
    
    // Use this context when handling requests
    // ...
}
```

</details>

### 请求钩子（Hooks）

通过创建包含你选择的回调函数的 `Hooks` 对象，可以拦截请求生命周期。这支持全功能的遥测数据收集，以及对各种事实的可观测性，例如统计格式不正确的请求数量，或在初始化期间记录代理身份。

在服务器创建时使用 `server.WithHooks` 选项添加 `Hooks`。

### 工具处理器中间件

使用 `server.WithToolHandlerMiddleware` 选项为工具调用处理器添加中间件。中间件可在服务器创建时注册，并应用于每次工具调用。

提供了一个恢复（recovery）中间件选项，用于从工具调用的 panic 中恢复，可通过 `server.WithRecovery` 选项添加到服务器。

### 提示词处理器中间件

使用 `server.WithPromptHandlerMiddleware` 选项为提示词处理器添加中间件。中间件可在服务器创建时注册，并应用于每次 `prompts/get` 调用。

### 提示词过滤

通过 `server.WithPromptFilter` 选项基于上下文过滤提示词。其工作方式与工具过滤相同，但作用于 `prompts/list` 结果。

### 重新生成服务器代码

服务器钩子和请求处理器是自动生成的。运行以下命令重新生成：

```bash
go generate ./...
```

你需要已安装 `go` 且系统中有 `goimports` 工具可用。生成器会自动运行 `goimports` 进行格式化和修复导入。

### 自动补全（Auto-completions）

当用户为特定提示词（按名称标识）或资源模板（按 URI 标识）填写参数值时，服务器可以提供上下文建议。
要启用补全支持，请在创建服务器时使用 `server.WithCompletions()` 选项。

#### 补全提供者（Completion Providers）

你可以通过实现相应的接口并将它们作为选项传递给服务器，为提示词参数和资源模板参数提供补全逻辑。

<details>
<summary>Show Completion Provider Examples</summary>

```go
type MyPromptCompletionProvider struct{}

func (p *MyPromptCompletionProvider) CompletePromptArgument(
    ctx context.Context,
    promptName string,
    argument mcp.CompleteArgument,
    context mcp.CompleteContext,
) (*mcp.Completion, error) {
    // Example: provide style suggestions for a "code_review" prompt
    if promptName == "code_review" && argument.Name == "style" {
        styles := []string{"formal", "casual", "technical", "creative"}
        var suggestions []string
        
        // Filter based on current input
        for _, style := range styles {
            if strings.HasPrefix(style, argument.Value) {
                suggestions = append(suggestions, style)
            }
        }
        
        return &mcp.Completion{
            Values: suggestions,
        }, nil
    }
    
    // Return empty suggestions for unhandled cases
    return &mcp.Completion{Values: []string{}}, nil
}

type MyResourceCompletionProvider struct{}

func (p *MyResourceCompletionProvider) CompleteResourceArgument(
    ctx context.Context,
    uri string,
    argument mcp.CompleteArgument,
    context mcp.CompleteContext,
) (*mcp.Completion, error) {
    // Example: provide file path completions
    if uri == "file:///{path}" && argument.Name == "path" {
        // You can access previously completed arguments from context.Arguments
        // context.Arguments is a map[string]string of already-resolved arguments
        
        paths := getMatchingPaths(argument.Value) // Your custom logic
        
        return &mcp.Completion{
            Values:  paths[:min(len(paths), 100)], // Max 100 items
            Total:   len(paths),                    // Total available matches
            HasMore: len(paths) > 100,              // More results available
        }, nil
    }
    
    return &mcp.Completion{Values: []string{}}, nil
}

// Register the provider
mcpServer := server.NewMCPServer(
    "my-server",
    "1.0.0",
    server.WithCompletions(),
    server.WithPromptCompletionProvider(&MyPromptCompletionProvider{}),
    server.WithResourceCompletionProvider(&MyResourceCompletionProvider{}),
)
```

</details>

#### 补全上下文

对于具有多个参数的提示词或资源模板，`CompleteContext` 参数提供了对已补全参数的访问权限。这允许你基于之前的选择提供上下文建议。

<details>
<summary>Show Completion Context Example</summary>

```go
func (p *MyProvider) CompleteResourceArgument(
    ctx context.Context,
    uri string,
    argument mcp.CompleteArgument,
    context mcp.CompleteContext,
) (*mcp.Completion, error) {
    // Access previously completed arguments
    if previousValue, ok := context.Arguments["previous_arg"]; ok {
        // Provide suggestions based on previous_arg value
        return getSuggestionsFor(argument.Value, previousValue), nil
    }
    
    return &mcp.Completion{Values: []string{}}, nil
}
```

</details>

#### 响应限制

返回补全结果时请注意：
- 每次响应最多包含 100 个项目
- 使用 `Total` 指示可用匹配的总数
- 使用 `HasMore` 指示返回值之外是否还有更多结果