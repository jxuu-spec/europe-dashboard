# GitHub Pages 部署指南

> Cloudflare Workers/Pages 默认子域名在中国大陆访问不稳定（常见 ERR_CONNECTION_TIMED_OUT）。
> GitHub Pages 的 `github.io` 域名在中国大陆访问相对稳定，推荐改用此方案。

---

## 为什么 GitHub Pages 更稳定？

| 对比项 | Cloudflare Pages (默认域名) | GitHub Pages |
|--------|---------------------------|-------------|
| 默认域名 | `xxx.pages.dev` / `xxx.workers.dev` | `xxx.github.io` |
| 国内访问 | 常被墙/限速 ❌ | 相对稳定 ✅ |
| 费用 | 免费 | 免费 |
| 部署难度 | 简单 | 简单 |
| HTTPS | 自动 | 自动 |

---

## 部署步骤（5分钟完成）

### 第1步：创建 GitHub 仓库

1. 访问 [github.com](https://github.com) 登录你的账号
2. 点击右上角 **+** → **New repository**
3. 填写信息：
   - **Repository name**: `europe-dashboard`（可自定义）
   - **Description**: 携程国旅欧洲业务经营看板
   - **Visibility**: Public（必须公开才能免费使用 Pages）
   - ✅ 勾选 **Add a README file**
4. 点击 **Create repository**

### 第2步：上传文件

**方式一：网页直接上传（推荐新手）**

1. 进入刚创建的仓库页面
2. 点击 **Add file** → **Upload files**
3. 将本文件夹内的以下文件拖入上传区域：
   ```
   index.html
   lib/
   └── chart.js
   ```
   ⚠️ **注意**：拖 `index.html` 和 `lib/` 文件夹，不要拖外层文件夹
4. Commit message 填写：`v1.2.3: 初始部署`
5. 点击 **Commit changes**

**方式二：Git 命令行**

```bash
# 克隆仓库到本地
git clone https://github.com/<你的用户名>/europe-dashboard.git
cd europe-dashboard

# 复制本文件夹内的 index.html 和 lib/ 到仓库目录

# 提交并推送
git add -A
git commit -m "v1.2.3: 初始部署"
git push origin main
```

### 第3步：启用 GitHub Pages

1. 在仓库页面，点击顶部 **Settings** 标签
2. 左侧菜单找到 **Pages**（在 "Code and automation" 分类下）
3. 在 "Build and deployment" 区域：
   - **Source**: 选择 **Deploy from a branch**
   - **Branch**: 选择 `main`（或 `master`）
   - 文件夹选择 `/(root)`
4. 点击 **Save**

### 第4步：访问网址

等待 1-3 分钟后，你的看板就会上线：

```
https://<你的GitHub用户名>.github.io/europe-dashboard/
```

例如：
```
https://jxuu.github.io/europe-dashboard/
```

在仓库的 **Settings → Pages** 页面也可以看到实际网址。

---

## 日后更新方法

修改 `index.html` 后：

**网页方式：**
1. 进入仓库 → 点击 `index.html` → 点击右上角铅笔图标编辑
2. 粘贴更新后的内容
3. 填写 Commit message（如 `v1.2.4: 更新价格带数据`）
4. 点击 **Commit changes**
5. 等待 1-2 分钟，网址自动更新

**Git 方式：**
```bash
cd europe-dashboard
# 替换 index.html 为最新版本
git add index.html
git commit -m "v1.2.4: 更新数据"
git push origin main
```

---

## 绑定自定义域名（可选）

如果你有自有域名，可以绑定到 GitHub Pages：

1. 仓库 → **Settings** → **Pages**
2. 在 "Custom domain" 处输入你的域名（如 `dashboard.yourdomain.com`）
3. 点击 **Save**
4. 在你的域名 DNS 服务商处添加 CNAME 记录：
   - 主机记录: `dashboard`（或 `@` 如果你用根域名）
   - 记录类型: `CNAME`
   - 记录值: `你的用户名.github.io`
5. 等待 DNS 生效（通常几分钟到几小时）

---

## 常见问题

**Q: 页面显示空白？**

A: 请检查：
1. 浏览器控制台（F12 → Console）是否有报错
2. `lib/chart.js` 文件是否已上传到仓库
3. 文件路径是否正确

**Q: 访问 404？**

A: 请检查：
1. Settings → Pages 中 Source 是否已正确设置（main 分支，root 目录）
2. 是否已等待 1-3 分钟（首次部署需要时间）
3. 仓库是否为 Public（Private 仓库的 Pages 需要付费）

**Q: 可以设置访问密码吗？**

A: GitHub Pages 不支持密码保护。如需限制访问，建议：
- 仓库设为 Private + 使用付费版 GitHub Pages
- 或在页面中加入前端密码验证（安全性较低，仅防君子）

---

## 技术支持

- GitHub Pages 文档: [docs.github.com/pages](https://docs.github.com/pages)
- 如遇问题，检查浏览器控制台（F12）查看报错信息

---

*GitHub Pages 部署指南 v1.0 | 2026-07-27*
