# Doc-style 组件 / Page Layout 速查 (横版 PPT 化)

> 用于 `assets/template-doc-landscape.html` 的 6 种 page layout + 内嵌组件.
> 模板自带 Thariq 文章作为示例填充, 你按内容性质从下方挑 layout, 替换其中内容.
>
> 配套规则:
> - 单栏全宽字号体系: `references/doc-style.md` § 单栏全宽基线 v3
> - 砍小字 / 装饰编号: `references/checklist.md` § 2c-2 / 2d / 2e / 2f
> - PDF 导出: chrome `--print-to-pdf` + 模板内置 `@page { size: 1600px 900px }`

## 内容驱动结构 — 怎么按章节数选 layout

按用户给的内容章节数, 拼装 .page 序列:

| 用户内容 | 推荐拼装 | 总页数 |
|---|---|---|
| 1 章短文 (论点 + 几例) | layout-1 cover + layout-2 thesis + layout-6 closing | 3 |
| 3 章中文 (论点 + 解释 + 收束) | cover + thesis + reasons + closing | 4 |
| 5 章长文 (论点 + 解释 + 案例 + FAQ + 收束) | cover + thesis + reasons + cases + faq + closing | 6 (默认) |
| 8 章超长文 | cover + (thesis × 2) + reasons + (cases × 2) + faq + closing | 8 |
| 简单 explainer (无 FAQ) | cover + thesis + reasons + closing | 4 |
| 周报 / 状态报告 (大量数字) | cover + thesis (with metric-row) + closing | 3 |

**核心原则**: layout 是积木, 不是模板固定 6 页. **按内容定 layout**, 不是按 layout 凑内容.

---

## layout-1 · Cover (封面 · 双栏)

**何时用**: 文档第一页, 必有.

```html
<div class="page">
  <div class="bar">
    <div>[REPLACE:bar] FIELD NOTE · 项目名 · 日期</div>
    <div><a href="[REPLACE:bar-link]">原文 ↗</a></div>
  </div>
  <div class="body">
    <div class="cover">
      <div class="left">
        <div class="kicker">[REPLACE] USING X · ESSAY 01</div>
        <h1>[REPLACE] 文章主标题<em>带高亮带</em></h1>
        <p class="lead">[REPLACE] 1-2 句话导语</p>
        <div class="by">[REPLACE] 作者 · 出处 · 阅读量</div>
      </div>
      <aside class="right">
        <div>
          <div class="label">TL;DR</div>
          <div class="tldr-body">[REPLACE] 1-2 句总结全文</div>
        </div>
        <ol>
          <li><a href="#thesis"><b>§ 01 论点</b><span>简介</span></a></li>
          <li><a href="#why"><b>§ 02 为什么</b><span>简介</span></a></li>
          <!-- 按章节数加/删 li -->
        </ol>
      </aside>
    </div>
  </div>
  <div class="foot">
    <div>01 / N · COVER</div>
    <div>WRITTEN IN HTML</div>
  </div>
</div>
```

**关键 class**: `.cover` (1.4fr / 1fr 双栏), `.cover .left .kicker / h1 / lead / by`, `.cover .right .label / .tldr-body / ol`

**字号**: h1 64px (PDF 模式 print 已 override), lead 19px, by 13px

---

## layout-2 · Thesis (论点 · bullets + pull + metric-row)

**何时用**: 阐述核心论点, 通常 1-3 个. 结合 pull quote (引文) + metric-row (4 个数字证据) 填满一页.

```html
<div class="page">
  <div class="bar">...</div>
  <div class="body">
    <div class="section-head">
      <div>
        <h2>[REPLACE] 三件事 / 三个变化 / 三条结论</h2>
        <p class="sub">[REPLACE] 1 句引导</p>
      </div>
    </div>
    <div class="section-body">
      <div class="main">
        <ul class="bullets">
          <li><b>[REPLACE] 论点 1。</b>解释...</li>
          <li><b>[REPLACE] 论点 2。</b>解释...</li>
          <li><b>[REPLACE] 论点 3。</b>解释...</li>
        </ul>
        <div class="pull">"[REPLACE] 关键引文 / 金句" — [作者]</div>

        <!-- metric-row · 4 个数字证据填底 -->
        <div class="metric-row">
          <div class="metric">
            <div class="metric-num">[NUM]<span class="metric-unit">单位</span></div>
            <div class="metric-label">[REPLACE] LABEL</div>
            <div class="metric-note">[REPLACE] 一句解释</div>
          </div>
          <!-- 重复 4 次, 第 4 个加 class="metric metric-accent" 黄底突出 -->
        </div>
      </div>
    </div>
  </div>
  <div class="foot">...</div>
</div>
```

**关键 class**: `.bullets` (li 间分割线 + 加粗 b), `.pull` (左 5px accent border + 高亮带 em), `.metric-row` (4 列 grid + 第 4 卡 .metric-accent 黄底)

**何时省略 metric-row**: 论点较空虚 / 论文型, 不强求"数字证据". 但**不加就会页面下半空** — 必须用其他组件填 (例如 `.faq-grid` 或 `.reasons`).

---

## layout-3 · Reasons (理由 · 6 卡 grid 3×2)

**何时用**: "N 条理由 / N 个原因 / N 种好处" 类内容, **6 卡最佳** (3 卡或 8 卡也行, 改 grid-template-columns).

```html
<div class="page">
  <div class="bar">...</div>
  <div class="body">
    <div class="section-head">
      <div>
        <h2>[REPLACE] 六条理由</h2>
        <p class="sub">[REPLACE] 1 句引导</p>
      </div>
    </div>
    <div class="section-body">
      <div class="main" style="padding:0">
        <div class="reasons">
          <div class="reason">
            <div class="n">01 · [TAG]</div>
            <h4>[REPLACE] 标题</h4>
            <p>[REPLACE] 解释...</p>
          </div>
          <!-- 重复 6 次 -->
          <!-- 第 6 卡可加 class="reason starter" 黄底突出 (可选) -->
        </div>
      </div>
    </div>
  </div>
  <div class="foot">...</div>
</div>
```

**关键 class**: `.reasons` (3 列 2 行 grid + 1px 灰间隔), `.reason { padding: 24×28 }` (单卡), `.reason .n` (mono 标签 12px)

**何时换 4 卡**: 改 `.reasons { grid-template-columns: repeat(2, 1fr); grid-template-rows: 1fr 1fr; }` (2×2)

**何时换 9 卡**: 改 `.reasons { grid-template-columns: repeat(3, 1fr); grid-template-rows: repeat(3, 1fr); }` (3×3, 但卡内 padding 要收到 18×20)

---

## layout-4 · Cases (用例 · 6 卡 grid 3×2 with prompt 框)

**何时用**: "N 个用法 / N 个场景 / N 个 example" 类内容, 每条都有具体 prompt / 操作示例. **6 用例最佳**, 第 6 卡可换"起手式 / 总结" 黄底突出.

```html
<div class="page">
  <div class="bar">...</div>
  <div class="body">
    <div class="section-head">
      <div>
        <h2>[REPLACE] 五个用法 + 一个起手式</h2>
        <p class="sub">[REPLACE] 1 句引导</p>
      </div>
    </div>
    <div class="section-body">
      <div class="main" style="padding:0">
        <div class="uc-grid uc-grid-3x2">
          <div class="uc">
            <div class="head-uc"><h4>[REPLACE] 用例标题</h4><span class="tag">01 · TAG</span></div>
            <p>[REPLACE] 描述...</p>
            <pre class="prompt">[REPLACE] Example prompt 单行不超过 ~46 char</pre>
          </div>
          <!-- 重复 5 次 -->
          <!-- 第 6 卡: class="uc starter" 黄底, 内可放总结 / 起手式 -->
          <div class="uc starter">
            <div class="head-uc"><h4>[REPLACE] 起手式 / 总结</h4><span class="tag">06 · JUST DO IT</span></div>
            <p>[REPLACE] 关键提示 / 下一步建议</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="foot">...</div>
</div>
```

**关键 class**: `.uc-grid-3x2` (3 列 2 行, 撑满 .main), `.uc { gap 8px }`, `.uc.starter { 黄底 }`, `.uc .prompt` (mono 11px, margin-top:auto 推底)

**注意**: `.uc-grid-3x2` 自带 `flex: 1` + grid-rows `1fr 1fr` 撑满高度. 不要再加 margin-top.

---

## layout-5 · FAQ (问答 · 2 列 6 块)

**何时用**: 问答型内容, 4-8 条最佳. 适合"是不是..." / "What about..." 类回应.

```html
<div class="page">
  <div class="bar">...</div>
  <div class="body">
    <div class="section-head">
      <div>
        <h2>[REPLACE] 常见的"是不是太……"</h2>
        <p class="sub">[REPLACE] 1 句引导</p>
      </div>
    </div>
    <div class="section-body">
      <div class="main" style="padding:0">
        <div class="faq-grid">
          <div class="faq-item">
            <div class="q">[REPLACE] 问题 1</div>
            <div class="a">[REPLACE] 答案. 可加 <strong>加粗</strong> 或 <code>code</code></div>
          </div>
          <!-- 重复 6 条 -->
        </div>
      </div>
    </div>
  </div>
  <div class="foot">...</div>
</div>
```

**关键 class**: `.faq-grid` (2 列, gap 0/64px), `.faq-item` (上下 1px hairline + padding 14), `.faq-item .q` (17px / 600), `.faq-item .a` (14.5px / 1.65)

**何时换 4 条**: 直接少 4 个 .faq-item; .faq-grid 高度自适应

**何时换 1 列长文**: 改 `.faq-grid { grid-template-columns: 1fr; }`

---

## layout-6 · Closing (收束 · 引文 + 3 rules)

**何时用**: 文档最后一页, 必有. 包含: 总结引文 + 3 条行动 / takeaway 卡.

```html
<div class="page">
  <div class="bar">...</div>
  <div class="body">
    <div class="section-head">
      <div>
        <h2>[REPLACE] 真正让我没切回去的事</h2>
        <p class="sub">[REPLACE] 1 句引导</p>
      </div>
    </div>
    <div class="section-body">
      <div class="main" style="padding:0">
        <div class="pull" style="font-size: 22px; max-width: 80ch;">
          "[REPLACE] 收束金句, 跨语言保留原文 + 译文"
        </div>
        <div class="rules">
          <div class="rule">
            <div class="n">01 · ASK</div>
            <h5>[REPLACE] 短动词 (直接说 / 用链接 / 回灌)</h5>
            <p>[REPLACE] 一句具体做法</p>
          </div>
          <!-- 重复 3 次 -->
        </div>
      </div>
    </div>
  </div>
  <div class="foot">
    <div>N / N · END · WRITTEN IN HTML</div>
    <div><a href="[REPLACE:foot-link]">参考链接 ↗</a></div>
  </div>
</div>
```

**关键 class**: `.rules { 3 列 grid }`, `.rule { padding 24×26 }`, `.rule .n` (mono 标签), `.rule h5` (22px), `.rule p` (15px)

**何时换 4 / 5 卡**: 改 `.rules { grid-template-columns: repeat(4, 1fr); }`; 卡内 padding 收到 18×20

---

## 内嵌组件 (跨 layout 复用)

### `<div class="bar">` 顶部状态栏

```html
<div class="bar">
  <div>[REPLACE:bar] 项目标识 · 日期 · 主题</div>
  <div><a href="[REPLACE:bar-link]">原文 ↗</a></div>
</div>
```

字号 12px / mono uppercase. 跨页保持一致 (项目级标识).

### `<div class="foot">` 底部页脚

```html
<div class="foot">
  <div>[页号 N / 总数 M] · [章节名 e.g. THESIS]</div>
  <div>[REPLACE] 关键词标语 / 下一章关键词</div>
</div>
```

字号 11.5px. 章节名用 mono uppercase, 跟当前 .page 的 h2 主题对应.

### `<ul class="bullets">` 加粗式列表

```html
<ul class="bullets">
  <li><b>关键词。</b>句子...</li>
</ul>
```

字号 17.5px / lh 1.7. li 间 1px hairline 分隔.

### `<div class="pull">` 引文卡

```html
<div class="pull">
  "[REPLACE] 引文" — 作者
</div>
```

字号 25px / lh 1.5. 左 5px accent 竖条. 用 `<em>...</em>` 加高亮带.

### `<div class="metric-row">` 4 数字证据带

```html
<div class="metric-row">
  <div class="metric"> ... </div>
  <div class="metric"> ... </div>
  <div class="metric"> ... </div>
  <div class="metric metric-accent"> ... </div>  <!-- 第 4 个黄底 -->
</div>
```

字号: metric-num 38px / metric-unit 16px / metric-label 10px mono / metric-note 11.5px.

### `<pre class="prompt">` mono 代码框

```html
<pre class="prompt">[REPLACE] 多行 prompt, 单行 ≤46 char 防溢出</pre>
```

字号 11px (uc-grid-3x2 内) / 12px (其他场景). 左 3px ink-helper 竖条.

### `<span class="k">` 键盘 / 命令 chip

```html
<span class="k">/html</span>
```

mono 13px, 浅灰底, 圆角 3px. 用于嵌入正文标识 cmd / key / API.

---

## 输出格式

| 用途 | 命令 | 输出 |
|---|---|---|
| 浏览器看 | `open index.html` | HTML 滚动, 6 卡 1600×900 竖向堆叠 + 阴影 |
| PDF 导出 (16:9 1600×900) | `chrome --headless --print-to-pdf=out.pdf --no-margins --print-to-pdf-no-header --hide-scrollbars file://...` | 6 页 16:9 PDF, 一章一页 |
| 高分辨率截图 (1 页) | `chrome --headless --screenshot=p1.png --window-size=1600,900 file://...` | 1 张 1600×900 PNG (只截首屏) |
| 全文长截图 | `chrome --headless --screenshot=all.png --window-size=1600,5800 ...` | 1 张 1600×5800 PNG (含 6 张卡 + 间距) |

模板自带 `@page { size: 1600px 900px; margin: 0 }` + `.page` 设固定 1600×900px + `page-break-after: always`, 浏览器和 chrome PDF 都直接用同一份模板, 无需切换.

---

## 反例 (踩过的)

- **scrolling 单 .wrap + section.s + 强制 print PPT 化** ❌ — print CSS 跟模板原 CSS 双重 override 打架, hero 双栏 grid 在 PPT 模式下错位, 6 卡溢出被裁. 必须用多 .page 原生 PPT 化.
- **每页只塞 3-4 个 bullet, 下半空 50%** ❌ — NYX 评 "PDF 完全不对". 必须用组件 (metric-row / 6 卡 grid / FAQ 双列) 填满每 page 高度.
- **cases 拆 P4 + P5 各 3 用例** ❌ — 每页占 50%, NYX 评 "页面利用率不足". 合并 6 用例 1 页 (uc-grid-3x2) 才对.
- **section-head .num + sidebar .gutter 重复章节标识** ❌ — 跟顶 .bar 重复. v3 起强制单栏全宽, .num 和 .gutter 都 `display: none`.
- **chrome PDF 横向溢出** ❌ — 不是 viewport 问题 (chrome --print-to-pdf 用 @page 不用 window-size), 是 .page 跟 .body box-sizing 不对. 模板已统一 `* { box-sizing: border-box }`.
