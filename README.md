# CET-4 Vocab · 四级词汇背单词

纯静态单页应用，覆盖 **4544 个四级词汇**，每个词含音标、多义项、英文释义、例句、真题例句、短语、同近义词和助记。全部学习数据保存在浏览器 localStorage，无需后端。

**功能**：背词卡片 / 记忆曲线复习 / 选择测试 / 14 天学习量与掌握分布 / 词库检索 / 生词本 / 导出导入备份。

## 📁 目录结构

```
cet4-vocab/
├── index.html          # 主页面（所有 UI + 逻辑）
├── words.js            # 4544 词词库数据（加载后写入 window.CET4_WORDS）
├── qrcode.min.js       # 二维码生成库（分享面板用）
├── package.json        # 给 Vercel 用，声明纯静态项目
├── vercel.json         # Vercel 路由 + 缓存策略
├── .gitignore          # 排除 OS / 编辑器 / node_modules / zip 等
├── scripts/
│   ├── local-preview.sh      # 一键本地预览
│   └── deploy-vercel.sh      # 一键部署 Vercel 生产环境
└── README.md
```

> **不需要构建步骤**，没有 npm run build，没有 TypeScript，没有 Webpack。任何能托管静态文件的平台（GitHub Pages / Vercel / Netlify / Cloudflare Pages / 对象存储）都能直接上线。

## 🚀 本地预览

```bash
# 方式 A：一键脚本（自动选 python3 或 node）
./scripts/local-preview.sh          # 默认端口 8000
./scripts/local-preview.sh 3000     # 自定义端口

# 方式 B：手动起服务
python3 -m http.server 8000
# 或
npx --yes serve .
```

浏览器打开 <http://localhost:8000> 即可。**不要直接双击 index.html 用** **`file://`** **打开**——部分浏览器对 `file://` 协议下读取同目录 JS 有限制。

## 🌐 部署路径一：GitHub Pages（零成本、永久在线）

### Step 1 · 创建仓库

1. GitHub 右上角 `+` → New repository
2. Repository name：`cet4-vocab`（随便起）
3. Public 勾上
4. **不要**勾选 Add a README，保持空仓库

### Step 2 · 推送代码

```bash
cd /path/to/cet4-vocab

git init
git add -A
git commit -m "init: CET-4 vocab SPA"

# 把下面的 <你的GitHub用户名> 换掉
git remote add origin git@github.com:<你的GitHub用户名>/cet4-vocab.git
git branch -M main
git push -u origin main
```

第一次 push 会让你输 SSH key 或 token，按 GitHub 提示走就行。

### Step 3 · 开启 Pages

1. 仓库页面 → **Settings** → 左侧 **Pages**
2. Source 选 **Deploy from a branch**
3. Branch 选 `main`，Folder 选 `/ (root)`
4. Save
5. 等 30–60 秒，顶部横幅会出现一条绿色的访问链接，形如：

   ```
   https://<你的GitHub用户名>.github.io/cet4-vocab/
   ```

> ⚠️ **路径规则**：GitHub Pages 部署到子路径 `<repo>/` 下。本项目资源引用全是相对路径，已经过验证能正常加载，直接用就行。
>
> 如果仓库名是 `<你的GitHub用户名>.github.io`（个人主页仓库），访问地址就是 `https://<用户名>.github.io/` 根路径。

### Step 4 · 手机打开

手机浏览器访问上面那个 `github.io` 链接 → 点页面右上角**分享图标** → 弹层里显示二维码 → 扫自己手机就能用了。想让同学也用，直接把链接发过去。

### 自定义域名（可选）

1. Pages 设置页 → Custom domain 填你域名的子域，比如 `cet4.example.com`
2. DNS 服务商加一条 CNAME：`cet4 → <你的GitHub用户名>.github.io`
3. 勾选 **Enforce HTTPS**

## ☁️ 部署路径二：Vercel（最省心、自动 HTTPS）

### 方式 A · Vercel 面板 Import 仓库（推荐，图形界面）

1. 先按上面 GitHub 路径把代码推到 GitHub
2. 打开 [vercel.com](https://vercel.com) → 用 GitHub 账号登录
3. **Add New Project** → 选刚推的 `cet4-vocab` 仓库
4. **Framework Preset** → Vercel 会自动识别为 `Other`，**Build Command 留空**，**Output Directory 留空**
5. Project Name 随便填，点 **Deploy**
6. 20 秒后自动给你一个：

   ```
   https://cet4-vocab-xxxx.vercel.app
   ```

以后每次 `git push origin main`，Vercel 自动重新部署。

### 方式 B · 命令行一键脚本

适合 CI/CD 场景，或不想登 Vercel 面板。

```bash
# 1. 安装 Vercel CLI（如果没装）
npm install -g vercel

# 2. 去 https://vercel.com/account/tokens 创建一个 Personal Token，复制出来
export VERCEL_TOKEN=你复制的token

# 3. 一键部署生产环境
./scripts/deploy-vercel.sh
```

脚本跑完会打印公网 `vercel.app` URL，直接复制给手机用。也可以 `./scripts/deploy-vercel.sh --token 你的token` 不带环境变量。

### Vercel 部署要点速查

| 字段               | 填什么                 |
| ---------------- | ------------------- |
| Framework Preset | `Other`             |
| Build Command    | **留空**（本项目是纯静态，不构建） |
| Output Directory | **留空**（直接发布根目录）     |
| Install Command  | 不需要（没有 build 依赖）    |
| Root Directory   | 仓库根目录               |
| Auto Deploy      | ✅ 勾上（push 自动发布）     |

> 项目根目录的 `vercel.json` 会帮 Vercel 正确处理静态文件缓存（words.js 缓存 30 天，index.html 缓存 7 天），**不要删**。

## 📱 手机使用流程

```
本地预览 / 部署上线
        │
        ▼
电脑浏览器打开页面 ──▶ 右上角分享按钮
        │                      │
        │                      ▼
        │                弹出二维码 + 链接
        │                      │
        ▼                      ▼
手机扫二维码 ←─────────── 手机浏览器直接输入链接
        │
        ▼
开始背单词 📚
```

**学习记录保存在各自设备的浏览器 localStorage**，同一浏览器清缓存会丢。如果想换设备继续：页面「数据」Tab 底部有 **导出记录** → 生成 JSON → 新设备「导入记录」。

## 🧰 常见问题

**Q: 手机扫 GitHub Pages 二维码打不开？**
A: 检查你填的仓库分支是不是 `main` 而不是 `master`，Pages 设置里 Folder 是不是 `/ (root)`。地址必须是 `https://<user>.github.io/<repo>/`，注意结尾的 `/`。

**Q: GitHub Pages 页面空白 / 只显示词库加载失败？**
A: 多半是 `index.html` 和 `words.js` 不在同一个路径下，或浏览器缓存了旧版本。硬刷新（Ctrl+Shift+R）或加查询参数 `?v=2` 试试。

**Q: Vercel 部署失败 / 404？**
A: 确认 Build Command 和 Output Directory 都留空。`vercel.json` 文件必须在项目根目录。如果是 monorepo 的子目录项目，面板里要把 Root Directory 指到有 `index.html` 的目录。

**Q: 背到一半换设备，数据怎么同步？**
A: 目前没有云端同步（不需要后端），用页面内置的 **导出记录 / 导入记录** 做手动迁移。未来如果上云端同步，加一个 JSON 存储后端即可。

## 📜 许可

词库数据来自公开的 [kajweb/dict](https://github.com/kajweb/dict) 项目（非商业用途学习使用）。本站代码 MIT License，随便拿去用。
