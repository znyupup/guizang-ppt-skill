---
description: 风格 C · 文档形态 (单文件 HTML, 不是 PPT). 当用户想要"长读文章 / explainer / 摘读 / Field Note / blog post"风格的可滚动 HTML 输出时使用. 提供横版竖版两套模板, 每套支持 Skill 原始 6 套颜色变体 (IKB 蓝 / 安全橙 / 柠檬黄 / 柠檬绿 / 森林墨 / 牛皮纸).
---

# 风格 C · 文档形态 (Doc Style)

## 这是什么

**单文件 HTML 长读文档**, 不是横向翻页 PPT, 是**纯滚动**的可读形态. 灵感来自 [thariqs.github.io/html-effectiveness](https://thariqs.github.io/html-effectiveness/) 这一类 Claude/Anthropic 团队的实际产出 —— 字号克制, 信息密度高, 像精修过的 Markdown.

**与风格 A/B 的差别**

| | 风格 A 杂志 | 风格 B 瑞士 | **风格 C 文档** |
|---|---|---|---|
| 形态 | 横向翻页 PPT | 横向翻页 PPT | **纯滚动单页** |
| 适合时长 | 演讲 15-30min | 演讲 15-30min | **3-10min 阅读** |
| 字号特征 | 大字 vw-based 对比强 | 大字 200 weight 极简 | **px-based 收紧, 整体 ≤38px** |
| 互动 | 翻页 / ESC 索引 | 翻页 / ESC 索引 | **scroll / details 折叠** |
| 锚点 | Monocle 杂志 / 私享会 PPT | Vignelli / Helvetica | **Anthropic / GitHub README / Substack** |

## 何时用风格 C (而不是 A/B)

- ✅ 用户说"做个网页 / 文章 / explainer / 摘读 / Field Note / 学习笔记 / 报告"
- ✅ 内容是长文翻译/摘读, 自然有段落叙事而不是"分镜表"
- ✅ 准备发到群里 / 邮件 / S3 链接让别人**自己读完**, 不是演讲讲给别人听
- ✅ 需要 FAQ / 折叠区 / 代码片段 / 引文 / 链接外跳的 web-native 元素
- ❌ 用户明说要"演讲 PPT / slides / deck / 现场分享" → 用风格 A/B
- ❌ 内容主要是数据 / KPI / 章节切换演讲节奏 → 用风格 B 瑞士

## 横版 vs 竖版

| | 竖版 `template-doc-portrait.html` | 横版 `template-doc-landscape.html` |
|---|---|---|
| 内容栏宽 | 760px max (移动友好) | 1320px max + **单栏全宽** (居中) |
| 适合 | 手机 / iPad / 单人阅读 | 桌面屏 / 横屏分享 / 投屏导出 PDF |
| 章节结构 | 线性单栏 | **单栏全宽** (chrome 顶 + 主体 + chrome 底) |
| 网格 | reasons 2 列, FAQ 单列 | reasons 3 列, use cases 3 列, FAQ 2 列 |
| 默认 | 推荐 | 当用户明说"横屏 / 桌面优先 / 多列展示" 或要导 PDF |

> ⚠️ **横版 v3 起强制单栏全宽**, 不再做"左侧 240px sticky 栏 + 右侧 1fr 主体"那种印刷书排版.
> 章节标识只允许出现在顶 chrome / 底 foot **二选一**, 不允许第三处. 详见 § 单栏全宽基线 v3.

**问用户**: 不确定时让用户选, 或推荐竖版 (移动 + 桌面通吃, 体验更普世).

## 模板组成

两个模板都是**完整可运行**的单文件 HTML, 包含:

- **Hero**: 标题 / kicker / lead / 作者 by-line / TL;DR (横版还有 §索引)
- **§01 论点 / Thesis**: 短列表 + pull quote
- **§02 理由 / Why**: 多列 reasons grid (2-3 列)
- **§03 实战 / In Practice**: use cases + 代码 prompt 框
- **§04 FAQ**: `<details>` 折叠
- **§05 收束 / Closing**: pull quote + numbered rules

每个块的 CSS 类都有语义化命名 (`.tldr`, `.pull`, `.uc`, `.rule`), 用户改内容时不需要碰 CSS.

## 6 套颜色 (与 Skill 原表绑定)

文档形态用单一 accent + 中性背景, 最契合 Skill 已有的 9 套主题. 横版/竖版都可以套用以下任一组:

### Swiss 系 (4 套, 白底 + 单一高饱和 accent)

| 主题 | accent | accent-rgb | 强调字策略 |
|---|---|---|---|
| 🔵 IKB 克莱因蓝 (默认) | `#002FA7` | `0,47,167` | accent 色 + weight 600 + 底色高亮带 |
| 🟠 安全橙 | `#FF6B35` | `255,107,53` | 同上 |
| 🟡 柠檬黄 | `#FFD500` | `255,213,0` | **accent 太浅, 强调字必须改回 ink 黑字, 只用 accent 做高亮带** |
| 🟢 柠檬绿 | `#C5E803` | `197,232,3` | 同柠檬黄, 同样规则 |

### Magazine 系 (2 套实战可用变体)

Magazine 主题原本是 paper+ink 单色调, **没有 accent**. 文档形态需要一个 accent 用于链接 / 编号 / FAQ open 状态, 因此从 ink 派生:

| 主题 | paper | ink | 派生 accent | 派生 ink-soft |
|---|---|---|---|---|
| 🌿 森林墨 | `#f5f1e8` | `#1a2e1f` | `#2d5a35` 中绿 | `#3d4f43` |
| 🍂 牛皮纸 | `#eedfc7` | `#2a1e13` | `#8b3a1a` 烧赭石 | `#4a3a2a` |

(其他 Magazine 主题如靛蓝瓷/沙丘也可派生, 按需调.)

### 换色操作 (3 行 CSS)

打开模板的 `<style>` 块开头 `:root{...}`, 改 3 个变量:

```css
:root {
  --accent:      #FF6B35;       /* 换主色 */
  --accent-rgb:  255,107,53;    /* 同主色的 RGB */
  --accent-soft: rgba(255,107,53, .16);  /* 高亮带, alpha 0.16-0.42 看主色饱和度 */
}
```

**Magazine 系还要换 paper / ink 三件套**:

```css
:root {
  --paper:    #f5f1e8;     /* 米黄底 */
  --paper-2:  #ece7da;     /* prompt box 底 */
  --ink:      #1a2e1f;     /* 主文字 */
  --ink-soft: #3d4f43;     /* 段落正文 */
  --ink-helper: #7a8a7e;   /* meta / kicker */
  --rule:     #d8d3c2;     /* 分割线 */
  --accent:   #2d5a35;
  --accent-rgb: 45,90,53;
  --accent-soft: rgba(45,90,53, .16);
}
```

## 强调字硬规则 (黑体没真斜体)

模板默认中文字体是 **PingFang SC / 苹方** (无衬线 / 黑体). 黑体没有真斜体, 浏览器 fake italic 会糊. 因此 `<em>` 标签:

- ❌ 不要用 `font-style: italic`
- ✅ 用 `color: var(--accent)` + `font-weight: 600`
- ✅ 在正文 (非标题) 中, 加 **底部高亮带**:
  ```css
  background: linear-gradient(to bottom, transparent 65%, var(--accent-soft) 65%);
  padding: 0 2px;
  ```
- ✅ 标题里的 `<em>`: 只用纯色 + weight, 不加底色 (太花)

**浅色 accent (黄/绿) 例外**: 文字颜色保持 `var(--ink)` 黑色, 只让高亮带保留 accent 色. 否则浅黄/浅绿文字在白底上对比度不够.

## 字号体系 (照 Thariq 官方比例)

```
h1 (页面主标题)   38px / weight 600 / line-height 1.18
h2 (章节标题)     26px / weight 600 / line-height 1.25
h3 (小节标题)     19px / weight 600 / line-height 1.3
body / p          14.5px / line-height 1.65
list / li         14.5px / line-height 1.6
mono / kicker     11-12px / letter-spacing 0.06-0.18em
prompt 代码框     12-12.5px (mono) / line-height 1.6
pull quote        21-22px / line-height 1.45 / 左 2px accent border
```

**横版字号略小** (h1 用 clamp 到 34-52px), 因为视口更宽, 行长更控制.

**不要在文档形态里使用 vw 字号**. 浏览器宽度变化时字号跳跃, 阅读体验崩.

## 单栏全宽基线 v3 (横版必读)

横版 v2 起去掉 240px sticky 左栏后, 整个 main 区从 ~1100px 双栏宽度一下子扩到 ~1300px 全宽, 原 17px 正文行长会冲到 80+ char/行, 章节标题 36px 在大空间里又显单薄. v3 起按下面这套基线重平衡:

```css
/* 顶 / 底 chrome (页眉页脚) */
.bar { font-size: 13px; margin-bottom: 44px; }
.foot { font-size: 12.5px; margin-top: 32px; }

/* 章节头放大 + 头身分隔加深 */
.section-head { display: block; margin-bottom: 60px; }   /* 不再用 240px grid */
.section-head .num { display: none; }                     /* 章节大字砍, chrome 已含 */
.section-head h2 { font-size: 46px; line-height: 1.14; margin-bottom: 16px; letter-spacing: -.02em; }
.section-head .sub { font-size: 17.5px; line-height: 1.6; max-width: 80ch; color: var(--ink-soft); }

/* main 区: 单栏全宽 + 限行长 + 区块呼吸 */
.section-body { display: block; flex: 1; min-height: 0; }
.section-body .gutter { display: none; }                  /* 240px 侧栏小字砍 */
.section-body > .main { gap: 32px; }                       /* 区块间距 20→32 */

/* 列表 / 引用 (限行长) */
ul.bullets { max-width: 92ch; }                            /* 宁少行也别拉爆行长 */
ul.bullets li { padding: 20px 0 20px 32px; font-size: 17.5px; line-height: 1.7; }
ul.bullets li b { font-weight: 700; color: var(--ink); }
.pull { font-size: 25px; line-height: 1.5; padding: 16px 0 16px 32px;
  margin-top: 32px; border-left-width: 5px; max-width: 76ch; }

/* 卡片 (reasons 3×2, rules 3 卡, uc 3 列): 单栏全宽 → padding 必须放大 */
.reason { padding: 36px 36px; gap: 14px; }
.reason h4 { font-size: 25px; line-height: 1.22; margin-top: 6px; }
.reason p { font-size: 15.5px; line-height: 1.62; }

.uc-grid { gap: 32px 32px; }
.uc { gap: 14px; }
.uc h4 { font-size: 21px; }
.uc p { font-size: 15px; line-height: 1.62; }
.uc.starter { padding: 26px 28px; }
.uc.starter p { font-size: 16px; line-height: 1.65; }

/* FAQ 双列, gap 拉开 */
.faq-grid { gap: 0 64px; }
.faq-item { padding: 22px 0; }
.faq-item .q { font-size: 18px; line-height: 1.4; margin-bottom: 12px; }
.faq-item .a { font-size: 15px; line-height: 1.7; }

/* closing rules (3 卡) */
.rule { padding: 32px 32px; gap: 14px; }
.rule h4, .rule h5 { font-size: 24px; line-height: 1.22; }
.rule p { font-size: 15.5px; line-height: 1.62; }

/* page-level: 给 .body 一个 max-width 限制, 太宽就居中 */
.body { max-width: 1320px; margin-left: auto; margin-right: auto; width: 100%; }
```

**为什么这套数字**:
- `h2 46px / 正文 17.5px = 2.6×` — 单栏全宽下需要 ≥2.5× 才有头身气场 (双栏时 36/17 = 2.1× 也够, 因为左栏分摊视觉重量)
- `max-width: 92ch ≈ 13.7em × 92` — 17.5px × 92ch 大约 1080px, 留出右侧 220px 留白避免阅读断裂
- `.body 1320px 居中` — 16:9 1600px 宽屏导 PDF 时主体居中, 边距 140px × 2 视觉舒适
- `卡 padding 36×36` — 全宽下平均 433px/卡, 24px padding 显憋屈, 36px 才有"卡片感"
- `lh 1.7` — 行高从 1.6 拉到 1.7, 单栏全宽下大量正文需要"喘息"

**反例 (踩过的)**:
- 横版 v2 (去左栏后没调字号) — NYX 评 "整个页面布局不流畅, 字号和区块大小要调整再协调一点"
- 直接照抄竖版 17px 行高 1.6 → 横版 80+ char 行长 → 视觉太散

## 语义化结构 (复用模板时不要破坏)

```html
<div class="page">                    <!-- 竖版 / .wrap 是横版 -->
  <div class="bar">…</div>            <!-- 顶部状态栏 -->
  <header class="hero">
    <div class="kicker">…</div>       <!-- 小标 -->
    <h1>…</h1>                        <!-- 主标题 -->
    <div class="by">…</div>           <!-- 作者元数据 -->
  </header>

  <div class="tldr">…</div>           <!-- 1 句摘要 (强烈推荐) -->

  <section class="s" id="thesis">…</section>     <!-- 多个 §section -->

  <div class="closing">…</div>        <!-- 收尾卡片 (numbered ol) -->
  <div class="foot">…</div>
</div>
```

每个 `<section class="s">` 内必填:
- `<h2>` (主标题)
- `.sub` (副标题, 一句话引导)
- 主体 (`.section-body > .main` 直接段落 / 列表 / 卡片网格)

> ⚠️ **不要再用** `.section-head .num` (§ 编号 + 英文章节名 mono 大字) 或 `.section-body .gutter` (240px 侧栏小字) — 这些和顶 chrome 重复, 一律砍 (见 § 单栏全宽基线 v3).

## 工作流速查

1. **拷模板**: `cp <SKILL_ROOT>/assets/template-doc-{portrait|landscape}.html 项目/index.html`
2. **改 `<title>`** 和 `.bar` 的项目名 / 日期
3. **改 :root 颜色** (3 行 Swiss / 9 行 Magazine)
4. **改 hero h1 / lead / TL;DR**
5. **替换 §section 内容** —— 段落用 `<p>`, 列表用 `ul.bullets`, FAQ 用 `<details>`
6. **强调字** 用 `<em>`, 不要 inline `font-style:italic`
7. **prompt 代码块** 用 `<pre class="prompt">…</pre>`
8. **横版** 必查 § 单栏全宽基线 v3, 字号 + 卡 padding + .body max-width 全部按 v3 来 (不能用 v2 旧值)
9. **本地预览**: `open 项目/index.html` (浏览器直开, 无需 server)
10. **导 PDF** (横版): `chrome --headless --print-to-pdf` + 模板内置 `@page { size: 1600px 900px; margin: 0 }`

## 不要做的事

- ❌ 不要把 doc 模板套上 PPT 的翻页 JS / WebGL 背景 (那是风格 A/B 的事)
- ❌ 不要在 doc 里出现 vw 字号 (除横版 hero h1 已用的 clamp 例外)
- ❌ 不要给 `<em>` 加 `font-style:italic` (黑体伪斜体糊)
- ❌ 不要为浅色 accent (黄/绿) 把强调字本身染成 accent 色 (对比度不够)
- ❌ 不要混用横版竖版的 CSS class (网格列数不一样, 错位会很明显)
- ❌ 不要用任意 hex (Skill 9 套预设之外), 委婉拒绝并展示预设让选
- ❌ **不要做横版 240px sticky 左栏** (`.section-head { grid-template-columns: 240px 1fr }`) — v3 起强制单栏全宽, 章节标识只允许出现在顶 / 底 chrome **二选一**
- ❌ **不要在内容区放 `.section-head .num` 或 `.section-body .gutter`** — 跟顶 chrome 重复, 砍
- ❌ **不要用 v2 字号**做横版导出 PDF — 必须按 § 单栏全宽基线 v3 重平衡 (h2 46 / 正文 17.5 / 卡 padding 36×36 / .body 1320 居中)

## 内容驱动结构 (横版必读)

横版 `template-doc-landscape.html` 自带 6 .page (Thariq 文章作为示例填充). **不要死扣 6 页** —— `.page` 是积木, 按用户内容章节数任意增删 (典型范围 3-10 页).

| 用户内容 | 推荐拼装 | 总页数 |
|---|---|---|
| 1 章短文 (论点 + 几例) | cover + thesis + closing | 3 |
| 3 章中文 (论点 + 解释 + 收束) | cover + thesis + reasons + closing | 4 |
| 5 章长文 (论点 + 解释 + 案例 + FAQ + 收束) | cover + thesis + reasons + cases + faq + closing | 6 (默认) |
| 8 章超长文 | cover + (thesis × 2) + reasons + (cases × 2) + faq + closing | 8 |
| 简单 explainer (无 FAQ) | cover + thesis + reasons + closing | 4 |
| 周报 / 状态报告 (大量数字) | cover + thesis (with metric-row) + closing | 3 |

**核心原则**: layout 是积木, **按内容定 layout**, 不是按 layout 凑内容. 详见 `references/doc-components.md`.

## 拷模板后的工作流 (横版)

1. `cp <SKILL_ROOT>/assets/template-doc-landscape.html 项目/index.html`
2. `grep -n 'REPLACE:' 项目/index.html` — 列出所有要替换的 [REPLACE:xxx] 锚 (~20 个)
3. 改 `:root` 4 行换主题色 (`--accent` / `--accent-rgb` / `--accent-soft` / `--accent-text`)
4. 按用户内容章节数, 删 / 加 .page (不需要的章节直接删整 div, 缺章节按 `references/doc-components.md` § layout-X 复制 skeleton)
5. 替换每个 [REPLACE:section-N] 标记下的 h2 / sub / 主体内容
6. **重要**: 每页内容必须填到 .page 的 ≥85% 高度 (1600×900). 内容少就用 `metric-row` / 6 卡 grid / FAQ 双列填; 不要让某页空 50%.
7. 浏览器打开 `项目/index.html` 看 (HTML 直出, 6 页竖向堆叠 + 阴影)
8. 导 PDF (可选): `chrome --headless --print-to-pdf=out.pdf --no-margins --print-to-pdf-no-header --hide-scrollbars --virtual-time-budget=6000 file://...`

## 锚点示例

参考 Thariq 官方示例 (各种 doc-style 实战):
- https://thariqs.github.io/html-effectiveness/
- https://thariqs.github.io/html-effectiveness/16-implementation-plan.html (规划文档)
- https://thariqs.github.io/html-effectiveness/14-research-feature-explainer.html (技术 explainer)
- https://thariqs.github.io/html-effectiveness/11-status-report.html (周报)
