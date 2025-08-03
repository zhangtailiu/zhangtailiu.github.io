---
title: Hexo 博客搭建指南：为后端开发者量身定制
date: 2024-01-01 10:00:00
tags:
  - Hexo
  - 博客
  - GitHub Pages
  - 前端
  - 部署
categories:
  - 技术
timeline: article
---

## Hexo 博客搭建指南：为后端开发者量身定制

你好！作为一名后端 Java 开发者，你可能更专注于服务器端逻辑和数据库，对前端和部署流程感到陌生。没关系，这篇指南将为你详细解析你的 Hexo 博客的技术栈、目录结构以及日常使用方法，让你轻松管理和发布你的内容。

### 1. 技术栈概览

你的博客是基于 **Hexo** 搭建的，这是一个快速、简洁且高效的静态博客框架。它利用 Markdown 编写文章，通过 Node.js 生成静态网页，然后你可以将这些网页部署到任何静态文件托管服务上，例如 **GitHub Pages**。

以下是你的博客所使用的主要技术：

*   **Hexo**: 核心的静态博客生成器。你用 Markdown 撰写文章，Hexo 会将其转换为 HTML、CSS 和 JavaScript 文件。
*   **Node.js & npm**: Hexo 是一个 Node.js 应用，`npm` (Node Package Manager) 是用于安装和管理 Hexo 及其插件的工具。
*   **Nunjucks**: 你的主题 `tranquility` 使用 Nunjucks 作为模板引擎。它允许主题开发者创建可重用的 HTML 模板，Hexo 在生成页面时会填充这些模板。
*   **Stylus**: 你的主题使用 Stylus 作为 CSS 预处理器。它提供了一些 CSS 不具备的特性（如变量、嵌套），使得 CSS 编写更高效。最终 Stylus 文件会被编译成普通的 CSS。
*   **Git & GitHub Pages**: Git 用于版本控制你的博客源文件，而 GitHub Pages 则是一个免费的静态网站托管服务，非常适合部署 Hexo 博客。你的博客通过 GitHub Actions 自动化部署到 GitHub Pages。

### 2. 项目目录结构解析

理解项目结构是高效管理博客的关键。以下是你博客项目中的一些重要目录和文件：

```
.
├── _config.yml             # Hexo 全局配置文件
├── package.json            # Node.js 项目配置文件，记录依赖
├── package-lock.json       # 锁定依赖版本
├── source/                 # 博客内容源文件
│   └── _posts/             # 你的博客文章（Markdown 文件）
│       └── hello-hexo.md
├── themes/                 # 存放 Hexo 主题
│   └── tranquility/        # 你当前使用的主题
│       ├── _config.yml     # 主题配置文件
│       ├── layout/         # Nunjucks 模板文件（.njk）
│       │   └── _partials/  # 局部模板
│       ├── source/         # 主题的静态资源
│       │   ├── css/        # Stylus 样式文件（.styl）
│       │   ├── font/       # 字体文件
│       │   └── images/     # 主题图片
│       └── ...
├── public/                 # Hexo 生成的静态网站文件（不要手动修改）
├── .deploy_git/            # Hexo deploy 命令使用的部署目录（如果你使用 GitHub Actions，这个目录可能不重要）
├── .github/                # GitHub 相关配置
│   └── workflows/
│       └── deploy.yml      # GitHub Actions 部署工作流配置
└── ...
```

*   **`_config.yml` (根目录)**: 这是 Hexo 的主配置文件。你可以在这里设置网站标题、URL、分页、主题等全局配置。
*   **`package.json`**: 类似于 Java 项目中的 `pom.xml` 或 `build.gradle`，它定义了项目的元数据和所有 Node.js 依赖。
*   **`source/_posts/`**: 这是你撰写所有博客文章的地方。每篇文章都是一个 Markdown (`.md`) 文件。
*   **`themes/tranquility/`**: 这是你的博客主题的目录。主题有自己的配置、布局和样式。
    *   **`themes/tranquility/_config.yml`**: 这是主题的配置文件，用于定制主题的特定功能和外观。
    *   **`themes/tranquility/layout/`**: 包含 Nunjucks 模板文件 (`.njk`)，它们定义了博客页面的结构。
    *   **`themes/tranquility/source/css/`**: 包含 Stylus 样式文件 (`.styl`)，它们定义了博客的视觉样式。这些文件会被编译成 CSS。
    *   **`themes/tranquility/source/images/`**: 存放主题使用的图片资源。
*   **`public/`**: 当你运行 `hexo generate` 命令时，Hexo 会将所有 Markdown 文件、模板和样式编译成静态 HTML、CSS 和 JavaScript 文件，并存放在这个目录中。**这个目录的内容是最终部署到 GitHub Pages 上的。**
*   **`.github/workflows/deploy.yml`**: 这是 GitHub Actions 的配置文件。它定义了一个自动化流程，当你的代码推送到 `main` 分支时，会自动构建你的 Hexo 博客并将其部署到 GitHub Pages。

### 3. 如何使用你的博客

#### 3.1 前提条件

确保你的开发环境中安装了：

*   **Node.js**: 建议使用 LTS (长期支持) 版本。
*   **npm**: 通常随 Node.js 一起安装。
*   **Git**: 用于版本控制和与 GitHub 交互。

#### 3.2 安装依赖

如果你是第一次克隆项目，或者 `node_modules` 目录被删除，你需要安装所有 Node.js 依赖：

```bash
npm install
```

#### 3.3 撰写新文章

要创建一篇新的博客文章，使用 Hexo 命令：

```bash
hexo new "你的文章标题"
```

这会在 `source/_posts/` 目录下创建一个新的 Markdown 文件，例如 `source/_posts/你的文章标题.md`。

打开这个文件，你会看到类似这样的内容（称为 Front-matter）：

```markdown
---
title: 你的文章标题
date: 2024-01-01 10:00:00 # 文章创建日期和时间
tags: # 标签，可以有多个
  - Hexo
  - 指南
categories: # 分类，可以有层级
  - 技术
---

# 这是你的文章正文

在这里使用 Markdown 语法撰写你的内容。

## Markdown 示例

*   列表项 1
*   列表项 2

**粗体文本**

`行内代码`

```java
// 代码块示例
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Hexo!");
    }
}
```

你可以在 `---` 之间的 Front-matter 中修改文章标题、日期、添加标签和分类。

#### 3.4 本地预览

在发布之前，你可以在本地预览你的博客，确保一切正常：

```bash
hexo server
```

运行此命令后，通常你可以在浏览器中访问 `http://localhost:4000` 来查看你的博客。当你修改文章内容或主题文件时，Hexo 会自动重新生成并刷新页面。

要停止本地服务器，在终端中按 `Ctrl + C`。

#### 3.5 生成静态文件

当你准备好部署时，你需要生成静态文件：

```bash
hexo generate
```

这个命令会清空 `public/` 目录，然后重新生成所有 HTML、CSS、JS 和图片文件。

#### 3.6 部署到 GitHub Pages (通过 GitHub Actions)

你的博客已经配置了 GitHub Actions 自动化部署。这意味着你不需要手动运行 `hexo deploy` 命令。

**部署流程：**

1.  **撰写和修改文章**：在 `source/_posts/` 中创建或编辑 Markdown 文件。
2.  **提交并推送**：将你的更改提交到 Git 仓库，并推送到 `main` 分支：
    ```bash
    git add .
    git commit -m "feat: 添加新文章或更新内容"
    git push origin main
    ```
3.  **GitHub Actions 自动部署**：一旦你推送到 `main` 分支，GitHub Actions 会自动检测到更改，并执行 `.github/workflows/deploy.yml` 中定义的工作流。
    *   它会拉取你的代码。
    *   安装 Node.js 依赖。
    *   运行 `hexo clean` 和 `hexo generate`。
    *   将生成的 `public` 目录内容推送到你的 GitHub Pages 仓库（`zhangtailiu/zhangtailiu.github.io`）。

你可以在你的 GitHub 仓库的 "Actions" 标签页中查看部署的进度和结果。

### 4. 主题定制与样式调整

你的博客使用了 `tranquility` 主题。如果你想修改主题的外观或行为：

*   **主题配置**: 修改 `themes/tranquility/_config.yml` 文件来调整主题的各种选项，例如导航菜单、社交链接、评论系统等。
*   **样式修改**: 如果你想深入修改样式，可以编辑 `themes/tranquility/source/css/` 目录下的 `.styl` 文件。修改后，Hexo 会自动重新编译为 CSS。

### 5. 常见问题与故障排除

*   **图片不显示**: 如果图片在本地显示正常，但部署后不显示，通常是路径问题。确保你的图片路径是相对于网站根目录的绝对路径（例如 `/images/my-image.png`），而不是相对路径（例如 `../images/my-image.png`）。Hexo 和你的主题通常会处理好这一点，但如果手动添加图片，请注意。
*   **部署后页面无变化**:
    *   **GitHub Actions 失败**: 检查 GitHub 仓库的 "Actions" 标签页，看部署工作流是否成功完成。
    *   **浏览器缓存**: 尝试清除浏览器缓存，或者使用无痕模式访问你的博客。
    *   **CDN 缓存**: 如果你使用了 CDN，可能需要等待 CDN 刷新缓存。
*   **`npm install` 失败**: 检查你的 Node.js 和 npm 版本是否与 `package.json` 中的要求兼容。尝试删除 `node_modules` 目录和 `package-lock.json` 文件，然后重新运行 `npm install`。

### 总结

希望这篇指南能帮助你更好地理解和管理你的 Hexo 博客。作为后端开发者，你已经掌握了强大的逻辑思维能力，相信你很快就能驾驭这个静态博客系统。尽情享受撰写和分享的乐趣吧！如果你有任何进一步的问题，随时可以提问。
