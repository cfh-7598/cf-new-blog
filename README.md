# 我的博客（Hugo + PaperMod + Cloudflare Pages）

## 本地预览

1. 安装 Hugo（extended 版）：
   - macOS（Homebrew）：
     ```bash
     brew install hugo
     hugo version
     ```
     确保输出包含 `extended`。

2. 启动本地预览：
   ```bash
   hugo server -D
   ```
   访问 `http://localhost:1313`

> 本仓库通过 Hugo Modules 引入 PaperMod 主题，无需 git submodule。

## 目录说明

- `config.toml`：站点配置（主题、参数、模块等）
- `content/posts/`：你的文章目录
- `archetypes/`：文章模板
- `public/`：构建输出（被忽略）

## 写作

新建文章（草稿）：
```bash
hugo new posts/my-first-post.md
```
把文件头部的 `draft: true` 改为 `draft: false` 以发布。

## GitHub 与 Cloudflare Pages 部署

1. 推送到 GitHub
   ```bash
   git init
   git add .
   git commit -m "Init blog with Hugo + PaperMod"
   git branch -M main
   git remote add origin <你的GitHub仓库地址>
   git push -u origin main
   ```

2. Cloudflare Pages
   - 创建项目 → 连接 GitHub 仓库
   - 构建设置：
     - 框架预设：None
     - 构建命令：`hugo`
     - 发布目录：`public`
   - 环境变量：
     - `HUGO_VERSION` = 与本地一致（如 `0.134.2`，extended）
     - 可选：`HUGO_ENV` = `production`

3. 绑定自定义域名
   - 把域名接入 Cloudflare
   - 在 Pages 项目里添加自定义域，会自动生成 CNAME

4. 回填生产域名
   - 部署完成并绑定域名后，修改 `config.toml`:
     ```
     baseURL = "https://你的域名/"
     ```
   - 提交并推送，触发自动重建


