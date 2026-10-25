# Hydejack 简历网站 — AI Infra 方向

基于 [Hydejack](https://hydejack.com/) 免费版构建的个人简历网站，面向 **AI Platform Development Engineer** 岗位。

## 目录结构

```
hydejack-resume/
├── .github/workflows/
│   └── jekyll.yml          # GitHub Actions 自动部署工作流
├── _data/
│   └── authors.yml         # 作者信息（姓名、邮箱、头像、社交链接）
├── _includes/
│   ├── my-head.html        # 自定义 <head> 内容
│   └── my-body.html        # 自定义 <body> 底部脚本
├── _sass/                  # 样式文件
├── assets/img/             # 图片资源（侧边栏背景等）
├── _config.yml             # 站点核心配置
├── index.html              # 首页
├── resume.md               # ★ 简历页面（核心内容）
├── about.md                # 关于页面
├── 404.md                  # 404 页面
├── Gemfile                 # Ruby 依赖
└── .gitignore
```

---

## 部署到 GitHub Pages（完整步骤）

### 第 1 步：注册 GitHub 账号

如已有账号，跳过。访问 [github.com](https://github.com) 注册。

### 第 2 步：创建仓库

1. 登录 GitHub，点击右上角 **+** → **New repository**
2. Repository name 填：`<你的用户名>.github.io`
   - 例如你的用户名是 `zhangsan`，仓库名就是 `zhangsan.github.io`
   - **必须是这个格式**，否则 GitHub Pages 无法启用用户主页
3. 选择 **Public**（免费版 GitHub Pages 仅支持公开仓库）
4. **不要**勾选 "Add a README file" 等选项（保持空仓库）
5. 点击 **Create repository**

### 第 3 步：上传项目文件

#### 方式 A：用 GitHub 网页上传（最简单）

1. 将本目录 `hydejack-resume/` 中的**所有文件**打包为 ZIP
2. 在 GitHub 仓库页面点击 **uploading an existing file**
3. 拖入所有文件（注意：需要包含 `.github` 和 `.gitignore` 等隐藏文件）

#### 方式 B：用 Git 命令行（推荐）

```bash
# 1. 进入项目目录
cd hydejack-resume

# 2. 初始化 Git 仓库
git init
git branch -M master

# 3. 添加所有文件
git add -A

# 4. 提交
git commit -m "Initial commit: Hydejack resume site"

# 5. 关联远程仓库（替换 <你的用户名>）
git remote add origin https://github.com/<你的用户名>/<你的用户名>.github.io.git

# 6. 推送
git push -u origin master
```

### 第 4 步：启用 GitHub Pages

1. 进入仓库 → **Settings** → 左侧 **Pages**
2. **Source** 选择 **GitHub Actions**（不是 "Deploy from a branch"）
3. 保存

> 推送代码后，GitHub Actions 会自动构建并部署。进入仓库的 **Actions** 标签页可以查看构建进度。

### 第 5 步：修改配置（重要！）

推送后，需要编辑 `_config.yml` 中的占位符：

```yaml
# 将所有 <你的姓名>、<your-username>、<your-email@example.com> 替换为真实信息
url:                   https://<你的用户名>.github.io    # ← 改成你的
title:                 "<你的姓名> | AI Platform Engineer"  # ← 改成你的
author:
  name:                <你的姓名>                          # ← 改成你的
  email:               <your-email@example.com>            # ← 改成你的
copyright:             "© 2024 <你的姓名>. All rights reserved."
```

同样需要编辑以下文件中的占位符：
- `resume.md` — 简历内容（教育、工作、项目等）
- `about.md` — 关于页面
- `_data/authors.yml` — 作者信息和社交链接

可以在 GitHub 网页上直接编辑：点击文件 → ✏️ 铅笔图标 → 编辑 → Commit changes。
每次提交后 GitHub Actions 会自动重新构建部署。

### 第 6 步：访问你的网站

部署完成后（通常 1-2 分钟），访问：

```
https://<你的用户名>.github.io
```

---

## 本地预览（可选）

如果想在推送前预览效果：

### 安装 Ruby

**macOS:**
```bash
brew install ruby
```

**Ubuntu/Debian:**
```bash
sudo apt install ruby-full build-essential zlib1g-dev
```

**Windows:** 下载 [RubyInstaller](https://rubyinstaller.org/)

### 运行 Jekyll

```bash
cd hydejack-resume
gem install bundler
bundle install
bundle exec jekyll serve
```

然后打开 http://localhost:4000

---

## 自定义指南

### 修改简历内容

编辑 `resume.md`，所有内容都是标准 Markdown。主要板块：

| 板块 | 文件位置 | 说明 |
|------|----------|------|
| 姓名/联系方式 | `resume.md` 顶部 | 替换占位符 |
| 求职意向 | `resume.md` | 修改目标岗位描述 |
| 专业技能 | `resume.md` 表格 | 按实际技能调整 |
| 教育背景 | `resume.md` | 填写学校、专业、时间 |
| 工作经历 | `resume.md` | 填写公司、职位、成果 |
| 项目经历 | `resume.md` | 填写 2-3 个相关项目 |
| 学习方向 | `resume.md` | 展示自学路线和进度 |

### 修改侧边栏颜色

编辑 `_config.yml`：
```yaml
accent_color:          rgb(38,139,210)   # 主色调（侧边栏强调色）
theme_color:           rgb(25,55,71)     # 浏览器 UI 颜色
```

### 修改侧边栏背景图

替换 `assets/img/sidebar-bg.jpg` 为你自己的图片（建议 1920x1080 或更大）。

### 添加头像

1. 将头像图片放到 `assets/img/avatar.jpg`（建议 256x256）
2. 编辑 `_data/authors.yml`，取消 `picture` 部分的注释：
```yaml
picture:
  path: /assets/img/avatar.jpg
  srcset:
    1x: /assets/img/avatar.jpg
    2x: /assets/img/avatar@2x.jpg
```

### 添加社交链接

编辑 `_data/authors.yml` 的 `social` 部分，取消注释并填入用户名：
```yaml
social:
  github:          your-username
  linkedin:        your-linkedin-id
  email:           your-email@example.com
```

---

## 导出 PDF 简历

部署后，在浏览器中打开简历页面：
1. 访问 `https://<你的用户名>.github.io/resume/`
2. 按 `Ctrl+P`（Windows）或 `Cmd+P`（Mac）
3. 选择 "保存为 PDF"
4. 建议在打印设置中关闭页眉页脚

---

## 常见问题

### Q: 推送后网站没有更新？
A: 进入仓库 **Actions** 标签页查看构建状态。如果失败，检查 `_config.yml` 语法（YAML 对缩进敏感）。

### Q: 构建报错 "invalid YAML"？
A: 检查 `_config.yml` 中是否有多余的空格或 Tab。YAML 只允许空格缩进，不能用 Tab。

### Q: 想要更专业的简历布局（打印优化、结构化数据）？
A: 购买 [Hydejack PRO](https://hydejack.com/download/)（$79 一次性），获得内置 Resume 布局、Portfolio、搜索等功能。PRO 版的简历页面有专门的打印样式和 JSON-LD 结构化数据。

### Q: 仓库名不是 `<用户名>.github.io` 怎么办？
A: 如果仓库名是其他名称（如 `my-resume`），网站地址会是 `https://<用户名>.github.io/my-resume/`，且需要在 `_config.yml` 中设置 `baseurl: '/my-resume'`。

### Q: 分支是 main 而不是 master？
A: 编辑 `.github/workflows/jekyll.yml`，将 `branches: ["master"]` 改为 `branches: ["main"]`。

---

## 技术栈

- [Jekyll](https://jekyllrb.com/) 4.3 — 静态站点生成器
- [Hydejack](https://hydejack.com/) 9.2 — Jekyll 主题（免费版）
- [GitHub Pages](https://pages.github.com/) — 免费托管
- [GitHub Actions](https://github.com/features/actions) — 自动构建部署

## 许可证

Hydejack 免费版遵循 [GPL-3.0](https://github.com/hydecorp/hydejack/blob/master/LICENSE.md) 许可证。
