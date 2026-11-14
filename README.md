# 刘老师 · AI传道人 · 个人作品展示网站

纯静态个人站：**7 件 AI 作品 · 5 部著述（含「AI 三部曲」）· 扫码相连**。

## 特性

- 三套皮肤：纸（新中式宣纸）/ 夜（暗色科技）/ 雪（瑞士极简），右下角调色盘切换，选择本地记忆
- 两种布局：卷轴（编辑部级列表）/ 卡片（作品集网格），同一面板切换
- 在线阅读：三本技术书全文可在站内直接阅读，点击时才载入 PDF，首屏不加载整本
- 扫码相连：微信个人号 / 公众号「AI传道」/ 知识星球「AI产品和架构」，点击灯箱放大
- 纯静态零后端：无服务端依赖，Vercel 静态托管即可
- 响应式适配移动端，支持 `prefers-reduced-motion`
- 结构化数据：内置 `Person` + `Book` 的 JSON-LD，便于搜索引擎理解个人品牌与著作

## 目录

- `index.html` — 网站本体（仓库根目录）
- `public/images/` — 二维码与配图，页面中以 `public/images/...` 引用
- `public/*.pdf` — 三本技术书全文，页面中以 `public/...`（URL 编码）引用
- `vercel.json` — 未指定输出目录，Vercel 默认以仓库根目录作为站点根
- `.vercelignore` — 部署时排除 README、笔记等非站点文件
- `想法.md` — 需求原始笔记

## 本地预览

```powershell
npx serve .
```

或任意静态服务器指向**仓库根目录**（不是 `public/`）。**不要**直接双击 `index.html` 验证阅读器：`file://` 下部分浏览器会拦截 PDF 内嵌预览。

## 部署

保持纯静态托管：

- Vercel：导入仓库即可。`vercel.json` 不设置 `outputDirectory`，站点根就是仓库根目录，`/` 由根目录 `index.html` 提供，资源位于 `/public/...`。若在 Vercel 控制台手动填过 Output Directory，需要清空，避免仍指向 `public`。
- GitHub Pages / Netlify / 对象存储：同样以仓库根目录为发布目录。

## 电子书体积

| 文件 | 体积 |
| --- | --- |
| 拆解AI大模型——人人都能看懂AI大脑.pdf | 约 5.8 MB |
| 开发AI智能助手——人人都会做AI智能体.pdf | 约 2.9 MB |
| 企业AI落地实践——人人都会用FDE方法论.pdf | 约 3.2 MB |
| 合计 | 约 12 MB |

单文件均远低于 GitHub 100 MB 单文件上限。若后续频繁更新 PDF 版本、仓库历史明显膨胀，再考虑迁移到 Git LFS 或对象存储（CDN）并保留站内阅读链接。

## 维护

产品与书籍信息集中在 `index.html` 的「七件作品」「五卷著述」两个章节，直接改文字即可；新增书籍时复制一张 `.book-item`，并给「在线阅读全文」按钮补上 `data-reader`、`data-title`、`data-file`（`data-file` 使用 URL 编码后的 PDF 路径，当前形如 `public/%E6%8B%86...pdf`）。
