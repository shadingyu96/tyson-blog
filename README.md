# Playwright 博客（静态版）

一个纯 HTML + CSS 的轻量博客示例，无需 npm 或构建工具。

## 本地访问

方式一：直接双击打开
- 打开 `index.html`

方式二：本地 HTTP 服务（推荐）
```bash
cd /home/node/.openclaw/workspace/playwright-blog
python3 -m http.server 8080
```
然后访问：
- `http://localhost:8080`

## 已完成增强

- 顶部导航栏（首页 / 文章）
- 深色模式切换（自动保存到 localStorage）
- 文章列表 + 简单分页样式
- 移动端适配

## 目录结构

```text
playwright-blog/
├── index.html
├── styles.css
└── posts/
    └── playwright-sync-vs-async.html
```

## 发布到 GitHub Pages（可选）

1. 新建 GitHub 仓库（例如 `playwright-blog`）
2. 推送本目录代码
3. 在仓库 Settings → Pages
   - Source 选择 `Deploy from a branch`
   - Branch 选择 `main` / root
4. 几分钟后可访问：
   - `https://<你的GitHub用户名>.github.io/playwright-blog/`
