---
name: "math-hunt-notes"
description: "Builds the math-notes notebook: hunt sources (Bilibili/Douyin reposts), fact-check, author KaTeX+SVG entries, verify in browser, then push. Invoke when adding entries or hunting interesting math facts."
---

# 数学猎奇笔记 · 写作流程

把「找猎奇数学知识 → 核对 → 按格式写成条目 → 浏览器验证 → 推送」这条流程固化下来，用于维护 **数学趣味猎奇笔记**（Math Hunt Notes）。

## 何时调用

- 用户要求给「数学笔记 / 电子笔记 / math-notes」**新增条目**
- 用户要求「找有趣的数学知识 / 冷门定理 / 反直觉结论」并入库
- 对已有笔记做**批量扩充**或**按四栏补充**

## 先决条件

先读仓库里的 **`维护手册.md`**——定位、四栏结构、格式规范、审核规则、部署与凭证都在那里。本 Skill 只描述可复用的流程。

## 流程

### 1. 找源（Source hunting）
- B站**专栏/opus**（`bilibili.com/read/*`、`/opus/*`）：可抓全文 ✓
- B站**视频页**：只返回推荐栏（正文是 JS），拿不到内容 ✗
- **抖音**：抓不到（登录态 + 强风控）→ 走**转载源**（搜狐 / 头条 / 知乎 / 公众号）还原
- 权威源用于核对：维基 / MathWorld / OEIS / arXiv
- 搜索时用 `site:` 快速定位平台内容，如 `site:bilibili.com <主题>`

### 2. 核对（Fact-check）
- 转载/短视频源**常有错漏**，必须回权威源逐条核对，**不照抄**。
- 拿不准的结论标注「存疑」或直接放弃。

### 3. 写作（Authoring）
- 公式用 **KaTeX**：行内 `$...$`、块级 `$$...$$`
- 图示用**内联 SVG**，不用外链图片
- 每条：**一句话核心结论置顶** + 正文 + 来源链接 + 难度标签
- 超宽公式**拆多行**（`\begin{aligned}` / `\begin{gathered}`），否则会被卡片裁切
- 归类到四条线：定义 `def-*` / 定理 `thm-*` / 趣题 `puz-*` / 经验 `exp-*`

### 4. 验证（Verify）
- 本地 `python3 -m http.server 8080`，在浏览器打开
- **以浏览器实测为准**（预览面板更宽，可能「预览正常、浏览器错位」）
- 用脚本遍历所有块级公式，确认 `scrollWidth > clientWidth` 的公式数为 0

### 5. 提交（Ship）
- `git add <指定文件>`（勿用 `-A`，避免把大文件/凭证带进版本库）
- `commit` → `push`

## 审核约定

- **不自动补内容**：先给用户**候选清单**，用户挑选后再写。
- 成品**先给用户确认**再推送；每批默认 **5 条**。

## 注意

- 不要把 token、密码等访问凭证写进条目或本 Skill。
- 大文件（打包 zip、上传图片）不要提交。
