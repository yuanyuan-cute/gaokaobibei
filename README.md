# CET-4 Vocab · 高考词汇背单词

纯静态单页应用，覆盖 **3875 个高考考纲词汇**，每个词含音标、多义项释义、真题例句。新增**高频词汇优先学习**与**高频词专项测试**功能。全部学习数据保存在浏览器 localStorage，无需后端。

**功能**：背词卡片 / 记忆曲线复习 / 选择测试（含高频词专项）/ 14 天学习量与掌握分布 / 高频词掌握率 / 词库检索 / 生词本 / 导出导入备份。

## 📁 目录结构

```
gaokao-vocab/
├── index.html          # 主页面（所有 UI + 逻辑）
├── words.js            # 3875 词词库数据（window.GAOKAO_WORDS）
├── qrcode.min.js       # 二维码生成库
├── package.json        # 给 Vercel 用，声明纯静态项目
├── vercel.json         # Vercel 路由 + 缓存策略
├── .gitignore
├── scripts/
│   ├── local-preview.sh      # 一键本地预览
│   └── deploy-vercel.sh      # 一键部署 Vercel
└── README.md
```

## ⭐ 高频词汇功能

- **高频标记**：词库中出现年数 ≥ 3 年的高考词标记为「高频」，单词旁显示橙色「高频」标签
- **优先学习**：背单词页面可开启「高频词优先」，新词按出现年数从高到低排列，适合冲刺阶段
- **专项测试**：测试范围可选「高频词专项」，只考高频词汇
- **掌握统计**：数据页面有「高频词掌握」进度条，显示高频词的已掌握/学习中/未学习数量和掌握率

## 🚀 本地预览

```bash
./scripts/local-preview.sh
# 或
python3 -m http.server 8000
```

浏览器打开 <http://localhost:8000>。

## 🌐 部署到 GitHub Pages

```bash
git init && git add -A && git commit -m "init: gaokao vocab"
git remote add origin https://github.com/<用户名>/<仓库名>.git
git branch -M main && git push -u origin main
```

仓库 **Settings → Pages → Source 选 main / (root) → Save**，1 分钟后访问 `https://<用户名>.github.io/<仓库名>/`。

## ☁️ 部署到 Vercel

推到 GitHub 后，Vercel → New Project → 选仓库 → **Build Command 留空，Output Directory 留空** → Deploy。

或命令行：
```bash
export VERCEL_TOKEN=<你的token>
./scripts/deploy-vercel.sh
```

## 📱 手机使用

电脑浏览器打开部署后的地址 → 点页面右上角分享按钮 → 手机扫码即可。学习数据保存在各自浏览器，换设备用「数据」页面的导出/导入功能迁移。

## 📜 数据来源

- 高考词表：[DenoPark 高考 3500 词](https://cn.denopark.com/data/gaokao3500)（3875 词）
- 音标 / 释义 / 真题例句 / 高频标记：有道词典 API
- 重叠词汇复用 CET-4 词库数据
