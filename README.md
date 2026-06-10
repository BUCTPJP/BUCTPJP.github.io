# PJP 随笔

这是一个基于 [Hexo](https://hexo.io/) 和 Butterfly 主题搭建的个人博客，主要用于记录教程、实验过程、技术笔记与资源整理。站点源码托管在 GitHub，并由 Vercel 从源码仓库自动构建和发布。

- 站点地址：<https://buctpjp-github-io.vercel.app>
- GitHub：<https://github.com/BUCTPJP>
- Hexo 版本：8.x
- Node.js 版本：20.x
- npm 版本：10.x

## 主要功能

- Markdown 文章写作与静态页面生成
- 文章分类、标签、归档和本地搜索
- 文章目录、代码高亮、深色模式和阅读模式
- 文章封面、独立资源目录与图片引用
- 响应式布局，适配桌面端和移动端
- GitHub 源码版本管理
- Vercel 自动构建、预览和线上发布
- 可选的 Hexo Git 部署到 GitHub Pages

## 技术栈

| 类型 | 技术 |
| --- | --- |
| 静态站点生成器 | Hexo 8 |
| 博客主题 | Butterfly |
| 内容格式 | Markdown |
| 模板与样式 | Pug、Stylus、CSS |
| 运行环境 | Node.js 20、npm 10 |
| 代码托管 | GitHub |
| 部署平台 | Vercel |

## 目录结构

```text
.
├─ source/
│  ├─ _posts/             # 博客文章和文章资源目录
│  ├─ about/              # 关于页面
│  ├─ archives/           # 归档页面
│  ├─ categories/         # 分类页面
│  ├─ tags/               # 标签页面
│  └─ css/custom.css      # 自定义样式
├─ scaffolds/             # Hexo 文章、页面和草稿模板
├─ themes/butterfly/      # Butterfly 主题
├─ _config.yml            # Hexo 主配置
├─ _config.butterfly.yml  # Butterfly 主题配置
└─ package.json           # 依赖和项目命令
```

`public/` 和 `db.json` 是 Hexo 构建时生成的内容，不应作为文章源码手动维护。

## 本地运行

### 1. 安装环境

安装 Node.js 20.x，进入项目目录后安装依赖：

```bash
npm install
```

### 2. 启动本地预览

```bash
npm run server
```

默认访问地址为 <http://localhost:4000>。修改文章后刷新页面即可检查排版、图片和链接。

### 3. 构建静态站点

```bash
npm run clean
npm run build
```

生成结果位于 `public/`。提交前建议至少执行一次构建，确认没有 Markdown、Front Matter 或资源路径错误。

## 文章写作

### 创建文章

可以使用 Hexo 命令：

```bash
npx hexo new post "文章标题"
```

也可以直接在 `source/_posts/` 下创建 Markdown 文件。推荐的 Front Matter：

```yaml
---
title: 文章标题
date: 2026-06-11 10:00:00
tags:
  - 标签
categories:
  - 教程
description: 用一句话概括文章内容
cover: ''
---
```

在文章摘要结束处添加：

```html
<!-- more -->
```

首页只展示该标记前的摘要，进入文章后显示全文。

### 上传和引用图片

项目已开启 `post_asset_folder: true`。建议让文章和图片使用同名目录：

```text
source/_posts/
├─ ZView2拟合EIS数据.md
└─ ZView2拟合EIS数据/
   ├─ 01-import-data.png
   └─ 02-fit-result.png
```

文章中使用相对路径：

```markdown
![导入数据](./ZView2拟合EIS数据/01-import-data.png)
```

图片建议使用 PNG、JPG 或 WebP；上传前压缩超大截图，并避免文件名包含空格和特殊符号。

## 同步到 GitHub

完成文章并通过本地构建后，将源码提交到 GitHub：

```bash
git status
git add source/_posts README.md
git commit -m "docs: add new blog post"
git push origin main
```

如果默认分支不是 `main`，将最后一条命令中的分支名替换为实际分支。提交前应检查 `git status`，避免把临时文件、软件安装包或隐私数据一并上传。

> `_config.yml` 中还配置了 `gh-pages` 部署目标。只有在安装并配置 `hexo-deployer-git` 后，`npm run deploy` 才会将生成站点发布到该分支。当前站点使用 Vercel 时，日常发布只需推送源码分支。

## Vercel 部署

### 首次配置

1. 登录 Vercel，选择 **Add New Project**。
2. 导入博客对应的 GitHub 仓库。
3. Framework Preset 选择 **Hexo**；若未自动识别，可使用以下配置：

| 配置项 | 值 |
| --- | --- |
| Install Command | `npm install` |
| Build Command | `npm run build` |
| Output Directory | `public` |
| Node.js Version | `20.x` |

4. 点击部署，完成后将生产域名填写到 `_config.yml` 的 `url` 字段。

### 日常发布

源码推送到 Vercel 绑定的生产分支后，Vercel 会自动执行安装和构建，并更新线上站点。其他分支或 Pull Request 通常会生成独立预览地址，适合发布前检查。

发布链路如下：

```text
撰写 Markdown
  -> 本地预览与构建
  -> Git 提交
  -> 推送 GitHub
  -> Vercel 自动构建
  -> 更新线上站点
```

## 常用命令

| 命令 | 作用 |
| --- | --- |
| `npm run server` | 启动本地预览 |
| `npm run clean` | 清理 Hexo 缓存和生成目录 |
| `npm run build` | 生成静态站点 |
| `npm run deploy` | 按 `_config.yml` 的 deploy 配置部署 |
| `npx hexo new post "标题"` | 创建新文章 |

## 发布检查清单

- Front Matter 格式正确，日期、标签和分类已填写
- `<!-- more -->` 放在合适的摘要位置
- 图片全部位于文章资源目录，链接可以正常显示
- 外部链接可以访问，敏感信息已移除
- `npm run clean && npm run build` 执行成功
- 本地预览的桌面端和移动端排版正常
- Git 提交只包含本次需要发布的文件

