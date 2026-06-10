# 软件开发者作品集 ⚡️ [![GitHub](https://img.shields.io/github/license/saadpasta/developer-portfolio?color=blue)](https://github.com/saadpasta/developerFolio/blob/master/LICENSE) [![GitHub stars](https://img.shields.io/github/stars/saadpasta/developerFolio)](https://github.com/saadpasta/developerFolio/stargazers)  [![All Contributors](https://img.shields.io/badge/all_contributors-4-orange.svg?style=flat-square)](#contributors)

## 一款简洁、美观且响应式的开发者作品集模板！


<p align="center">
  <kbd>
<img src="https://user.githubusercontent.com/53429438/106779355-e9cd9e80-666c-11eb-9417-8a4b54441bc6.gif"></img>
  </kbd>
</p>


只需修改 `src/portfolio.js` 即可生成你的个人作品集。通过在 `src/_globalColor.scss` 文件中自定义全局颜色方案来定制主题。你可以直接使用，也可以按需进行个性化调整。

如果你想**贡献**代码并让该项目对其他用户更有用，请查看 [Issues](https://github.com/saadpasta/developerFolio/issues)。

为你的 Fork 版本创建了很棒的功能或组件想分享吗？欢迎提交 [pull request（合并请求）](https://github.com/saadpasta/developerFolio/pulls)。

## 目录
- [功能模块](#sections)
- [环境准备](#getting-started)
- [使用方法](#how-to-use)
- [将作品集关联至 GitHub](#linking-portfolio-to-github)
- [将博客模块关联至 Medium](#linking-blogs-section-to-medium)
- [按需修改与自定义各模块](#change-and-customize-every-section-according-to-your-need)
- [部署](#deployment)
- [使用技术](#technologies-used)
- [插图资源](#illustrations)
- [未来计划](#for-the-future)
- [贡献者](#contributors)

## 功能模块
✔️ 摘要与自我介绍\
✔️ 技能\
✔️ 教育背景\
✔️ 工作经历\
✔️ 关联 GitHub 的开源项目\
✔️ 大型项目\
✔️ 成就与认证 🏆\
✔️ 博客文章\
✔️ 演讲记录\
✔️ 播客节目\
✔️ 联系我\
✔️ Twitter 时间线\
✔️ GitHub 个人资料

查看在线演示，**[点击此处](https://developerfolio.js.org/)。


## 环境准备

这些说明将帮助你在本地机器上获取并运行项目副本，以便进行开发和测试。

你的电脑上需要安装 [Git](https://git-scm.com) 和 [Node.js](https://nodejs.org/en/download/)（自带 [npm](http://npmjs.com)），或者使用 [Docker](https://www.docker.com/products/docker-desktop)。

```
node@v10.16.0 or higher
npm@6.9.0 or higher
git@2.17.1 or higher
```
### Docker 命令

```
1) BUILD IMAGE : docker build -t developerfolio:latest .
2) RUN IMAGE: docker run -t -p 3000:3000 developerfolio:latest
```


## 使用方法 

在命令行中，克隆并运行 developerFolio：

```bash
# Clone this repository
git clone https://github.com/saadpasta/developerFolio.git

# Go into the repository
cd developerFolio

# Setup default environment variables

# For Linux
cp env.example .env
# For Windows
copy env.example .env

# Install dependencies
npm install

# Start a local dev server
npm start
```

## 将作品集关联至 GitHub

按照以下[说明](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic)生成一个经典的 GitHub 个人访问令牌（确保不要选择任何权限范围，只需生成一个简单的令牌即可）。如果你使用 [GitHub Actions](#configuring-github-actions-recommended) 部署作品集，可以跳过此部分。

1. 在项目根目录创建一个名为 `.env` 的文件（如果在[使用方法](#how-to-use)章节中已完成则无需重复）

注意：强烈建议在部署前配置环境变量，因为某些组件依赖于 API 数据。 

```bash
- DeveloperFolio
  - node_modules
  - public
  - src
  - .env         <-- create it here
  - env.example  <-- this is the base file
  - .gitignore
  - package-lock.json
  - package.json
```

2. 在 `.env` 文件中添加键 `REACT_APP_GITHUB_TOKEN` 并填入你的 GitHub 令牌，同时添加用户名作为 `GITHUB_USERNAME`：

```env
// .env
REACT_APP_GITHUB_TOKEN = "YOUR GITHUB TOKEN HERE"
GITHUB_USERNAME = "YOUR GITHUB USERNAME"
USE_GITHUB_DATA = "true"
```

将 `showGithubProfile` 设置为 true 或 false 以控制是否通过 GitHub 显示联系资料，默认为 false。

**警告：** 请像对待密码一样妥善保管你的令牌。在使用 API 时，请将令牌作为环境变量使用，切勿硬编码到程序中。

注意：“开源项目”模块仅显示你 GitHub 资料中置顶的项目。如果你看到如下错误提示，请按照以下[说明](https://docs.github.com/en/enterprise/2.13/user/articles/pinning-items-to-your-profile)操作。

![ERROR](https://i.imgur.com/Hj6mu1K.png)

如果上述方法仍无效，请访问 [Wiki 页面](https://github.com/saadpasta/developerFolio/wiki/Github-Setup-For-Open-Source-Projects)。

## 将博客模块关联至 Medium

可选地，你可以将博客模块关联到你的 Medium 账号：

* 在 `.env` 文件中添加键 `MEDIUM_USERNAME` 并填入你的 Medium 用户名：

```env
// .env
MEDIUM_USERNAME = "YOUR MEDIUM USERNAME"
```

* 对于 GitHub Actions，请在 `.github/workflows/deploy.yml` 中修改变量 `MEDIUM_USERNAME`。

在 portfolio.js 中将 `displayMediumBlogs` 设置为 true 或 false 以控制是否显示获取的 Medium 博客，默认为 true。

## 按需修改与自定义各模块。

#### 个性化页面内容
在 `/src/portfolio.js` 中个性化页面内容，并根据你的需求进行修改。你还需要修改 `index.html` 以更改标题和元数据，从而为你的个人作品集提供准确的 SEO 支持。

```javascript
/* Change this file to get your Personal Porfolio */

const greeting = {
  /* Your Summary And Greeting Section */
  title: "Hi all I'm Saad",
  subTitle: emoji("A passionate Full Stack Software Developer 🚀"),
  resumeLink: "https://drive.google.com/file/d/1ofFdKF_mqscH8WvXkSObnVvC9kK7Ldlu/view?usp=sharing"
};

const socialMediaLinks = {
  /* Your Social Media Link */
  github: "https://github.com/saadpasta",
  linkedin: "https://www.linkedin.com/in/saadpasta/",
  gmail: "saadpasta70@gmail.com",
  gitlab: "https://gitlab.com/saadpasta",
  facebook: "https://www.facebook.com/saad.pasta7"
};


const skillsSection = { .... }

const techStack = { .... }

const workExperience = { .... }

const openSource = { .... }

const bigProjects = { .... }

const achievementSection = { .... }

const blogSection = { .... }

const contactInfo = { .... }

const twitterDetails = { ... }

```
#### 上传简历
要上传你自己的简历，只需将 PDF 文件上传至 `src/containers/greeting/resume` 并重命名为 `resume.pdf`。 

#### 使用表情符号

要在 Portfolio.js 的文本中添加表情符号 😃，请使用 `emoji()` 函数并将所需文本作为参数传入。这有助于确保表情符号在不同浏览器和平台上的兼容性。

#### 自定义 Lottie 动画

你可以从 [此类网站](https://lottiefiles.com/) 选择并下载 JSON 格式的 Lottie 动画。在 `src/assets/lottie` 中，用相同文件名替换你想修改的 Lottie JSON 文件。若要更改 Lottie 选项，请前往 `src/components/displayLottie/DisplayLottie.js` 修改 `defaultOptions` 对象，关于该对象的更多信息可参考 [lottie-react 文档](https://www.npmjs.com/package/lottie-react)。

#### 在页面中添加 Twitter 时间线
将你的 Twitter 用户名插入到 portfolio.js 中即可在页面上展示你的近期动态。

```javascript
const twitterDetails = {
  userName : "Your Twitter Username"
};
```
注意：添加用户名时请勿使用 `@` 符号。

## 部署
完成设置后，你应该将网站托管到线上。
我们强烈建议通读 React 的 [GitHub Pages 部署文档](https://create-react-app.dev/docs/deployment/#github-pages)。

#### 配置 GitHub Actions（推荐）
首先，你需要为所使用的仓库启用 GitHub Actions。

GitHub 的个人资料和仓库信息仅在部署时生成，如果需要更新这些信息则需要重新部署站点。因此，我们设置了一个可配置的 [CRON Job（定时任务）](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#scheduled-events)，每周自动部署一次你的站点，这样当你更新了 GitHub 个人资料后，作品集就会同步显示。你也可以通过 `workflow_dispatch` 事件手动触发部署，详见[此指南](https://github.blog/changelog/2020-07-06-github-actions-manual-triggers-with-workflow_dispatch)。

- 完成配置后，我们强烈建议通读 [GitHub Actions 工作流配置文档](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow)。

#### 部署到 GitHub Pages

本节将指导你将作品集部署到 GitHub Pages。

- 打开 `package.json`，将 `homepage` 变量中的 `https://developerfolio.js.org/` 替换为你的域名。例如，若希望站点地址为 `https://<your-username>.github.io/developerFolio`，请在 `package.json` 的 homepage 字段中填入相同内容。

- 简而言之，你也可以在 `package.json` 中添加 `/devloperFolio`（两者完全相同）。这样操作后，你是在告诉 `create-react-app` 相应地添加路径资源。

- （可选）配置域名。你可以通过在 `public/` 文件夹中添加 `CNAME` 文件来为 GitHub Pages 配置自定义域名。

- 按照官方 CRA 文档中的指南完成设置：[此处](https://create-react-app.dev/docs/deployment/#github-pages)。

#### 部署到 Netlify

你也可以直接通过 Netlify 托管，只需链接你自己的仓库即可。

[![Deploy To Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/saadpasta/developerFolio)

更多信息请阅读 [Netlify 托管指南](https://create-react-app.dev/docs/deployment/#netlify)。


## 使用技术 

- [React](https://reactjs.org/)
- [graphql](https://graphql.org/)
- [apollo-boost](https://www.apollographql.com/docs/react/get-started/)
- [react-twitter-embed](https://github.com/saurabhnemade/react-twitter-embed)
- [react-easy-emoji](https://github.com/appfigures/react-easy-emoji)
- [react-headroom](https://github.com/KyleAMathews/react-headroom)
- [color-thief](https://github.com/lokesh/color-thief)

## 插图资源
- [UnDraw](https://undraw.co/illustrations)
- [Lottie by Oblikweare](https://lottiefiles.com/oblikweare)


## 未来计划
如果你能帮助我们完成以下工作，请随时提交 [pull request（合并请求）](https://github.com/saadpasta/developerFolio/pulls)。

- 对接 LinkedIn API 以获取摘要、技能、教育和工作经历数据

- 迁移至 Gatsby 框架

- 增加更多功能模块

## 项目维护者 

<table>
  <tr>
    <td align="center"><a href="http://saadpasta.github.io"><img src="https://avatars2.githubusercontent.com/u/23307811?v=4" width="100px;" alt=""/><br /><sub><b>Saad Pasta</b></sub></a></td>
    <td align="center"><a href="https://github.com/kartikcho"><img src="https://avatars1.githubusercontent.com/u/48270786?v=4" width="100px;" alt=""/><br /><sub><b>Kartik Choudhary</b></sub></a></td>
    <td align="center"><a href="https://github.com/naveen521kk"><img src="https://avatars1.githubusercontent.com/u/49693820?v=4" width="100px;" alt=""/><br /><sub><b>Naveen M K</b></sub></a></td>
    <td align="center"><a href="http://www.muhammadhasham.com"><img src="https://avatars0.githubusercontent.com/u/17927649?v=4" width="100px;" alt=""/><br /><sub><b>Muhammad Hasham</b></sub></a></td>
  </tr>
</table>

## 贡献者 

感谢以下精彩人士 ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="http://facebook.com/9inpachi"><img src="https://avatars2.githubusercontent.com/u/36920441?v=4?s=100" width="100px;" alt="Fawad Ali"/><br /><sub><b>Fawad Ali</b></sub></a><br /><a href="#ideas-9inpachi" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/saadpasta/developerFolio/commits?author=9inpachi" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://dasunnavoda.wordpress.com/"><img src="https://avatars0.githubusercontent.com/u/5556085?v=4?s=100" width="100px;" alt="Dasun Navoda"/><br /><sub><b>Dasun Navoda</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=IamDZN" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://brian.teeman.net"><img src="https://avatars3.githubusercontent.com/u/1296369?v=4?s=100" width="100px;" alt="Brian Teeman"/><br /><sub><b>Brian Teeman</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=brianteeman" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://rajkumaar.co.in"><img src="https://avatars1.githubusercontent.com/u/37476886?v=4?s=100" width="100px;" alt="Rajkumar S"/><br /><sub><b>Rajkumar S</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=rajkumaar23" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/viveksharmaui"><img src="https://avatars1.githubusercontent.com/u/28563357?v=4?s=100" width="100px;" alt="Slim Coder"/><br /><sub><b>Slim Coder</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=viveksharmaui" title="Code">💻</a> <a href="https://github.com/saadpasta/developerFolio/commits?author=viveksharmaui" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://msayyaf.com"><img src="https://avatars3.githubusercontent.com/u/22149734?v=4?s=100" width="100px;" alt="Mohamed Sayyaf"/><br /><sub><b>Mohamed Sayyaf</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=msayyaf1" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://ashutosh1919.github.io"><img src="https://avatars3.githubusercontent.com/u/20843596?v=4?s=100" width="100px;" alt="Ashutosh Hathidara"/><br /><sub><b>Ashutosh Hathidara</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=ashutosh1919" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.upwork.com/freelancers/~01d10c23d4ffe3c658"><img src="https://avatars0.githubusercontent.com/u/8683960?v=4?s=100" width="100px;" alt="Rizwan Jamal ⚡️"/><br /><sub><b>Rizwan Jamal ⚡️</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Rizwanjamal" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://www.muhammadhasham.com"><img src="https://avatars0.githubusercontent.com/u/17927649?v=4?s=100" width="100px;" alt="Muhammad Hasham"/><br /><sub><b>Muhammad Hasham</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=MohammadHasham" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://sourcerer.io/joshiujjawal22"><img src="https://avatars3.githubusercontent.com/u/44023234?v=4?s=100" width="100px;" alt="UJJAWAL JOSHI"/><br /><sub><b>UJJAWAL JOSHI</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=joshiujjawal22" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/palak-sethi"><img src="https://avatars2.githubusercontent.com/u/51605219?v=4?s=100" width="100px;" alt="Palak Sethi"/><br /><sub><b>Palak Sethi</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=palak-sethi" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://viniciusbds.github.io/"><img src="https://avatars3.githubusercontent.com/u/34755896?v=4?s=100" width="100px;" alt="Vinicius Barbosa"/><br /><sub><b>Vinicius Barbosa</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=viniciusbds" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://bharatkammakatla.github.io"><img src="https://avatars1.githubusercontent.com/u/28840761?v=4?s=100" width="100px;" alt="Bharat Kammakatla"/><br /><sub><b>Bharat Kammakatla</b></sub></a><br /><a href="#design-BharatKammakatla" title="Design">🎨</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://bit.ly/garimasingh"><img src="https://avatars2.githubusercontent.com/u/44302373?v=4?s=100" width="100px;" alt="Garima Singh"/><br /><sub><b>Garima Singh</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=garimasingh128" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/HenryHengZJ"><img src="https://avatars2.githubusercontent.com/u/26460777?v=4?s=100" width="100px;" alt="Henry Heng"/><br /><sub><b>Henry Heng</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=HenryHengZJ" title="Code">💻</a> <a href="#design-HenryHengZJ" title="Design">🎨</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/PulkitBanta"><img src="https://avatars2.githubusercontent.com/u/43134750?v=4?s=100" width="100px;" alt="Pulkit Banta"/><br /><sub><b>Pulkit Banta</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=PulkitBanta" title="Code">💻</a> <a href="https://github.com/saadpasta/developerFolio/issues?q=author%3APulkitBanta" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/AkshayCHD"><img src="https://avatars1.githubusercontent.com/u/25455546?v=4?s=100" width="100px;" alt="Akshay Kumar"/><br /><sub><b>Akshay Kumar</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=AkshayCHD" title="Code">💻</a> <a href="https://github.com/saadpasta/developerFolio/issues?q=author%3AAkshayCHD" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/AmnaEjaz"><img src="https://avatars3.githubusercontent.com/u/14257959?v=4?s=100" width="100px;" alt="Amna Ejaz"/><br /><sub><b>Amna Ejaz</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=AmnaEjaz" title="Code">💻</a> <a href="#ideas-AmnaEjaz" title="Ideas, Planning, & Feedback">🤔</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/parasnagpal"><img src="https://avatars0.githubusercontent.com/u/39419139?v=4?s=100" width="100px;" alt="Paras Nagpal"/><br /><sub><b>Paras Nagpal</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=parasnagpal" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://sourcerer.io/sparsh-99"><img src="https://avatars0.githubusercontent.com/u/56729873?v=4?s=100" width="100px;" alt="Sparsh Garg"/><br /><sub><b>Sparsh Garg</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=sparsh-99" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://aashutosh.dev"><img src="https://avatars2.githubusercontent.com/u/21199234?v=4?s=100" width="100px;" alt="Aashutosh Rathi"/><br /><sub><b>Aashutosh Rathi</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=aashutoshrathi" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://abhishekashyap.studio/"><img src="https://avatars3.githubusercontent.com/u/29458374?v=4?s=100" width="100px;" alt="Abhishek Kashyap"/><br /><sub><b>Abhishek Kashyap</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3Aabhishekashyap" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/lcsvcn"><img src="https://avatars1.githubusercontent.com/u/6011385?v=4?s=100" width="100px;" alt="Lucas V C Nicolau"/><br /><sub><b>Lucas V C Nicolau</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=lcsvcn" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://bradleycherrin.com"><img src="https://avatars0.githubusercontent.com/u/5648785?v=4?s=100" width="100px;" alt="Bradley C. Herrin"/><br /><sub><b>Bradley C. Herrin</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=bradleycherrin" title="Documentation">📖</a> <a href="#ideas-bradleycherrin" title="Ideas, Planning, & Feedback">🤔</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://www.zekinahlecaros.com"><img src="https://avatars0.githubusercontent.com/u/43392346?v=4?s=100" width="100px;" alt="Zekinah Lecaros"/><br /><sub><b>Zekinah Lecaros</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=zekinah" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/vandana1499"><img src="https://avatars2.githubusercontent.com/u/29394600?v=4?s=100" width="100px;" alt="unbeat"/><br /><sub><b>unbeat</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=vandana1499" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/lARSHADl"><img src="https://avatars3.githubusercontent.com/u/45604332?v=4?s=100" width="100px;" alt="Arshad Ahmed"/><br /><sub><b>Arshad Ahmed</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=lARSHADl" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://xiaohuiliu.me"><img src="https://avatars1.githubusercontent.com/u/33507446?v=4?s=100" width="100px;" alt="Xiaohui Liu"/><br /><sub><b>Xiaohui Liu</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Ergouzii" title="Documentation">📖</a> <a href="https://github.com/saadpasta/developerFolio/commits?author=Ergouzii" title="Code">💻</a> <a href="#design-Ergouzii" title="Design">🎨</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://seungyeon-lee.github.io/"><img src="https://avatars1.githubusercontent.com/u/26589915?v=4?s=100" width="100px;" alt="Seungyeon-Lee"/><br /><sub><b>Seungyeon-Lee</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Seungyeon-Lee" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/NajamShehzad"><img src="https://avatars2.githubusercontent.com/u/37629243?v=4?s=100" width="100px;" alt="Najam Shehzad "/><br /><sub><b>Najam Shehzad </b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=NajamShehzad" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://www.exspiravit.ga/"><img src="https://avatars1.githubusercontent.com/u/22334680?v=4?s=100" width="100px;" alt="Randy Jesus Real Srsen"/><br /><sub><b>Randy Jesus Real Srsen</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Exspiravit" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://tamojitdas.netlify.app"><img src="https://avatars0.githubusercontent.com/u/40804626?v=4?s=100" width="100px;" alt="Tamojit Das"/><br /><sub><b>Tamojit Das</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=tamojit-123" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://warengonzaga.com"><img src="https://avatars1.githubusercontent.com/u/15052701?v=4?s=100" width="100px;" alt="Waren Gonzaga"/><br /><sub><b>Waren Gonzaga</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=WarenGonzaga" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://www.benjaminbourgeois.com"><img src="https://avatars3.githubusercontent.com/u/20949060?v=4?s=100" width="100px;" alt="Benjamin Bourgeois"/><br /><sub><b>Benjamin Bourgeois</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=BourgeoisBenjamin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://www.linkedin.com/in/keshavjain235"><img src="https://avatars2.githubusercontent.com/u/52530690?v=4?s=100" width="100px;" alt="Keshav Jain"/><br /><sub><b>Keshav Jain</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=keshavjain235" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://hanzla.ga"><img src="https://avatars.githubusercontent.com/u/59178380?v=4?s=100" width="100px;" alt="Hanzla"/><br /><sub><b>Hanzla</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=1hanzla100" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/yogeshhrathod"><img src="https://avatars.githubusercontent.com/u/46518134?v=4?s=100" width="100px;" alt="Yogesh Rathod"/><br /><sub><b>Yogesh Rathod</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=yogeshhrathod" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/AlKun25"><img src="https://avatars.githubusercontent.com/u/53429438?v=4?s=100" width="100px;" alt="Kunal Mundada"/><br /><sub><b>Kunal Mundada</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=AlKun25" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/jayhawk24"><img src="https://avatars.githubusercontent.com/u/38766415?v=4?s=100" width="100px;" alt="Anubhav Gupta"/><br /><sub><b>Anubhav Gupta</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=jayhawk24" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://vatsaldavevdwpblog.wordpress.com/"><img src="https://avatars.githubusercontent.com/u/42956495?v=4?s=100" width="100px;" alt="Vatsal Dave"/><br /><sub><b>Vatsal Dave</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=vatsaldaveVD" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://www.elvisciuffetelli.com"><img src="https://avatars.githubusercontent.com/u/35818757?v=4?s=100" width="100px;" alt="Elvis Ciuffetelli"/><br /><sub><b>Elvis Ciuffetelli</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=elvisciuffetelli" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://ScottJellen.com"><img src="https://avatars.githubusercontent.com/u/51421669?v=4?s=100" width="100px;" alt="Scott Jellen"/><br /><sub><b>Scott Jellen</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=SJellen" title="Code">💻</a> <a href="#design-SJellen" title="Design">🎨</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.linkedin.com/in/karthik-mohan-/"><img src="https://avatars.githubusercontent.com/u/25052382?v=4?s=100" width="100px;" alt="Karthik Mohan"/><br /><sub><b>Karthik Mohan</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3Akarthikmohan" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/mhowell11"><img src="https://avatars.githubusercontent.com/u/62813469?v=4?s=100" width="100px;" alt="mhowell11"/><br /><sub><b>mhowell11</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=mhowell11" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/gajanandh"><img src="https://avatars.githubusercontent.com/u/80502737?v=4?s=100" width="100px;" alt="gajanandh"/><br /><sub><b>gajanandh</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3Agajanandh" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/JooHyukKim"><img src="https://avatars.githubusercontent.com/u/61615301?v=4?s=100" width="100px;" alt="JooHyukKim"/><br /><sub><b>JooHyukKim</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=JooHyukKim" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://redheadphone.github.io/"><img src="https://avatars.githubusercontent.com/u/55500003?v=4?s=100" width="100px;" alt="Red Headphone"/><br /><sub><b>Red Headphone</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=RedHeadphone" title="Code">💻</a> <a href="https://github.com/saadpasta/developerFolio/issues?q=author%3ARedHeadphone" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://sunitroy2703.github.io"><img src="https://avatars.githubusercontent.com/u/67560900?v=4?s=100" width="100px;" alt="Sunit Roy"/><br /><sub><b>Sunit Roy</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3ASunitRoy2703" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/nayabatir1"><img src="https://avatars.githubusercontent.com/u/91016903?v=4?s=100" width="100px;" alt="Atir Nayab"/><br /><sub><b>Atir Nayab</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3Anayabatir1" title="Bug reports">🐛</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="http://thatdevsherry.pk"><img src="https://avatars.githubusercontent.com/u/40890226?v=4?s=100" width="100px;" alt="Shehriyar Qureshi"/><br /><sub><b>Shehriyar Qureshi</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=thatdevsherry" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Rispectech"><img src="https://avatars.githubusercontent.com/u/90450963?v=4?s=100" width="100px;" alt="respectech"/><br /><sub><b>respectech</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Rispectech" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://braydentw.com"><img src="https://avatars.githubusercontent.com/u/47185402?v=4?s=100" width="100px;" alt="Brayden"/><br /><sub><b>Brayden</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3ABraydenTW" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/CanciuCostin"><img src="https://avatars.githubusercontent.com/u/27332434?v=4?s=100" width="100px;" alt="Canciu Costin"/><br /><sub><b>Canciu Costin</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=CanciuCostin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/SpectralGT"><img src="https://avatars.githubusercontent.com/u/78777556?v=4?s=100" width="100px;" alt="Atharv Singh"/><br /><sub><b>Atharv Singh</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=SpectralGT" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://allishaan.co"><img src="https://avatars.githubusercontent.com/u/59707330?v=4?s=100" width="100px;" alt="Ishan Khandelwal"/><br /><sub><b>Ishan Khandelwal</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Ishan-001" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://slyapustin.com"><img src="https://avatars.githubusercontent.com/u/370774?v=4?s=100" width="100px;" alt="Sergey Lyapustin"/><br /><sub><b>Sergey Lyapustin</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=slyapustin" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.cam1pozas.xyz/"><img src="https://avatars.githubusercontent.com/u/89259499?v=4?s=100" width="100px;" alt="Camila Pozas"/><br /><sub><b>Camila Pozas</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=camipozas" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://saiteja13427.github.io"><img src="https://avatars.githubusercontent.com/u/40917760?v=4?s=100" width="100px;" alt="Sai Teja"/><br /><sub><b>Sai Teja</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/issues?q=author%3Asaiteja13427" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Vinitvh"><img src="https://avatars.githubusercontent.com/u/42197888?v=4?s=100" width="100px;" alt="Vinit Hemadri "/><br /><sub><b>Vinit Hemadri </b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Vinitvh" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Njong392"><img src="https://avatars.githubusercontent.com/u/81039882?v=4?s=100" width="100px;" alt="Njong Emy"/><br /><sub><b>Njong Emy</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Njong392" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://tamal.vercel.app/"><img src="https://avatars.githubusercontent.com/u/72851613?v=4?s=100" width="100px;" alt="Tamal Das "/><br /><sub><b>Tamal Das </b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=IAmTamal" title="Documentation">📖</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://dunsin.vercel.app"><img src="https://avatars.githubusercontent.com/u/78784850?v=4?s=100" width="100px;" alt="Dunsin"/><br /><sub><b>Dunsin</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=Dun-sin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/muneebahmedayub"><img src="https://avatars.githubusercontent.com/u/65030135?v=4?s=100" width="100px;" alt="Muneeb Ahmed"/><br /><sub><b>Muneeb Ahmed</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=muneebahmedayub" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://www.linkedin.com/in/qais-attarwala/"><img src="https://avatars.githubusercontent.com/u/52388168?v=4?s=100" width="100px;" alt="Qais Attarwala"/><br /><sub><b>Qais Attarwala</b></sub></a><br /><a href="https://github.com/saadpasta/developerFolio/commits?author=KazAttarwala" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---