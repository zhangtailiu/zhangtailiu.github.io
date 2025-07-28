# My Awesome Blog

This is a Hexo blog using the Tranquility theme. It is automatically deployed to GitHub Pages using GitHub Actions.

## 如何使用

### 新增博客文章

要创建一篇新的博客文章，请运行以下命令：

```bash
hexo new "你的文章标题"
```

这将在 `source/_posts` 目录下创建一个新的 Markdown 文件。你可以编辑此文件来撰写你的博客文章。

### 运行本地开发服务器

要在本地预览你的博客，请运行以下命令：

```bash
hexo server
```

这将在 `http://localhost:4000` 启动一个本地服务器。

### 部署博客

博客会自动部署到 GitHub Pages。每次你向 `main` 分支推送代码时，博客都会自动更新。部署过程由 `yarn deploy` 命令处理，该命令会将生成的静态文件推送到 `main` 分支。

## 主题

本博客使用 [Tranquility](https://github.com/hooozen/hexo-theme-tranquility) 主题。