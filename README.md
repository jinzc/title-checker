# 标题原创校验工具

一个纯前端（零依赖、单文件）的在线校验小工具，用于判断新闻类标题是否为重复提交。

## 校验规则

- **输入格式**（固定）：`【频道栏目名称】标题`
- **频道栏目名称** 必须是以下 16 个之一：
  朝闻天下、新闻直播间、午夜新闻、新闻30分、中国新闻、今日环球、共同关注、正点财经、天下财经、体坛快讯、国防军事早报、经济信息联播、军事报道、新闻联播、晚间新闻、24小时
- **判定逻辑**：若新输入内容的「标题」部分与**历史记录中任意一条**的标题完全相同 → 判定为 `重复`；否则判定为 `原创`。
- **每日统计**：以北京时间（UTC+8）0 点作为清零时点；跨天后当日统计自动归零，历史记录按日期归档保留（时间、输入内容、校验结果）。
- **数据存储**：使用浏览器 `localStorage` 持久化，无需后端。数据保存在当前浏览器中，换设备/浏览器不共享。

## 文件结构

```
title-checker/
├── index.html      # 全部功能（页面 + 样式 + 逻辑），单文件即可运行
├── README.md       # 本文件
├── LICENSE         # MIT 开源协议
└── .gitignore
```

## 本地使用

直接用浏览器打开 `index.html` 即可；或：

```bash
# 任选其一启动本地服务
python3 -m http.server 8080
npx serve .
```

然后访问 http://localhost:8080

## 部署到 GitHub Pages（免费在线使用）

1. 在 GitHub 新建仓库（如 `title-checker`），把本目录推上去：
   ```bash
   git init
   git add .
   git commit -m "init: title checker"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/title-checker.git
   git push -u origin main
   ```
2. 仓库页面 → **Settings** → **Pages** → Source 选择 `Deploy from a branch` → 分支选 `main`、目录选 `/(root)` → Save。
3. 约 1 分钟后即可通过 `https://<你的用户名>.github.io/title-checker/` 在线访问。

## 常见问题

**Q：如何修改允许的栏目列表？**
编辑 `index.html` 顶部的 `CHANNELS` 数组。

**Q：数据存在哪里？会丢吗？**
存在浏览器 `localStorage`（键名 `title_checker_records_v1`）。清空浏览器数据会丢失；换浏览器不共享。如需多人共用/跨设备，需要增加后端存储（可自行 fork 扩展）。

**Q：判定是"完全相同"吗？**
是严格的全等比较（含空格、标点、大小写敏感），去首尾空格后比较。
