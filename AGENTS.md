# AGENTS.md

本仓库用于根据试卷照片或截图生成 HTML 错题集文件。生成结果应适合打印、浏览、归档和二次复习，但当前定位不是完整解析本。

## 工作目标

- 根据用户提供的试卷信息、照片或截图，生成单文件 HTML 错题集。
- HTML 内容聚焦学生复习：题干、必要参考图、考察知识点、难度评分、易错点。
- 不输出完整答案、完整解析、最优解法、举一反三题或知识拓展，除非用户明确要求。

## 文件命名

HTML 文件名由试卷名称自动生成，格式为：

```text
试卷名称.html
```

示例：

```text
期末综合练习卷20.html
```

优先从试卷截图或用户说明中识别：

- 试卷名称，如「期末综合练习」
- 卷号，如「卷20」

文件名不追加「_错题板书本」等类型后缀。

不要在页面标题或正文中显示「根据试卷截图识别」等说明性文字。

## 页面标题

页面顶部只保留必要标题，推荐格式：

```text
六年级下册数学｜期末综合练习卷20
```

标题要求：

- 简洁清楚。
- 不显示「错题重做本」等重复说明。
- 不显示「根据试卷截图识别」。
- 不显示过长副标题。

## 每题结构

每道错题使用独立卡片，结构固定为：

```text
第 X 题    知识点：……    难度：X分    □ □ □

题干

参考图（仅当原题自带图形时显示）

易错点
```

题号、考察知识点、题目难度评分保持同一行展示；空间不足时可以自然换行，但不要让题号单独成行。

题号右侧保留三个空白打卡框，用于学生三次复习后手写打钩。打卡框不要默认打勾，并保持适合打印书写的尺寸。

知识点和难度要求：

- 知识点应简洁概括本题考察内容，如「圆柱切拼与表面积变化」。
- 难度评分由 AI 基于知识点、题型、计算量、推理层数、易错程度和综合难度判断生成。
- 难度使用 1-10 分制，最难为 10 分。
- 难度显示格式固定为「难度 8分」或结构化标签中的「难度」「8分」，不要写成「8/10」。

## 题干规则

「原题」统一命名为「题干」。

题干应保留：

- 题目文字。
- 必要数学符号。
- 选择题选项。
- 填空题空格。
- 题目中的已知条件。

题干中不要加入：

- 解题思路。
- 正确答案。
- 错误答案。
- 解析。
- AI 说明文字。

## 参考图规则

「示意图」「原题自带参考示意图」统一命名为「参考图」。

只有原题本身带有参考图、示意图、几何图、统计图、立体图等图形时，才显示「参考图」模块。没有参考图时，直接进入「易错点」模块，不要显示「本题原题没有自带参考图」等占位说明。

参考图不要直接使用整题截图，也不要简单裁剪贴图。优先用内嵌 SVG 重建原题图形。

当题目包含参考图时，默认按下列规则排版：

- 如果该题只有 1 个参考图，参考图和易错点使用左右分栏：
  左侧为「参考图」，右侧为「易错点」，其中「基于学生板书总结」和「AI总结」上下排列。
  左侧图框和右侧易错点区域保持同高，便于屏幕浏览和打印对齐。
- 如果该题有 2-3 个参考图，不要把易错点放到右侧。
  这类题统一使用纵向结构：题干 → 参考图 → 易错点。
  参考图区域内部按原卷顺序和相对位置正常排布多个分图，但易错点必须整体放在参考图下方。
  每个分图应作为独立图块绘制和排版，不要把多个图挤在同一个 SVG 画布里。
- 移动端或窄屏下自然改为单列。
- 无参考图题目仍保持原结构：题干之后直接显示「易错点」，两块总结左右双栏。

重建参考图时：

- 只保留原题印刷信息。
- 去掉纸张背景、阴影和拍照倾斜。
- 去掉学生笔迹、圈画、划线、箭头、批注、涂改和辅助计算。
- 尽量保持原图结构、比例、标注、图形关系和分图数量。
- 以复刻原图为优先，不要擅自改动，不要随意增减内容，不要自行补充解释性元素。

如果图中出现手写数字、手写公式或额外标记，应判断为学生笔迹并剔除。例如圆柱切拼图上手写的 `20`、`40`、`2` 属于学生笔迹，不应放入参考图。

## 错题板书规则

当前模板不再预留「错题板书」空白书写区。

生成 HTML 时不要输出：

- 「错题板书」标题。
- 大面积空白书写区。
- 横线背景书写区。
- 预填答案或解题步骤。

## 易错点规则

「易错点」放在题干和参考图之后，分为两部分：

```text
基于学生板书总结
AI总结
```

「基于学生板书总结」应结合学生在试卷上的错误答案、圈选、笔迹、辅助计算或批注，总结错误来源。可从概念混淆、条件漏看、公式用错、比例关系理解错误、单位换算错误、图形关系判断错误、把辅助数字误当原题条件、解的范围混淆、长度面积体积变化倍数混淆等角度分析。

「AI总结」应简洁、可复用，能提醒学生下次避坑，最好用一句话点破题型关键。

## 排版与样式

整体风格：简洁、留白充足、适合打印、适合学生手写，不追求复杂装饰。

每道题使用独立卡片，避免内容混在一起。主色从「色调规则」中的 6 套低饱和配色里选择，不固定使用特定颜色。

### 标准页面结构

```
.page          页面容器，max-width 1020px，上下留白
.cover         封面标题栏，渐变背景（--cover-from → --cover-to），圆角 18px
.card          题目卡片，白底，顶部 3px 渐变色条，圆角 14px，hover 轻微上浮
  .q-head      题号行：题号（渐变文字）+ 知识点/难度小号标签 + 打卡框
  .section-title  小节标题：左侧 4px 实色竖条 + 浅色背景块
  .question    题干区：浅底色方框，字重 400，关键词 <b> 用 accent 色
  .figure      参考图容器：浅底色方框，内嵌 SVG
  .figure-error-layout  单图题可用的左右分栏容器：左侧参考图，右侧易错点
  .error-points  易错点双栏网格
    .error-box:first-child   基于学生板书总结：暖橙色调
    .error-box:last-child    AI总结：清绿色调
```

### 标准 CSS 组件

生成 HTML 时，`<style>` 中的组件 CSS 保持以下结构不变，仅替换 `:root` 色调变量：

```css
/* ─ 页面容器 ─ */
.page {
  max-width: 1020px;
  margin: 36px auto;
  padding: 0 0 56px;
  background: transparent;
}

/* ─ 封面 ─ */
.cover {
  text-align: center;
  margin-bottom: 32px;
  padding: 36px 42px 30px;
  background: linear-gradient(135deg, var(--cover-from) 0%, var(--cover-to) 100%);
  border-radius: 18px;
  box-shadow: 0 8px 32px var(--cover-shadow);
}
.cover h1 {
  margin: 0;
  font-size: 30px;
  font-weight: 700;
  letter-spacing: .5px;
  color: #ffffff;
  text-shadow: 0 1px 4px rgba(0,0,0,.18);
}

/* ─ 卡片 ─ */
.card {
  background: var(--paper);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 30px 34px 36px;
  margin: 20px 0;
  box-shadow: var(--card-shadow);
  transition: box-shadow .2s ease, transform .2s ease;
  position: relative;
  overflow: hidden;
}
.card::before {
  content: "";
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  background: linear-gradient(90deg, var(--accent) 0%, var(--accent-mid) 100%);
  border-radius: 14px 14px 0 0;
}
.card:hover {
  box-shadow: var(--card-shadow-hover);
  transform: translateY(-1px);
}

/* ─ 题目头部 ─ */
.q-head {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 24px;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--line);
}
.q-main {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 10px 16px;
  min-width: 0;
}
.q-title {
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-mid) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-size: 26px;
  font-weight: 800;
  letter-spacing: -.5px;
}

/* ─ 知识点 / 难度小号标签 ─ */
.q-meta {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 6px 10px;
  color: var(--muted);
  font-size: 13.5px;
  line-height: 1.45;
}
.tag {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  background: var(--accent-soft);
  border: 1px solid var(--tag-border);
  border-radius: 20px;
  padding: 3px 10px;
  font-size: 13px;
  font-weight: 600;
}
.tag + .tag { margin-left: 4px; }
.tag + .tag::before { display: none; }
.tag-label { color: var(--accent); font-weight: 700; }
.tag-value { color: #2a3f3d; font-weight: 600; }

/* ─ 打卡框 ─ */
.checks { display: flex; gap: 10px; align-items: center; white-space: nowrap; flex-shrink: 0; }
.box {
  width: 26px; height: 26px;
  border: 2px solid var(--check-border);
  border-radius: 6px;
  background: #fff;
  transition: border-color .15s;
}
.box:hover { border-color: var(--accent); }

/* ─ 小节标题 ─ */
.section-title {
  margin: 22px 0 11px;
  padding: 6px 14px;
  border-left: 4px solid var(--accent);
  background: var(--accent-softer);
  border-radius: 0 8px 8px 0;
  color: var(--ink);
  font-size: 17px;
  font-weight: 700;
  letter-spacing: .2px;
}

/* ─ 题干 ─ */
.question {
  background: var(--soft);
  border: 1px solid var(--line);
  border-radius: 10px;
  padding: 18px 22px;
  font-size: 18px;
  font-weight: 400;
  line-height: 1.85;
  color: var(--ink);
}
.question b { font-weight: 600; color: var(--accent); }

/* ─ 参考图 ─ */
.figure {
  background: var(--soft);
  border: 1px solid var(--line);
  border-radius: 10px;
  padding: 14px 18px;
  text-align: center;
  overflow: auto;
  display: inline-block;
  max-width: 100%;
  min-width: 360px;
}
.figure-error-layout {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 16px;
  align-items: stretch;
}
.figure-pane,
.error-pane {
  min-width: 0;
}
.figure-error-layout .section-title { margin-top: 22px; }
.figure-error-layout .figure {
  width: 100%;
  min-width: 0;
  height: calc(100% - 56px);
}
.figure-error-layout .error-points {
  grid-template-columns: 1fr;
  height: calc(100% - 56px);
}

/* ─ 易错点（双栏固定色调，不随主题变化） ─ */
.error-points {
  margin-top: 14px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}
.error-box {
  min-height: 120px;
  border-radius: 10px;
  padding: 16px 18px;
  font-size: 16px;
  line-height: 1.7;
}
.error-box:first-child { background: #fff8f0; border: 1px solid #f0dbc4; }
.error-box:first-child h4 { color: #b85c00; }
.error-box:last-child  { background: #f0f8f0; border: 1px solid #c0ddc0; }
.error-box:last-child  h4 { color: #2a7a3a; }
.error-box h4 {
  margin: 0 0 8px;
  font-size: 15px;
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 6px;
}
.error-box:first-child h4::before { content: "⚠️"; font-size: 14px; }
.error-box:last-child  h4::before { content: "✅"; font-size: 14px; }
.error-box p { margin: 0; color: #363330; }

/* ─ 响应式 ─ */
@media (max-width: 720px) {
  .page { margin: 0; padding: 0 0 32px; }
  .cover { border-radius: 0; padding: 28px 20px 22px; }
  .cover h1 { font-size: 22px; }
  .card { border-radius: 10px; padding: 22px 18px 26px; margin: 16px 12px; }
  .card::before { border-radius: 10px 10px 0 0; }
  .q-title { font-size: 22px; }
  .section-title { font-size: 16px; }
  .question { font-size: 16px; }
  .figure-error-layout { grid-template-columns: 1fr; gap: 0; }
  .error-points { grid-template-columns: 1fr; }
}

svg { max-width: 100%; height: auto; }
.figure svg { max-height: 300px; width: auto; }

/* ─ 打印 ─ */
@media print {
  body { background: #fff; }
  .page { margin: 0; max-width: none; padding: 0; }
  .cover { background: var(--cover-from); border-radius: 0; box-shadow: none; margin-bottom: 6px; padding: 6mm 10mm 5mm; }
  .cover h1 { font-size: 15pt; letter-spacing: 0; }
  .card { box-shadow: none; margin: 7px 0; border-color: #ccc; padding: 10px 12px 12px; border-radius: 0; }
  .card::before { display: none; }
  .card { break-inside: avoid; }
  .q-head { gap: 10px; margin-bottom: 8px; padding-bottom: 6px; }
  .q-main { gap: 4px 8px; }
  .q-title { font-size: 15pt; letter-spacing: 0; }
  .q-meta { gap: 3px 5px; font-size: 8.5pt; line-height: 1.2; }
  .tag { padding: 1px 6px; font-size: 8.5pt; border-radius: 12px; }
  .checks { gap: 5px; }
  .box { width: 16px; height: 16px; border-radius: 4px; }
  .section-title { margin: 8px 0 5px; padding: 2px 8px; font-size: 10.5pt; border-left-width: 3px; }
  .question { padding: 8px 10px; font-size: 10.5pt; line-height: 1.48; border-radius: 6px; }
  .figure-error-layout { gap: 8px; }
  .figure-error-layout .section-title { margin-top: 8px; }
  .figure-error-layout .figure,
  .figure-error-layout .error-points { height: calc(100% - 30px); }
  .figure { padding: 8px; border-radius: 6px; }
  .figure svg { max-height: 42mm; width: auto; }
  .error-points { margin-top: 6px; gap: 6px; }
  .error-box { min-height: 0; padding: 7px 9px; font-size: 9.5pt; line-height: 1.45; border-radius: 6px; }
  .error-box h4 { margin-bottom: 3px; font-size: 9pt; }
  .error-box p { margin: 0; }
}
```

> **注意：** 易错点两栏的颜色（暖橙 / 清绿）是固定的语义色，不随主题色调变化。

---

## 色调规则

生成新的错题集 HTML 时，如果用户没有指定色调，从以下 6 套中随机选择 1 套。整份 HTML 使用同一套，不在同一文件中混用。

将对应 `:root` 块粘贴到 `<style>` 顶部即可切换主题，其余组件 CSS 保持不变。

```css
/* ══ 色调 01：清泉青绿 ══ */
:root {
  --bg: #eef2f0;
  --paper: #ffffff;
  --ink: #1e2422;
  --muted: #6b7876;
  --accent: #1f7a75;
  --accent-mid: #2a9d97;
  --accent-soft: #e8f5f4;
  --accent-softer: #f2faf9;
  --border: #d4e2de;
  --line: #e4edea;
  --soft: #f7faf9;
  --cover-from: #1f7a75;
  --cover-to: #2ab5ad;
  --cover-shadow: rgba(31,122,117,.28);
  --card-shadow: 0 2px 12px rgba(20,50,46,.07), 0 1px 3px rgba(20,50,46,.05);
  --card-shadow-hover: 0 8px 28px rgba(20,50,46,.11), 0 2px 6px rgba(20,50,46,.07);
  --tag-border: #c4dbd8;
  --check-border: #b0c8c4;
  /* SVG: stroke #1f7a75 · shade-fill #d9e6e3 */
}

/* ══ 色调 02：海盐蓝 ══ */
:root {
  --bg: #edf1f6;
  --paper: #ffffff;
  --ink: #1e2228;
  --muted: #6b7280;
  --accent: #2c6aa8;
  --accent-mid: #3d8ed4;
  --accent-soft: #e5f0fb;
  --accent-softer: #f0f7fd;
  --border: #ccd9ea;
  --line: #dde7f2;
  --soft: #f5f9fd;
  --cover-from: #2c6aa8;
  --cover-to: #3fa8d8;
  --cover-shadow: rgba(28,80,140,.26);
  --card-shadow: 0 2px 12px rgba(20,40,70,.07), 0 1px 3px rgba(20,40,70,.05);
  --card-shadow-hover: 0 8px 28px rgba(20,40,70,.11), 0 2px 6px rgba(20,40,70,.07);
  --tag-border: #bad2e8;
  --check-border: #a8c0d8;
  /* SVG: stroke #2c6aa8 · shade-fill #d6e7f4 */
}

/* ══ 色调 03：松林绿 ══ */
:root {
  --bg: #edf2eb;
  --paper: #ffffff;
  --ink: #1e2420;
  --muted: #6b786a;
  --accent: #3d7045;
  --accent-mid: #54965e;
  --accent-soft: #e5f2e6;
  --accent-softer: #f0f8f0;
  --border: #cadac7;
  --line: #dce8d9;
  --soft: #f4f9f3;
  --cover-from: #3d7045;
  --cover-to: #60b070;
  --cover-shadow: rgba(35,80,40,.26);
  --card-shadow: 0 2px 12px rgba(30,50,28,.07), 0 1px 3px rgba(30,50,28,.05);
  --card-shadow-hover: 0 8px 28px rgba(30,50,28,.11), 0 2px 6px rgba(30,50,28,.07);
  --tag-border: #badbb8;
  --check-border: #a8c8a4;
  /* SVG: stroke #3d7045 · shade-fill #d4e8d2 */
}

/* ══ 色调 04：靛青灰 ══ */
:root {
  --bg: #edeef4;
  --paper: #ffffff;
  --ink: #1e2028;
  --muted: #6b6f80;
  --accent: #4a5f8a;
  --accent-mid: #6278a8;
  --accent-soft: #e8ecf5;
  --accent-softer: #f2f4fa;
  --border: #ccd0e4;
  --line: #dde1ee;
  --soft: #f5f6fc;
  --cover-from: #4a5f8a;
  --cover-to: #6e8ab8;
  --cover-shadow: rgba(40,50,100,.26);
  --card-shadow: 0 2px 12px rgba(30,35,65,.07), 0 1px 3px rgba(30,35,65,.05);
  --card-shadow-hover: 0 8px 28px rgba(30,35,65,.11), 0 2px 6px rgba(30,35,65,.07);
  --tag-border: #bcc5dc;
  --check-border: #a8b2cc;
  /* SVG: stroke #4a5f8a · shade-fill #d4daea */
}

/* ══ 色调 05：梅子玫瑰 ══ */
:root {
  --bg: #f3eef1;
  --paper: #ffffff;
  --ink: #28201e;
  --muted: #7a7078;
  --accent: #8a4a63;
  --accent-mid: #ae6280;
  --accent-soft: #f5e8ef;
  --accent-softer: #faf2f6;
  --border: #e0cdd6;
  --line: #ecdde6;
  --soft: #fdf7fa;
  --cover-from: #8a4a63;
  --cover-to: #c07090;
  --cover-shadow: rgba(100,40,65,.26);
  --card-shadow: 0 2px 12px rgba(65,30,45,.07), 0 1px 3px rgba(65,30,45,.05);
  --card-shadow-hover: 0 8px 28px rgba(65,30,45,.11), 0 2px 6px rgba(65,30,45,.07);
  --tag-border: #d8b8c8;
  --check-border: #c8a8b8;
  /* SVG: stroke #8a4a63 · shade-fill #ecd8e0 */
}

/* ══ 色调 06：月桂金 ══ */
:root {
  --bg: #f2f0e8;
  --paper: #ffffff;
  --ink: #26231a;
  --muted: #78756a;
  --accent: #7a6428;
  --accent-mid: #9e8238;
  --accent-soft: #f5f0dc;
  --accent-softer: #faf7ec;
  --border: #ddd5b8;
  --line: #e8e3cc;
  --soft: #faf8f0;
  --cover-from: #7a6428;
  --cover-to: #b89840;
  --cover-shadow: rgba(90,72,20,.26);
  --card-shadow: 0 2px 12px rgba(60,50,20,.07), 0 1px 3px rgba(60,50,20,.05);
  --card-shadow-hover: 0 8px 28px rgba(60,50,20,.11), 0 2px 6px rgba(60,50,20,.07);
  --tag-border: #d4c898;
  --check-border: #c4b888;
  /* SVG: stroke #7a6428 · shade-fill #e4dab8 */
}
```

## 技术要求

- 使用单文件 HTML。
- CSS 写在 `<style>` 中。
- 不依赖外部 CDN。
- 不依赖网络字体。
- 不依赖外部图片。
- 参考图优先使用内嵌 SVG。
- SVG 应清晰可打印，便于后续修改和读取图形结构。

## 禁止内容

除非用户明确要求，不要生成：

- 完整答案。
- 完整解析步骤。
- 最优解法。
- 举一反三题。
- 知识点拓展。
- AI 解释性废话。
- 「本题没有参考图」等占位说明。
- 「根据试卷截图识别」等过程说明。

## 生成前检查

生成或修改 HTML 前，确认：

- 文件名符合「试卷名称.html」，不包含年级学科前缀，不追加「_错题板书本」后缀。
- 页面标题简洁，不含多余模板说明。
- 每题有题号、知识点、难度评分和三个空白打卡框。
- 难度评分已由 AI 基于知识点、题型和综合难度判断生成。
- 题号、知识点、难度评分尽量保持同一行；难度格式为「X分」，不要写成「X/10」。
- 每题有「题干」「易错点」。
- 只有原题有图时才出现「参考图」。
- 单图参考图题目可使用左右分栏；若一题有 2-3 个图，不要把易错点放到右边。
- 参考图已优先按原图复刻，没有擅自增减内容或补充解释性元素。
- 参考图已剔除学生笔迹、圈画、批注和辅助计算。
- 不生成「错题板书」标题、空白书写区或横线书写区。
- 易错点包含「基于学生板书总结」和「AI总结」。
- HTML 不依赖外部资源，并包含打印样式。
