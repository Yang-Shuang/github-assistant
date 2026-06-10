# Web Skills 技能图谱

<p align="center">
	Web Skills 是一份面向前端开发者的实用技能可视化概览。访问 <a href="https://andreasbm.github.io/web-skills" target="_blank" aria-label="Link to Web Skills">https://andreasbm.github.io/web-skills</a> 查看可视化图谱，或向下滚动本文件以列表形式浏览。如果你喜欢这个项目，非常欢迎成为 ⭐ Star 收藏者 🤩
</p> 
<p align="center">
	<a href="http://andreasbm.github.io/web-skills" target="_blank">
		<img src="https://raw.githubusercontent.com/andreasbm/web-skills/master/demo.gif" alt="Web Skills Demo" width="800" />
	</a>
</p>
<br />
<details>
<summary>📖 目录</summary>
<br />


[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#table-of-contents)



## ➤ 目录

* [➤ 常见问题解答 (FAQ)](#-faq)

	* [什么是 Web Skills？](#what-is-web-skills)

	* [你是如何选择这些技能的？](#how-did-you-choose-the-skills)

	* [我该如何支持你？](#how-can-i-support-you)

	* [我该如何参与贡献？](#how-can-i-get-involved)

	* [我该如何跟踪自己已掌握的技能？](#how-can-i-keep-track-of-what-skills-i-know)

	* [内容太多了，我感到 overwhelmed！帮帮我！](#i-am-overwhelmed-help-me)

	* [为什么没有包含 XYZ 技术？](#why-havent-you-included-xyz-technology)

	* “experimental”（实验性）标签是什么意思？](#what-does-the-experimental-banner-mean)

	* [如何与你取得联系？](#how-can-i-get-in-contact-with-you)

* [➤ 基础核心 (Fundamentals)](#-fundamentals)

	* [HTML](#html)

	* [语法 (Syntax)](#syntax)

		* [基础标签 (Basic Tags)](#basic-tags)

	* [表单 (Forms)](#forms)

	* [搜索引擎优化 (SEO)](#seo)

		* [可发现内容 (Discoverable Content)](#discoverable-content)

	* [SVG](#svg)

	* [最佳实践 (Best Practices)](#best-practices)

	* [CSS](#css)

	* [语法 (Syntax)](#syntax-1)

	* [选择器 (Selectors)](#selectors)

		* [特异性 (Specificity)](#specificity)

		* [伪类/伪元素选择器 (Pseudo Selectors)](#pseudo-selectors)

	* [盒模型 (Box Model)](#box-model)

		* [外边距折叠 (Margin Collapsing)](#margin-collapsing)

	* [颜色 (Colors)](#colors)

	* [`calc()` 函数](#calc)

	* [布局 (Layout)](#layout)

		* [Flexbox 弹性布局](#flex)

		* [Grid 网格布局](#grid)

	* [变换与动画 (Transforms & Animations)](#transforms)

		* [CSS 动画](#animations)

	* [响应式设计 (Responsive Design)](#responsive-design)

		* [媒体查询 (Media Queries)](#media-queries)

		* [相对单位 (Relative Units)](#relative-units)

		* [图片适配 (Images)](#images)

	* [CSS 变量](#css-variables)

	* [最佳实践 (Best Practices)](#best-practices-1)

	* [JavaScript](#javascript)

	* [语法 (Syntax)](#syntax-2)

		* [展开语法 (Spread)](#spread)

		* [解构赋值 (Destructuring)](#destructuring)

	* [DOM 操作](#dom)

		* [DOM 节点操作](#dom-manipulation)

	* [事件处理 (Events)](#events)

	* [对象 (Objects)](#objects)

		* [原型链 (Prototype)](#prototype)

			* [`class` 类语法](#classes)

	* [正则表达式 (Regex)](#regex)

	* [模板字符串 (Template Literals)](#template-literals)

	* [Promise 异步编程](#promises)

		* [回调函数 (Callbacks)](#callbacks)

		* [`async/await`](#asyncawait)

		* [`fetch` API](#fetch)

	* [Web Animations API](#web-animations)

	* [ES6 模块 (Modules)](#modules)

	* [`Intl` 国际化 API](#intl)

	* [`Canvas` 绘图](#canvas)

	* [文档编写 (Documentation)](#documentation)

	* [最佳实践 (Best Practices)](#best-practices-2)

	* [浏览器原理 (The Browser)](#the-browser)

	* [标准化组织 (Standardization)](#standardization)

		* [W3C](#w3c)

		* [TC39](#tc39)

		* [WHATWG](#whatwg)

		* [技术规范 (Specifications)](#specifications)

	* [浏览器引擎 (Browser Engines)](#browser-engines)

		* [Webkit](#webkit)

		* [Blink](#blink)

		* [Gecko](#gecko)

	* [HTTP 协议](#http)

	* [互联网基础 (The Internet)](#the-internet)

	* [Polyfill 兼容性填充](#polyfills)

	* [调试技巧 (Debugging)](#debugging)

		* [开发者控制台 (Developer console)](#developer-console)

* [➤ 无障碍访问 (Accessibility)](#-accessibility)

	* [为什么重要？(The why)](#the-why)

	* [屏幕阅读器 (Screen Readers)](#screen-readers)

	* [无障碍树 (Accessibility tree)](#accessibility-tree)

		* [ARIA](#aria)

		* [语义化 HTML](#accessible-html)

			* [`alt` 文本描述](#alt-text)

		* [无障碍 CSS](#accessible-css)

	* [无障碍表单 (Accessible forms)](#accessible-forms)

	* [UI 状态反馈 (UI States)](#ui-states)

	* [键盘可访问性 (Keyboard Accessibility)](#keyboard-accessibility)

		* [焦点管理 (Focus)](#focus)

	* [色彩对比度 (Accessible Colors)](#accessible-colors)

	* [法律法规与政策 (Laws & Policies)](#laws--policies)

		* [无障碍审计 (Audits)](#audits)

* [➤ Web Components 组件化](#-web-components)

	* [自定义元素 (Custom Elements)](#custom-elements)

	* [HTML 模板 (`<template>`)](#html-templates)

	* [Shadow DOM 影子 DOM](#shadow-dom)

		* [`::part` 阴影部分样式](#shadow-parts)

		* `<slot>` 插槽 (Slots)](#slots)

	* [最佳实践 (Best practices)](#best-practices)

	* [可构造样式表 (Constructible Stylesheets)](#constructible-stylesheets)

	* [表单参与机制 (Form Participation)](#form-participation)

* [➤ 渐进式 Web 应用 (Progressive Webapps)](#-progressive-webapps)

	* [APIs](#apis)

	* [数据存储 (Storage)](#storage)

	* [路由 (Routing)](#routing)

		* [`History API`](#history-api)

	* [Service Workers 服务工作者](#service-workers)

		* [离线优先 (Offline first)](#offline-first)

		* [推送通知 (Push notifications)](#push-notifications)

	* [Web App Manifest 应用清单](#web-app-manifest)

	* [添加到主屏幕 (Add to homescreen)](#add-to-homescreen)

	* [指针事件 (Pointer Events)](#pointer-events)

	* [加载性能优化 (Loading Performance)](#loading-performance)

	* [App Shell 应用外壳](#app-shell)

	* [渲染阻塞资源 (Render-Blocking Resources)](#render-blocking-resources)

	* [资源压缩 (Compression)](#compression)

	* [性能指标 (Performance metrics)](#performance-metrics)

		* [LCP - 最大内容绘制 (Largest Contentful Paint)](#largest-contentful-paint)

		* [TBT - 总阻塞时间 (Total Blocking Time)](#total-blocking-time)

		* [TTI - 可交互时间 (Time to Interactive)](#time-to-interactive)

	* [懒加载 (Lazy Loading)](#lazy-loading)

		* [`dynamic import()`](#dynamic-import)

		* [离屏图片优化 (Offscreen images)](#offscreen-images)

	* [关键请求链 (Critical Request Chains)](#critical-request-chains)

	* [Tree Shaking 摇树优化](#tree-shaking)

	* [代码分割 (Codesplitting)](#codesplitting)

	* [PRPL 模式](#prpl-pattern)

	* [资源优先级 (Resource Prioritization)](#resource-prioritization)

	* [缓存策略 (Caching)](#caching)

	* [渲染性能优化 (Rendering Performance)](#rendering-performance)

	* [渲染流程 (Rendering)](#rendering)

	* [事件循环 (Event loop)](#event-loop)

		* [微任务队列 (Microtask)](#microtask)

		* [调用栈 (Stack)](#stack)

		* [堆内存 (Heap)](#heap)

	* [RAIL 性能模型](#rail-model)

		* [`requestAnimationFrame`](#requestanimationframe)

		* [`requestIdleCallback`](#requestidlecallback)

	* [关键渲染路径 (Critical Rendering Path)](#critical-rendering-path)

	* [像素流水线 (The Pixel Pipeline)](#the-pixel-pipeline)

		* [样式计算](#style-calculations)

		* [变换与合成](#transforms-1)

		* [绘制区域优化 (Paint areas)](#paint-areas)

		* [布局重排/回流 (Layout Trashing)](#layout-trashing)

		* [图层提升 (Layers)](#layers)

		* [`debounce` 防抖](#debounce)

	* [`contain` CSS 属性](#css-containment)

	* [Web Workers 多线程](#web-workers)

	* [安全机制 (Security)](#security)

	* [HTTPS 加密传输](#https)

	* [浏览器沙箱 (Browser Sandbox)](#browser-sandbox)

	* [OWASP 安全标准](#owasp)

		* [跨站脚本攻击 XSS (Cross-Site Scripting)](#cross-site-scripting)

		* [点击劫持 (Clickjacking)](#clickjacking)

	* [内容安全策略 CSP (Content Security Policy)](#content-security-policy)

	* [性能审计 (Audits)](#audits-1)

	* [性能预算 (Performance budgets)](#performance-budgets)

	* [Lighthouse 性能检测](#lighthouse)

	* [Chrome DevTools 开发者工具](#chrome-devtools)

* [➤ 构建工具 (Build tools)](#-build-tools)

	* [包管理器 (Package Managers)](#package-managers)

		* [NPM](#npm)

		* [Yarn](#yarn)

	* [模块打包器 (Module Bundlers)](#module-bundlers)

		* [Rollup](#rollup)

		* [Webpack](#webpack)

		* [Parcel](#parcel)

		* [Snowpack](#snowpack)

	* [代码检查与格式化 (Linters and formatters)](#linters-and-formatters)

		* [Prettier](#prettier)

		* [ESLint](#eslint)

	* [任务运行器 (Task Runners)](#task-runners)

		* [NPM Scripts](#npm-scripts)

	* [代码转译器 (Transpilers)](#transpilers)

		* [Babel](#babel)

		* [TypeScript](#typescript)

	* [CSS 预处理器 (CSS Pre-processors)](#css-pre-processors)

		* [SASS/SCSS](#sass)

		* [PostCSS](#postcss)

	* [Node.js 运行时](#nodejs)

* [➤ 框架与库 (Frameworks & Libraries)](#-frameworks--libraries)

	* [lit-element](#lit-element)

	* [Vue](#vue)

	* [React](#react)

	* [Angular](#angular)

	* [Svelte](#svelte)

	* [Stencil](#stencil)

* [➤ 测试 (Testing)](#-testing)

	* [测试方法论 (Testing Methodologies)](#testing-methodologies)

		* [单元测试 (Unit Testing)](#unit-testing)

		* [集成测试 (Integration Testing)](#integration-testing)

		* [系统测试 (System Testing)](#system-testing)

		* [验收测试 (Acceptance Testing)](#acceptance-testing)

		* [冒烟测试 (Smoke Testing)](#smoke-testing)

		* [性能测试 (Performance Testing)](#performance-testing)

		* [可用性测试 (Usability Testing)](#usability-testing)

		* [白盒测试 (White Box Testing)](#white-box-testing)

		* [黑盒测试 (Black Box Testing)](#black-box-testing)

		* [自动化测试 (Automated Testing)](#automated-testing)

		* [手动测试 (Manual Testing)](#manual-testing)

	* [持续集成 (Continuous integration)](#continuous-integration)

	* [A/B 测试](#ab-testing)

	* [测试运行器 (Test Runners)](#test-runners)

		* [Karma](#karma)

		* [Mocha](#mocha)

		* [Jasmine](#jasmine)

		* [Cypress](#cypress)

		* [Ava](#ava)

	* [最佳实践 (Best Practices)](#best-practices-3)

* [➤ 架构与范式 (Architecture & paradigms)](#-architecture--paradigms)

	* [编程范式概述 (Paradigms)](#paradigms)

	* [面向对象编程 (Object Oriented Programming)](#object-oriented-programming)

		* [S.O.L.I.D 原则](#solid)

	* [函数式编程 (Functional programming)](#functional-programming)

		* [递归 (Recursion)](#recursion)

		* [高阶函数 (Higher-Order Functions)](#higher-order-functions)

		* [柯里化 (Currying)](#currying)

		* [单子模式 (Monads)](#monads)

	* [设计架构 (Architecture)](#architecture)

	* [设计模式 (Design Patterns)](#design-patterns)

		* [单例模式 (Singleton)](#singleton)

		* [观察者模式 (Observer)](#observer)

		* [原型模式 (Prototype)](#prototype-1)

		* [桥接模式 (Bridge)](#bridge)

		* [代理模式 (Proxy)](#proxy)

		* [责任链模式 (Chain of responsibility)](#chain-of-responsibility)

		* [构造器模式 (Constructor)](#constructor)

	* [CSS 架构方法论 (CSS Methodologies)](#css-methodologies)

		* [BEM](#bem)

		* [SMACSS](#smacss)

		* [OOCSS](#oocss)

* [➤ 团队协作 (Team Collaboration)](#-team-collaboration)

	* [版本控制 (Version Control)](#version-control)

	* [Git](#git)

		* [Github](#github)

		* [Bitbucket](#bitbucket)

	* [项目管理 (Management)](#management)

	* [敏捷开发 (Agile Development)](#agile-development)

		* [Scrum 框架](#scrum)

		* [看板管理 (Kanban)](#kanban)

	* [瀑布模型 (Waterfall Development)](#waterfall-development)

	* [测试驱动开发 TDD (Test Driven Development)](#test-driven-development)

* [➤ 设计与用户体验 (Design & UX)](#-design--ux)

	* [色彩理论 (Color Theory)](#color-theory)

		* [色轮 (Color Wheel)](#color-wheel)

	* [排版设计 (Typography)](#typography)

		* [字体大小 (Font Size)](#font-size)

		* [行间距 (Line Spacing)](#line-spacing)

	* [CRAP 设计原则](#crap)

		* [对比度 (Contrast)](#contrast)

		* [重复性 (Repetition)](#repetition)

		* [对齐 (Alignment)](#alignment)

		* [ proximity/邻近性 (Proximity)](#proximity)

	* [一致性 (Consistency)](#consistency)

	* [间距控制 (Spacing)](#spacing)

	* [错误处理 UX (Error Handling)](#error-handling)

	* [加载状态设计 (Loading)](#loading)

	* [黄金比例 (The Golden Ratio)](#the-golden-ratio)

	* [移动端优先 (Mobile First)](#mobile-first)

		* [触控热区/点击目标 (Hit Targets)](#hit-targets)

	* [设计系统 (Design Systems)](#design-systems)

		* [Material Design](#material-design)

		* [Fluent Design](#fluent-design)

	* [无障碍设计 (Accessibility)](#accessibility)

	* [最佳实践 (Best Practices)](#best-practices-4)

* [➤ 现代 Web API (The Modern Web)](#-the-modern-web)

	* [数据流/Streams](#streams)

		* [媒体流 (Media Streams)](#media-streams)

		* [`MediaRecorder` 录制器](#media-recorder)

		* [WebRTC](#web-rtc)

		* [屏幕捕获 (Screen Capture)](#screen-capture)

		* [生成器函数 (Generators)](#generators)

	* [语音合成 API (Speech Synthesis)](#speech-synthesis)

	* [WebSocket 长连接](#web-sockets)

	* [地理定位 API (Geolocation)](#geolocation)

	* [设备方向与运动传感器 (Device orientation & motion)](#device-orientation--motion)

	* [全屏 API (Fullscreen)](#fullscreen)

	* [可变字体 (Variable Fonts)](#variable-fonts)

	* [HTTP/2 协议](#http2)

	* [`Payment Request` 支付请求 API](#payment-request-api)

	* [Web Audio 音频处理](#web-audio)

	* [观察者模式 API (Observers)](#observers)

		* [`MutationObserver`](#mutation-observer)

		* [`IntersectionObserver`](#intersection-observer)

		* [`ResizeObserver`](#resize-observer)

		* [`PerformanceObserver`](#performance-observer)

	* [滚动吸附 (Scrollsnapping)](#scrollsnapping)

	* [WebAssembly](#web-assembly)

	* [`Beacon` 信标 API](#beacon)

	* [剪贴板 API (Clipboard)](#clipboard)

	* [分享 API (Share)](#share)

	* [性能指标 API (Performance API)](#performance-api)

	* [游戏手柄 API (Gamepad API)](#gamepad-api)

	* [语音识别 API (Speech Recognition)](#speech-recognition)

	* [交互媒体查询 (Interaction Media Queries)](#interaction-media-queries)

	* [浏览器扩展开发 (Browser Extensions)](#browser-extensions)

	* [`Pointer Lock` 指针锁定 API](#pointer-lock-api)

	* [画中画模式 (Picture In Picture)](#picture-in-picture)

	* [`Proxy` 代理对象](#proxies)

	* [Houdini CSS 实验特性](#houdini)

	* [Project Fugu 浏览器能力增强计划](#project-fugu)

	* [Web Authentication API (WebAuthn)](#web-authentication-api)

		* [`Credentials Manager` 凭证管理 API](#credentials-manager-api)

	* [原生文件系统 API (Native File System)](#native-file-system)

	* [形状检测 API (Shape Detection)](#shape-detection)

	* [Web Bluetooth 蓝牙 API](#web-bluetooth)

	* [Web USB API](#web-usb)

	* [Web XR 扩展现实 API](#web-xr)

	* [`Presentation` 投屏 API](#presentation)

	* [网络信息 API (Network Information API)](#network-information-api)

* [➤ 算法与数据结构 (Algorithms & Data structures)](#-algorithms--data-structures)

	* [数据结构概述 (Data structures)](#data-structures)

	* [数组 (Arrays)](#arrays)

	* [队列与栈 (Queues & Stacks)](#queues--stacks)

	* [树结构 (Trees)](#trees)

		* [二叉索引树/树状数组](#binary-indexed-tree)

		* [堆 (Heap)](#heap-1)

		* [红黑树 (Red-black Tree)](#red-black-tree)

		* [字典树/Trie](#trie)

		* [K-D 树 (K-D Tree)](#k-d-tree)

	* [哈希表 (Hash Tables)](#hash-tables)

	* [链表 (Linked Lists)](#linked-lists)

	* [图结构 (Graphs)](#graphs)

	* [算法分析 (Analysis)](#analysis)

	* [时间复杂度 (Time complexity)](#time-complexity)

		* [成本模型 (Cost model)](#cost-model)

		* [增长阶数 (Order of Growth)](#order-of-growth)

		* [大 O 表示法 (Big O notation)](#big-o-notation)

	* [空间复杂度 (Space Complexity)](#space-complexity)

	* [算法实现 (Algorithms)](#algorithms)

	* [排序算法 (Sorting)](#sorting)

		* [插入排序](#insertion-sort)

		* [快速排序 (Quicksort)](#quicksort)

		* [归并排序 (Mergesort)](#mergesort)

		* [堆排序 (Heapsort)](#heapsort)

	* [查找算法 (Searching)](#searching)

		* [二分搜索](#binary-search)

		* [广度优先搜索 BFS](#breadth-first-search)

		* [深度优先搜索 DFS](#depth-first-search)

		* [迪杰斯特拉算法 Dijkstra's Algorithm](#dijkstras-algorithm)

		* [字符串匹配/搜索 (String Search)](#string-search)

	* [哈希算法 (Hashing)](#hashing)

* [➤ 数据库与服务器 (Databases & Servers)](#-databases--servers)

	* [数据库概述 (Databases)](#databases)

	* [关系型数据库 (Relational Databases)](#relational-databases)

		* [SQL](#sql)

		* [MySQL](#mysql)

		* [PostgreSQL](#postgresql)

	* [非关系型数据库/NoSQL (Non-relational Databases)](#non-relational-databases)

		* [Redis](#redis)

		* [MongoDB](#mongodb)

	* [数据建模 (Data Modelling)](#data-modelling)

		* [ER 实体关系图 (ER Diagram)](#er-diagram)

		* [数据库键/Keys](#keys)

	* [索引优化 (Indexing)](#indexing)

	* [数据完整性 (Data Integrity)](#data-integrity)

	* [范式与规范化 (Normalization)](#normalization)

		* [函数依赖 (Functional Dependencies)](#functional-dependencies)

		* [数据库范式 (Normal Forms)](#normal-forms)

	* [事务管理 (Transactions)](#transactions)

		* [ACID 特性](#acid)

		* [可串行化 (Serializability)](#serializability)

		* [锁机制 (Locks)](#locks)

			* [死锁 (Deadlocks)](#deadlocks)

		* [优先图/前导图 (Precedence graph)](#precedence-graph)

	* [服务器架构 (Servers)](#servers)

	* [架构模式 (Architectural Models)](#architectural-models)

		* [客户端-服务端模型 (Client-Server)](#client-server)

		* [代理服务器 (Proxy Server)](#proxy-server)

		* [点对点网络 P2P (Peer-To-Peer)](#peer-to-peer)

	* [中间件 (Middleware)](#middleware)

	* [请求-响应协议 (Request-Reply Protocol)](#request-reply-protocol)

		* [UDP](#udp)

		* [TCP](#tcp)

	* [REST API 设计规范](#rest-api)

		* [CRUD 操作](#crud)

	* [Express.js 框架](#express)

	* [GraphQL 查询语言](#graphql)

	* [GNU/Linux 操作系统](#gnulinux)

	* [Docker 容器化](#docker)

	* [SSH 安全远程连接](#ssh)

* [➤ 贡献者 (Contributors)](#-contributors)

* [➤ 开源协议 (License)](#-license)
</details>



[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#faq)



## ➤ 常见问题解答 (FAQ)

### Web Skills 是什么？

Web Skills 是一份面向前端开发者的实用技能可视化概览。它适合刚开始学习前端开发的初学者，也适合从业多年想要拓展知识面的资深开发者。作为新手，我建议你不要把它当作一份“必须掌握”的绝对清单，而应视为一个可以探索的学习地图和起点。这些技能是按照我推荐的学习路径大致按顺序排列的，当然你也可以自由跳转。

### 你是如何选择这些技能的？
		
这些技能结合了本人 10 年的开发经验、软件工程学士学位背景，以及我个人在日常工作中认为最实用的知识点。因此，你可能会发现其中缺少了很多内容。例如，我不是 PHP 开发者——正因如此，PHP 并未包含在内。如果你是 PHP 开发者，这份图谱的呈现方式可能会完全不同。

### 我该如何支持你？

我利用业余时间免费构建 Web Skills，目的是帮助更多人进入前端开发领域。我的动力来源于大家觉得这个项目有用。如果你喜欢这个作品，欢迎以任何你喜欢的方式支持我！例如，非常欢迎你成为 [⭐ Star 收藏者](https://github.com/andreasbm/web-skills/stargazers)，将 Web Skills 分享给朋友和关注者，或者撰写博客文章并链接到本项目。如果你愿意，[请我喝杯咖啡 ☕](https://www.buymeacoffee.com/AndreasMehlsen) 绝对会让我开心一整天！<3

### 我该如何参与贡献？

欢迎以任何你喜欢的方式参与进来。你可以前往 [Issues 页面](https://github.com/andreasbm/web-skills/issues) 帮我修复拼写错误、提交 Bug 或建议新功能。任何形式的参与我都非常感谢！

### 我该如何跟踪自己已掌握的技能？
在页面底部，你会看到一个标有“Sign in with Google”（使用 Google 登录）的按钮。点击并登录后，你就可以将技能标记为已完成。

### 内容太多了，我感到 overwhelmed！帮帮我！

我非常理解面对这么多技能时产生的焦虑感——但我可以向你保证，这份概览包含的内容远远超过大多数人实际需要的量。我的主要目标是提供一个前端开发的可视化全景图，激发大家深入学习的热情。作为开发者，我最热爱的一点就是不断掌握新技能。我认为身处一个可以终身学习、永远有新东西可学的领域是非常棒的！没有人能成为这张表上所有技能的专家，所以请尝试找到你最感兴趣的方向，并把它做到极致。

### 为什么没有包含 XYZ 技术？
这些技能是基于我个人在日常工作中认为最实用的标准筛选的。如果你觉得某项重要技术缺失了，随时可以在 [Issues 页面](https://github.com/andreasbm/web-skills/issues) 提出建议。

### “experimental”（实验性）标签是什么意思？
当一项技能被标记为“experimental”时，意味着该技术尚不成熟，目前正处于向 Web 平台添加的过程中（或正在考虑中）。在任何生产项目中引入实验性技术前请谨慎评估。Web Skills 使用的定义参考了 [MDN](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Conventions_definitions#Experimental) 上优秀的分类标准。如果你发现某项技能应该被标记为“experimental”或移除该标签，欢迎提交 Issue。

### 如何与你取得联系？
你可以通过 Twitter [@AndreasMehlsen](https://twitter.com/AndreasMehlsen) 联系我，或者访问 [我的个人网站](https://andreasbm.github.io) 了解更多我正在参与的项目。



[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#fundamentals)



## ➤ 基础核心 (Fundamentals)

### HTML

### 语法 (Syntax)
学习 HTML 基础知识，熟悉其语法和核心概念。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTML 基础](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTML 入门](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.codecademy.com" alt="Logo" /> Codecademy - 学习 HTML](https://www.codecademy.com/learn/learn-html)



#### 基础标签 (Basic Tags)
熟悉常用的 HTML 基础标签

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTML 元素参考](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.tutorialspoint.com" alt="Logo" /> Tutorialspoint - HTML 基础标签](https://www.tutorialspoint.com/html/html_basic_tags.htm)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.elated.com" alt="Logo" /> Elated - 前 10 个 HTML 标签](https://www.elated.com/first-10-html-tags/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - HTML 标签参考](https://www.w3schools.com/tags/ref_byfunc.asp)



### 表单 (Forms)
学习如何设计高效的表单，进行有效验证，并为用户提供清晰的反馈。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTML 表单](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Web - 表单设计](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - 表单](https://www.w3schools.com/html/html_forms.asp)



### 搜索引擎优化 (SEO)
学习如何让你的内容更容易被搜索引擎发现。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fweb.dev" alt="Logo" /> web.dev - 可被发现性](https://web.dev/discoverable)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Search - 入门指南](https://developers.google.com/search/docs/guides/get-started)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Search - SEO 基础](https://developers.google.com/search/docs/guides/javascript-seo-basics)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fweb.dev" alt="Logo" /> web.dev - SEO 审计](https://web.dev/lighthouse-seo)



#### 可发现内容 (Discoverable Content)
学习如何结构化 HTML，以便在社交媒体或搜索引擎分享时提供丰富的预览体验。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Web - 社交发现](https://developers.google.com/web/fundamentals/discovery/social-discovery)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Search - 搜索功能特性](https://developers.google.com/search/docs/guides/search-features)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Search - 结构化数据](https://developers.google.com/search/docs/guides/intro-structured-data)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fweb.dev" alt="Logo" /> web.dev - 易于发现](https://web.dev/discoverable)



### SVG
学习如何使用 SVG 文件，确保图形在所有屏幕分辨率下都保持清晰锐利。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 将矢量图形添加到 Web](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fsvgontheweb.com" alt="Logo" /> SVG on the web](https://svgontheweb.com/)



### 最佳实践 (Best Practices)
学习编写 HTML 的最佳实践。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTML 编码规范](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Code_guidelines/HTML)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - HTML 编码约定](https://www.w3schools.com/html/html5_syntax.asp)





### CSS

### 语法 (Syntax)
学习 CSS 基础知识，熟悉其语法和核心概念。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 基础](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 教程](https://www.w3schools.com/css/default.asp)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.youtube.com" alt="Logo" /> Supercharged - CSS 选择器](https://www.youtube.com/watch?v=IKho_xDKaLw)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 第一步](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 构建块](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 值与单位](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 语法](https://developer.mozilla.org/en-US/docs/Web/CSS/Syntax)



### 选择器 (Selectors)
学习 CSS 选择器，掌握如何高效定位 DOM 元素。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 选择器](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 所有选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 子元素与兄弟选择器](https://css-tricks.com/child-and-sibling-selectors/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 所有选择器速查](https://css-tricks.com/almanac/selectors/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 组合器](https://www.w3schools.com/css/css_combinators.asp)



#### 特异性 (Specificity)
学习什么是选择器优先级（特异性），以及如何在编写 CSS 时正确使用它。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 特异性](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 层叠与继承](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> dev.to - CSS 特异性详解](https://dev.to/emmawedekind/css-specificity-1kca)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fspecificity.keegan.st" alt="Logo" /> 特异性计算器](https://specificity.keegan.st/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 特异性](https://www.w3schools.com/css/css_specificity.asp)



#### 伪类/伪元素选择器 (Pseudo Selectors)
学习如何使用伪类和伪元素。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 伪类](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 认识伪类选择器](https://css-tricks.com/pseudo-class-selectors/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fbitsofco.de" alt="Logo" /> `:hover`、`:focus` 和 `:active` 伪类何时生效？](https://bitsofco.de/when-do-the-hover-focus-and-active-pseudo-classes-apply/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 伪元素](https://www.w3schools.com/css/css_pseudo_elements.asp)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 伪类](https://www.w3schools.com/css/css_pseudo_classes.asp)



### 盒模型 (Box Model)
学习 CSS 盒模型的基本概念。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 基础盒模型介绍](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 盒模型详解](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 继承 `box-sizing`](https://css-tricks.com/inheriting-box-sizing-probably-slightly-better-best-practice/)



#### 外边距折叠 (Margin Collapsing)
学习关于外边距折叠（Margin Collapse）的机制。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 精通外边距折叠](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> CSS 外边距折叠：是什么、为什么以及如何解决](https://medium.com/@joseph0crick/margin-collapse-in-css-what-why-and-how-328c10e37ca0)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 你必须知道的折叠外边距](https://css-tricks.com/what-you-should-know-about-collapsing-margins/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fbitsofco.de" alt="Logo" /> 折叠外边距到底是怎么回事？](https://bitsofco.de/collapsible-margins/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjonathan-harrell.com" alt="Logo" /> 外边距折叠的真相](https://jonathan-harrell.com/whats-the-deal-with-margin-collapse/)



### 颜色 (Colors)
学习在 CSS 中定义颜色的不同方式。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - color](https://developer.mozilla.org/en-US/docs/Web/CSS/color)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - `<color>`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 颜色](https://www.w3schools.com/css/css_colors.asp)



### `calc()` 函数
学习如何使用 CSS 的 `calc()` 函数进行动态计算。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Calc](https://developer.mozilla.org/en-US/docs/Web/CSS/calc)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - `calc()` 的实用场景](https://css-tricks.com/a-couple-of-use-cases-for-calc/)



### 布局 (Layout)
学习 Web 中不同的布局类型。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Chrome Dev - 基础布局](https://developers.google.com/training/certification/mobile-web-specialist/study-guide/basic-layout)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - CSS 网站布局](https://www.w3schools.com/css/css_website_layout.asp)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 文档与网站结构](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 布局](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout)



#### Flexbox 弹性布局
学习如何使用 Flexbox 创建响应式布局。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Flexbox](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> Flexbox 完全指南](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fflexboxfroggy.com" alt="Logo" /> Flexbox Froggy (互动练习)](https://flexboxfroggy.com/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=http%3A%2F%2Fflexboxdefense.com" alt="Logo" /> Flexbox Defense (游戏化学习)](http://flexboxdefense.com)



#### Grid 网格布局
学习如何使用 CSS Grid 创建二维布局。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Grids](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Grids)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Grid 完全指南](https://css-tricks.com/snippets/css/complete-guide-grid/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcssgridgarden.com" alt="Logo" /> CSS Grid Garden (互动练习)](https://cssgridgarden.com/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.youtube.com" alt="Logo" /> Supercharged - CSS Grids](https://www.youtube.com/watch?v=AqwPrR7hklE)



### 变换与动画 (Transforms & Animations)
学习通过 CSS 对元素进行变形和动画处理。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - Transform](https://css-tricks.com/almanac/properties/t/transform/)



#### CSS 动画
学习如何使用关键帧（keyframes）通过 CSS 制作元素动画。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 使用 CSS 动画](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - Animation](https://css-tricks.com/almanac/properties/a/animation/)



### 响应式设计 (Responsive Design)
学习如何让网站在不同屏幕尺寸下自适应显示。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 响应式设计](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.udacity.com" alt="Logo" /> Google - 响应式 Web 设计基础](https://www.udacity.com/course/responsive-web-design-fundamentals--ud893)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Dev - 响应式设计](https://developers.google.com/web/fundamentals/design-and-ux/responsive)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Dev - UX 模式](https://developers.google.com/web/fundamentals/design-and-ux/responsive/patterns)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Dev - 响应式内容](https://developers.google.com/web/fundamentals/design-and-ux/responsive/content)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcodelabs.developers.google.com" alt="Logo" /> Codelabs - 响应式设计](https://codelabs.developers.google.com/codelabs/pwa-responsive-design/index.html?index=..%2F..dev-pwa-training#0)



#### 媒体查询 (Media Queries)
学习如何使用媒体查询构建响应式布局。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - CSS 媒体查询与可用空间](https://css-tricks.com/css-media-queries/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 使用媒体查询](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 使用媒体查询实现无障碍](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_Media_Queries_for_Accessibility)



#### 相对单位 (Relative Units)
学习如何在字体大小和间距等属性中使用相对单位。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 尺寸设置](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Sizing_items_in_CSS)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 值与单位](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fthecssworkshop.com" alt="Logo" /> The CSS Workshop - 相对单位](https://thecssworkshop.com/lessons/relative-units)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - 玩转视口单位](https://css-tricks.com/fun-viewport-units/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> dev.to - 15 种 CSS 相对单位](https://dev.to/bytegasm/15-css-relative-units-how-many-do-you-know-em-rem-ex-cap-ch-ic-6m)



#### 图片适配 (Images)
学习如何使图片响应式显示，始终根据屏幕尺寸展示最佳版本。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - 响应式图片](https://developers.google.com/web/fundamentals/design-and-ux/responsive/images)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 响应式图片](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)



### CSS 变量
学习如何定义和使用 CSS 自定义属性（CSS Variables）。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 使用 CSS 自定义属性](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - CSS 变量：为什么你应该关心？](https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> dev.to - CSS Quickies: CSS 变量](https://dev.to/lampewebdev/css-quickies-css-variables-or-how-you-create-a-white-dark-theme-easily-1i0i)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcodeburst.io" alt="Logo" /> CSS 变量详解（含 5 个示例）](https://codeburst.io/css-variables-explained-with-5-examples-84adaffaa5bd)



### 最佳实践 (Best Practices)
学习编写 CSS 的最佳实践。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CSS 编码规范](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Code_guidelines/CSS)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 组织你的 CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fspeckyboy.com" alt="Logo" /> Speckyboy - CSS 好坏实践对比](https://speckyboy.com/good-bad-css-practices/)





### JavaScript

### 语法 (Syntax)
学习 JavaScript 基础知识，熟悉其语法和核心概念。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - JavaScript 第一步](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - JavaScript 基础](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - JavaScript 构建块](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks)



#### 展开语法 (Spread)
学习如何使用展开语法（`...`）处理数组。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.freecodecamp.org" alt="Logo" /> Freecodecamp - Spread 语法入门](https://www.freecodecamp.org/news/an-introduction-to-spread-syntax-in-javascript-fba39595922c/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fv8.dev" alt="Logo" /> V8 - 对象剩余与展开属性](https://v8.dev/features/object-rest-spread)



#### 解构赋值 (Destructuring)
学习如何使用解构语法处理对象和数组。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fhacks.mozilla.org" alt="Logo" /> MDN - ES6 In Depth: Destructuring](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjavascript.info" alt="Logo" /> javascript.info - Destructuring assignment](https://javascript.info/destructuring-assignment)



### DOM
学习 HTML 如何被表示为对象，以及文档的结构和内容是如何构成的。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - DOM 简介](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.freecodecamp.org" alt="Logo" /> Freecodecamp - 什么是 DOM？](https://www.freecodecamp.org/news/whats-the-document-object-model-and-why-you-should-know-how-to-use-it-1a2d0bc5429d/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Flearn.co" alt="Logo" /> DOM 入门](https://learn.co/lessons/introduction-to-the-dom)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fhtmldom.dev" alt="Logo" /> htmldom.dev](https://htmldom.dev/)



#### DOM 节点操作 (DOM Manipulation)
学习如何通过 JavaScript 查询和操作 HTML 元素。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 使用选择器定位 DOM 元素](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.youtube.com" alt="Logo" /> Supercharged - querySelector](https://www.youtube.com/watch?v=s0vg_H9hBuU)



### 事件处理 (Events)
学习如何派发和监听事件。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 事件入门](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 创建和触发事件](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> JavaScript 中的事件冒泡与捕获](https://medium.com/@vsvaibhav2016/event-bubbling-and-event-capturing-in-javascript-6ff38bec30e)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.freecodecamp.org" alt="Logo" /> Freecodecamp - JavaScript 事件传播简化指南](https://www.freecodecamp.org/news/a-simplified-explanation-of-event-propagation-in-javascript-f9de7961a06e/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fflaviocopes.com" alt="Logo" /> JavaScript Events Explained](https://flaviocopes.com/javascript-events/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - removeEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.quirksmode.org" alt="Logo" /> Event order](https://www.quirksmode.org/js/events_order.html)



### 对象 (Objects)
学习如何创建和使用 JavaScript 对象。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 认识 JavaScript 对象](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - 操作对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjavascript.info" alt="Logo" /> javascript.info - Objects](https://javascript.info/object)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - this 关键字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> W3Schools - JavaScript this Keyword](https://www.w3schools.com/js/js_this.asp)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - bind()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - new 运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - new.target](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fscotch.io" alt="Logo" /> Data Structures: Objects and Arrays](https://scotch.io/courses/10-need-to-know-javascript-concepts/data-structures-objects-and-arrays)



#### 原型链 (Prototype)
学习如何通过原型扩展对象和函数。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> The prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> Prototypes in JavaScript](https://medium.com/better-programming/prototypes-in-javascript-5bba2990e04b)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> dev.to - JavaScript Visualized: Prototypal Inheritance](https://dev.to/lydiahallie/javascript-visualized-prototypal-inheritance-47co)



##### `class` 类语法 (Classes)
学习如何定义和使用 ES6 Class。熟悉面向对象概念，如继承和封装。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> Medium - ES6 Classes](https://medium.com/@luke_smaki/javascript-es6-classes-8a34b0a6720a)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Inheritance](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Object Oriented Programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - super](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super)



### 正则表达式 (Regex)
学习如何使用正则表达式从字符串中提取信息。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjavascript.info" alt="Logo" /> javascript.info - Regular expressions](https://javascript.info/regular-expressions)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)



### 模板字符串 (Template Literals)
学习如何使用模板字符串和 Tagged Templates 操作字符串。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fhacks.mozilla.org" alt="Logo" /> MDN - ES6 In Depth: Template strings](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - Getting Literal With ES6 Template Strings](https://developers.google.com/web/updates/2015/01/ES6-Template-Strings)



### Promise 异步编程 (Promises)
学习如何使用 Promise，理解什么是异步代码。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - JavaScript Promises: an Introduction](https://developers.google.com/web/fundamentals/primers/promises)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> Master the JavaScript Interview: What is a Promise?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261)



#### 回调函数 (Callbacks)
学习如何使用回调，以及为什么它们并不总是最佳选择。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Callback function](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcodeburst.io" alt="Logo" /> JavaScript: What the heck is a Callback?](https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjavascript.info" alt="Logo" /> javascript.info - Callbacks](https://javascript.info/callbacks)



#### `async/await`
学习如何使用 `async` 和 `await` 关键字简化异步代码编写。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - Async functions](https://developers.google.com/web/fundamentals/primers/async-functions)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjavascript.info" alt="Logo" /> javascript.info - Async/await](https://javascript.info/async-await)



#### `fetch` API
学习如何使用 Fetch API 获取数据。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - Introduction to fetch](https://developers.google.com/web/updates/2015/03/introduction-to-fetch)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - Networking](https://developers.google.com/training/certification/mobile-web-specialist/study-guide/networking)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.freecodecamp.org" alt="Logo" /> Freecodecamp - Fetch 实用指南](https://www.freecodecamp.org/news/a-practical-es6-guide-on-how-to-perform-http-requests-using-the-fetch-api-594c3d91a547/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Falligator.io" alt="Logo" /> Alligator - Fetch API](https://alligator.io/js/fetch-api/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.youtube.com" alt="Logo" /> Supercharged - Fetch](https://www.youtube.com/watch?v=GiI77ya60yk)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcodelabs.developers.google.com" alt="Logo" /> Codelabs - Fetch](https://codelabs.developers.google.com/codelabs/pwa-fetch/index.html?index=..%2F..dev-pwa-training#0)



### Web Animations API
学习如何使用 Web Animations API 对 DOM 元素进行动画处理。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdevelopers.google.com" alt="Logo" /> Google Devs - Animations](https://developers.google.com/web/fundamentals/design-and-ux/animations)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Using The Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - CSS Animations vs Web Animations API](https://css-tricks.com/css-animations-vs-web-animations-api/)



### ES6 模块 (Modules)
学习如何使用 `export` 和 `import` 关键字将代码模块化。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fv8.dev" alt="Logo" /> V8 - Modules](https://v8.dev/features/modules)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.freecodecamp.org" alt="Logo" /> Freecodecamp - ES6 模块实用指南](https://www.freecodecamp.org/news/how-to-use-es6-modules-and-why-theyre-important-a9b20b480773/)



### `Intl` 国际化 API
学习如何使用 `Intl` API 实现网站本地化。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Date Time Format](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fblog.bitsrc.io" alt="Logo" /> New Intl APIs in JavaScript](https://blog.bitsrc.io/new-intl-apis-in-javascript-c50dc89d2cf3)



### `Canvas` 绘图
学习如何在 Canvas 上绘制图形。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Canvas tutorial](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcss-tricks.com" alt="Logo" /> CSS Tricks - Manipulating Pixels Using Canvas](https://css-tricks.com/manipulating-pixels-using-canvas/)



### 文档编写 (Documentation)
学习如何编写高质量的代码文档及其重要性。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fjsdoc.app" alt="Logo" /> Getting Started with JSDoc](https://jsdoc.app/about-getting-started.html)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.writethedocs.org" alt="Logo" /> A beginner’s guide to writing documentation](https://www.writethedocs.org/guide/writing/beginners-guide-to-docs/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fhackernoon.com" alt="Logo" /> Write Good Documentation](https://hackernoon.com/write-good-documentation-6caffb9082b4)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> The power of jsDoc](https://dev.to/gmartigny/the-power-of-jsdoc-272d)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdev.to" alt="Logo" /> Document your Javascript code with JSDoc](https://dev.to/paulasantamaria/document-your-javascript-code-with-jsdoc-2fbf)



### 最佳实践 (Best Practices)
学习编写 JavaScript 的最佳实践。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - JavaScript guidelines](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Code_guidelines/JavaScript)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fgithub.com" alt="Logo" /> Airbnb - JavaScript Style Guide](https://github.com/airbnb/javascript)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fgithub.com" alt="Logo" /> Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fcodeburst.io" alt="Logo" /> 5 JavaScript Style Guides including Airbnb, GitHub & Google](https://codeburst.io/5-javascript-style-guides-including-airbnb-github-google-88cbc6b2b7aa)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3schools.com" alt="Logo" /> JavaScript Style Guide and Coding Conventions](https://www.w3schools.com/js/js_conventions.asp)





### 浏览器原理 (The Browser)

### 标准化组织 (Standardization)
学习为什么 Web 标准很重要，以及新规范是如何标准化的。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Wikipedia - Web Standards](https://en.wikipedia.org/wiki/Web_standards)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.elcom.com.au" alt="Logo" /> What Are Web Standards?](https://www.elcom.com.au/resources/blog/web-standards)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Frobertnyman.com" alt="Logo" /> A Comprehensive Explanation of Web Standards](https://robertnyman.com/2007/05/21/what-are-web-standards-a-comprehensive-explanation-of-what-is-comprised-in-the-term/)



#### W3C
了解 W3C 的工作及其如何推动 Web 发展。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3.org" alt="Logo" /> W3C - About](https://www.w3.org/standards/about.html)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3.org" alt="Logo" /> W3C - Standards](https://www.w3.org/standards/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=http%3A%2F%2Fwebdiy.org" alt="Logo" /> W3C - Process](http://webdiy.org/w3c/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.smashingmagazine.com" alt="Logo" /> Web Standards Guide](https://www.smashingmagazine.com/2019/01/web-standards-guide/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3.org" alt="Logo" /> W3C - Groups](https://www.w3.org/community/groups/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.smashingmagazine.com" alt="Logo" /> The W3C At Twenty-Five](https://www.smashingmagazine.com/2019/10/happy-birthday-w3c/)



#### TC39
了解 TC39 的工作及其如何推动 JavaScript 语言发展。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2F2ality.com" alt="Logo" /> The TC39 process for ECMAScript features](https://2ality.com/2015/11/tc39-process.html)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fgithub.com" alt="Logo" /> Github - TC39](https://github.com/tc39)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.ecma-international.org" alt="Logo" /> Ecma International - Programme of work](https://www.ecma-international.org/memento/tc39.htm)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Wikipedia - Ecma International](https://en.wikipedia.org/wiki/Ecma_International)



#### WHATWG
了解 WHATWG 的工作及其如何推动 Web HTML/CSS/DOM 标准发展。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwhatwg.org" alt="Logo" /> WHATWG - FAQ](https://whatwg.org/faq)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fspec.whatwg.org" alt="Logo" /> WHATWG - Standards](https://spec.whatwg.org/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - WHATWG](https://developer.mozilla.org/en-US/docs/Glossary/WHATWG)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdzone.com" alt="Logo" /> W3C vs. WHATWG HTML5 Specs](https://dzone.com/articles/w3c-vs-whatwg-html5-specs)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fhtml.spec.whatwg.org" alt="Logo" /> WHATWG - HTML](https://html.spec.whatwg.org/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Wikipedia - WHATWG](https://en.wikipedia.org/wiki/WHATWG)



#### 技术规范 (Specifications)
学习如何阅读标准化组织发布的技术规范文档。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Ftimothygu.me" alt="Logo" /> How to Read the ECMAScript Specification](https://timothygu.me/es-howto/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Falistapart.com" alt="Logo" /> How to Read W3C Specs](https://alistapart.com/article/readspec/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.chenhuijing.com" alt="Logo" /> Learning CSS by reading specs](https://www.chenhuijing.com/blog/learning-css-by-reading-specifications/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.w3.org" alt="Logo" /> Understanding the CSS Specifications](https://www.w3.org/Style/CSS/read.en.html)



### 浏览器引擎 (Browser Engines)
了解什么是浏览器引擎，以及当前浏览器生态和市场占有率概况。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fmedium.com" alt="Logo" /> Medium - Browser Engines](https://medium.com/@jonbiro/browser-engines-chromium-v8-blink-gecko-webkit-98d6b0490968)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Wikipedia - Comparison](https://en.wikipedia.org/wiki/Comparison_of_browser_engines)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.html5rocks.com" alt="Logo" /> HTML5 Rocks - How Browsers Work](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Ftextslashplain.com" alt="Logo" /> Demystifying Browsers](https://textslashplain.com/2020/02/09/demystifying-browsers/)



#### Webkit
了解 Webkit 浏览器引擎。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwebkit.org" alt="Logo" /> Webkit](https://webkit.org/)



#### Blink
了解 Blink 浏览器引擎（Chrome, Edge, Opera 等使用）。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Blink](https://en.wikipedia.org/wiki/Blink_(browser_engine))



#### Gecko
了解 Gecko 浏览器引擎（Firefox 使用）。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Gecko](https://en.wikipedia.org/wiki/Gecko_(software))



### HTTP 协议
学习数据如何通过 HTTP 协议进行分发。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - HTTP Glossary](https://developer.mozilla.org/en-US/docs/Glossary/HTTP)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - An overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fen.wikipedia.org" alt="Logo" /> Wikipedia - Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)



### 互联网基础 (The Internet)
学习互联网是如何工作的。

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fdeveloper.mozilla.org" alt="Logo" /> MDN - How does the Internet work?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/How_does_the_Internet_work)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.youtube.com" alt="Logo" /> Youtube - How the Internet Works in 5 Minutes](https://www.youtube.com/watch?v=7_LPdttKXPc)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fwww.explainthatstuff.com" alt="Logo" /> Explain That Stuff - Internet](https://www.explainthatstuff.com/internet.html)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fweb.stanford.edu" alt="Logo" /> Stanford - How Does the Internet Work?](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm)

* [ ] [<img style="margin-bottom: 0;" src="https://plus.google.com/_/favicon?domain_url=https%3A%2F%2Fblog.hubspot.com" alt="Logo" /> How the Internet Works](https://blog.hub