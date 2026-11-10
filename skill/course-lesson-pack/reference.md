# Reference — 模板与检查表

配套 [`SKILL.md`](SKILL.md)。复制后改内容，不要改结构。

---

## A. `transcript.md` 骨架（12 页）

```markdown
# Lesson NN — <Title>

**Module id:** moduleNN-slug
**Lab:** <lab-id>
**Tracks:** A (real shell) · B (browser lab)
**Target length:** 5–8 min · 60–80 sentences

## Slide 1 — <Title>

<2–4 句：这是什么、学完能做什么。不要剧透最终数字。>

## Slide 2 — Where this is used

<真实场景里的对应物 + 为什么值钱 + 真实规模。这一页必须在数字之前：
学生看完前两页要能说出"这东西干什么用"。>

## Slide 3 — The situation

<你有什么 / 要什么；点出矛盾。>

## Slide 4 — The method

<主循环；说清每一步在干什么。>

## Slide 5 — The instance / test graph

<结点、边、权重；或模块、外框、golden 坐标。为什么用这么小的图。>

## Slide 6 — Baseline

<golden 逐格读出来；把关键指标算一遍。>

## Slide 7 — First attempt fails

<最省事的做法怎么失败；把错因说穿。>

## Slide 8 — The correct answer

<和上一步逐点对比；指出什么变了、什么没变。>

## Slide 9 — Read the panel

<真实工具面板三块：metrics / status / history；怎么读。>

## Slide 10 — The bounds

<哪条规则把自由卡死；为什么只有这么几个合法选项。>

## Slide 11 — The one trap

<1 个真正的坑：症状 + 为什么合法不等于好 + 怎么看出来。
 宁少勿滥：定义复述型的"坑"直接删。>

## Slide 12 — Your turn

<清单 3–5 步；下一课一句；不重复讲已教内容。>
```

**写作约束**

- 一句一个动作；单句 ≤ 22 词。
- 每页至少一句「所以呢」。
- 术语首次出现给中文/解释；全程同一个词。
- 不写「这个视频」「接下来我们」这类元话术（除非真的在指路）。

---

## B. 页面区块骨架（HTML 结构）

```html
<header class="hero">
  <p class="kicker">PARTITIONING · LAB 07</p>
  <h1>Recursive bisection</h1>
  <p class="promise">From one clean cut to four parts.</p>
  <ul class="chips"><li>5 min</li><li>k = 2 → 4</li><li>cut 3 → 13</li></ul>
  <a class="cta" href="#lab">Try the lab</a>
</header>

<section id="outcomes">   <!-- 3–5 条「学完你能…」 -->
<section id="prereq">     <!-- 2–3 个概念 + 回看链接 -->
<section id="picture">    <!-- 1 张主图 + 3 条要点 -->
<section id="worked">     <!-- 跟做表格：step / parts / cut -->
<section id="lab">        <!-- §5 实验：状态面板 + 操作区 + 校验 -->
<section id="practice">   <!-- 3–5 个任务，<details> 折叠答案 -->
<section id="pitfalls">   <!-- 3 张卡：症状 / 原因 / 修法 -->
<section id="quiz">       <!-- 6–8 题，判分 + 解析 -->
<section id="glossary">   <!-- 8–12 条 -->
<section id="video">      <!-- 播放器 + 章节时间戳 -->
<section id="downloads">  <!-- vtt/srt/pdf/png/md -->
<section id="next">       <!-- 下一课 + 参考 -->
```

**章节时间戳（视频索引）示例**

```html
<ol class="chapters">
  <li><button data-t="0">0:00 The situation</button></li>
  <li><button data-t="42">0:42 The loop</button></li>
  <li><button data-t="118">1:58 First split</button></li>
</ol>
```

---

## C. `quiz.json` 结构与出题

```json
{
  "id": "lab07-recursive-bisection",
  "title": "Recursive bisection — check yourself",
  "items": [
    {
      "id": "q1",
      "stem": "After ABC | DE, which part does recursive bisection split next?",
      "choices": ["ABC", "DE", "Both", "Neither"],
      "answer": 0,
      "explain": "The loop always splits the largest current part, so ABC (size 3) goes first."
    }
  ]
}
```

**出题规则**

- 6–8 题；覆盖：概念 2、计算 2、边界/坑 2、迁移 1–2。
- 每题 4 个选项，干扰项要「像真的会犯的错」。
- `explain` 必须说「为什么对」+「错项错在哪」，不能只写「因为 A」。
- 至少 1 题考「停在哪」（k=3 vs k=4）。
- 至少 1 题给具体图，要求算 cut，答案可手算验证。

**一道好题的形状**

> Graph: A–B 5, B–C 4, A–C 1, C–D 2, C–E 1, D–E 5.
> Split into `AB | CDE`. What is the cut?
> A 6 · B 7 · C 8 · D 13
> explain: 跨边是 A–C 1、B–C 4、C–D 2、C–E 1，合计 8；13 是把 D–E 也算进去的错。

---

## D. 实验设计单（写代码前先填）

```markdown
### Lab: <name>

- 目标：学完能 <一句话>
- 阶梯：L2（自由操作） / L3（加约束）
- 图/数据：<结点、边、权重、pin>
- 状态：parts, cut, history, mode, hintsUsed
- 阶段：
  1) 热身：<2 步，几乎不会错>
  2) 主任务：<3–4 步，含 2 个决策点>
  3) 挑战：<1 个开放题，允许不同解>
- 决策点：
  - D1：<选哪块切> → 判定规则 <largest part> → 错误解释 <...>
  - D2：<停不停> → 判定 <k 达标?> → 解释 <...>
- 校验：<同时查 parts 与 cut；diff 指到步>
- 提示：L1 方向 / L2 方法 / L3 答案
- 重置：<回起点，保留历史可选>
- 真实计算：<穷举/DP；n≤8 直接枚举>
- 验收：<三遍：不看视频能过 / 点错有解释 / 刷新可恢复>
```

---

## E. 机器门伪代码

```python
# 1. 容器
probe = ffprobe(video)
assert probe.has_video and probe.has_audio and not probe.has_subtitle
assert (probe.w, probe.h) == (1920, 1080)
assert abs(probe.duration - wav_duration) < 0.05

# 2. 页/帧
frames = load_manifest()            # [{page, t0, t1, file}]
assert frames[0].t0 == 0 and frames[-1].t1 == duration
for a, b in zip(frames, frames[1:]):
    assert abs(a.t1 - b.t0) < 1e-3

# 3. 字幕
for lang in ("en", "zh"):
    cues = parse_vtt(f"subs-{lang}.vtt")
    assert len(cues) == sentences_total
    for cue, sent in zip(cues, sentences):
        assert sent.page_start <= cue.start <= sent.page_end
        assert cue.start < cue.end <= sent.page_end
        assert abs(cue.start - sent.t0) <= 0.2
    for a, b in zip(cues, cues[1:]):
        assert a.end <= b.start + 1e-3

# 4. 抽帧（每页 >= 2，首句 + 中间句；只抽中间句会漏掉其它句的焦点错位）
for page in pages:
    for sent in (page.sentences[0], page.sentences[len(page.sentences) // 2]):
        img = grab(video, mid(sent))
        assert has_red_box(img)          # 红框像素占比阈值
        assert has_badge(img, page.n)    # 右下角徽标
        assert bottom_band_clean(img)    # 字幕带无烧录
        assert margins_intact(img)
        assert no_tofu_glyph(img)        # 无缺字形方框（禁用 ∈ ✓ ✗ 的直接后果）

# 5. 网站（有站才跑）
html = read("deliverable/index.html")
assert html.count("</body>") == 1 and html.count("</html>") == 1   # 装配守卫
for ref in refs(html): assert fetch(ref).status == 200            # 含 JS 拼的 slides/NN.png
if bilingual:
    assert '<button id="btn-zh"' in html and '<button id="btn-en"' in html
    # 切语言后：动态文案 / 已生成 DOM / quiz 已答状态 都要跟着变（浏览器实测，不能只查静态 HTML）
```

---

## F. 独立审：派单模板与 Orders 格式

**派单（给 subagent）**

```text
你是独立教学审核，不是制作方。先读：
- .cursor/skills/course-lesson-pack/SKILL.md
- learning/.cursor/skills/video-secretary/CONSTRAINTS.md
- <lesson>/transcript.md
- <lesson>/deliverable/index.html
- <lesson>/frames_review/*.png（每页一帧）

按顺序输出到 <lesson>/review.md：
1) ## Teaching judgment（Q1–Q4，各一句理由）
2) ## Middle-school perspective（3 问 + PASS/FAIL）
3) ## Evidence（逐页：第 N 页第 M 句；红框在不在讲的东西上）
4) ## Orders（只在 FAIL 时）：文件 + 页/行 + 换成什么
5) ## Verdict：PASS / FAIL

规则：不许只说「更口语」「再丰富点」；每条 Order 必须能让下一轮不看聊天记录就改。
```

**Orders 写法（正例）**

```markdown
- [ ] transcript.md Slide 7, sentence 3：
      原文 “D and E must split, so the cut jumps to thirteen.”
      改为 “Splitting D and E cuts the heaviest edge, so the total jumps from eight to thirteen.”
      原因：原句没说清 +5 从哪来。
- [ ] assets/s07-split3.py：红框从 4 条跨边容器改为 D–E 单行（y=596..636），
      并加该行底色高亮。
- [ ] subs-zh.vtt cue 41：“停在第三块” → “切到三块为止”，避免读成「第 3 块」。
```

---

## G. 交付检查表（上传前逐项打勾）

**内容**

- [ ] 12 页稿，每页 4–7 句；总句数 60–80
- [ ] **第 2 页是「用在哪」**：真实对应物 + 为什么值钱 + 真实规模
- [ ] 5 个关键数字与 goldens 一致（**跑代码核对，不抄源码**），页面与视频口径相同
- [ ] 中文术语表统一；无「第 X 块」歧义
- [ ] 坑：只留真正会让人白干一场的（1 个足矣）；没有定义复述型的"坑"
- [ ] 6–8 题，每题有解析；至少 1 题算 cut / 死区 / 密度
- [ ] 正文里没有改版说明、没有"这课只留…"这类制作理由

**视频**

- [ ] 软字幕双轨；mp4 无字幕流
- [ ] 一句一画面；红框跟讲且**不圈整块容器**；页码徽标
- [ ] 机器门 PASS；**抽帧每页 ≥ 2 张**全过
- [ ] 时长与 `full.wav` 一致；可 seek

**网站**

- [ ] 10–12 区块；正文达标（双语时两个语言版本各自达标）
- [ ] 实验至少 L2：能点错、有解释、能重置
- [ ] 390 px 无横向滚动；键盘可用
- [ ] 所有资源 200（含 JS 动态路径）；console 无 error
- [ ] `</body>` / `</html>` 各 1 次（装配脚本守卫）
- [ ] 双语：开关存在，切语言后动态文案 / 已生成 DOM / 已答状态都跟着变

**流程**

- [ ] `review.md` 有 Q1–Q4 + 中学生视角 + 证据句
- [ ] `orchestrator-state.md` 记录 round / verdict / next
- [ ] `docs/02-上传步骤.md` 可照抄
- [ ] `deliverable/` ≤ 12 MB，相对路径，含 README.md

---

## H. 可直接复制的片段（本技能自包含，不依赖某个 lab 目录）

> 下面四个片段是「任何一课都能用」的最小实现。**不要**去某个旧 lab 目录里找脚本 ——
> 把它复制到新 lab 的 `verify/` 或 `assets/` 下改路径即可。

### H1 数字实测脚本（`verify/check-numbers.mjs`）

```javascript
// node eda-labNN/verify/check-numbers.mjs
// 直接 import 平台的 core 模块，断言每个要讲的数字；不要凭印象抄数值。
import {
  OUTLINE, TINY_MODULES, GOLDEN_PACK, SOFT_PACK,
  moduleAreaSum, deadspace, density, isLegalPacking, legalityReport,
} from "../../<course-repo>/platform/assets/<core>.js";

const line = (k, v) => console.log(String(k).padEnd(40), v);
const ok = (cond, label) => console.log(`${cond ? "PASS" : "FAIL"}  ${label}`);

line("outline", `${OUTLINE.w} x ${OUTLINE.h} = ${OUTLINE.w * OUTLINE.h}`);
for (const m of TINY_MODULES) line(`module ${m.id}`, `${m.w}x${m.h} area=${m.w * m.h}`);
line("area sum", moduleAreaSum());
line("deadspace", deadspace());
line("density", density().toFixed(4));

ok(isLegalPacking(GOLDEN_PACK), "golden legal");
ok(isLegalPacking(SOFT_PACK), "soft pack legal");
line("bad case report", JSON.stringify(legalityReport(BAD_PACK)));  // 画面要用它的原文
```

要求：**每个要上画面的数字都有一行 `ok(...)`**；失败时脚本必须非零退出，别让错数字混过去。
把输出贴进 `orchestrator-state.md`，标注"哪一次运行"。

### H2 中文字幕条长检查（塞进 `_subs_*.py` 的 `main()` 之前）

```python
def cue_width(s: str) -> float:
    """全角当量：CJK/全角 = 1，ASCII = 0.5"""
    return sum(1.0 if ord(ch) > 0x2E80 else 0.5 for ch in s)

def check_cues(cues: list[str]) -> None:
    bad = []
    for i, cue in enumerate(cues, 1):
        lines = cue.split("\n")
        total = cue_width(cue.replace("\n", ""))
        # 单行 cue 由播放器自动折行：只看总量；显式换行才逐行看
        over = total > 44 if len(lines) == 1 else (max(map(cue_width, lines)) > 22 or total > 44)
        if over or len(lines) > 2:
            bad.append(f"cue {i}: lines={[round(cue_width(l), 1) for l in lines]}")
    if bad:
        raise SystemExit("zh cue too long:\n  " + "\n  ".join(bad))
```

### H3 双语页面骨架（CSS + 开关 + 重渲染钩子）

```html
<body class="lang-zh">
<button type="button" id="btn-zh" aria-pressed="true">中文</button>
<button type="button" id="btn-en" aria-pressed="false">English</button>
<p><span class="zh">中文</span><span class="en">English</span></p>
```

```css
body.lang-zh .en { display: none !important; }
body.lang-en .zh { display: none !important; }
```

```javascript
const isEN = () => document.body.classList.contains("lang-en");
const L = (zh, en) => (isEN() ? en : zh);          // 所有 JS 动态文案都过这里

function apply(lang) {
  document.body.classList.toggle("lang-en", lang === "en");
  document.body.classList.toggle("lang-zh", lang !== "en");
  document.documentElement.lang = lang === "en" ? "en" : "zh-CN";
  try { localStorage.setItem("<lab>-lang", lang); } catch (e) {}
  // 已生成的 DOM 必须重建（这三类最容易漏）
  window.__renderChapters?.();
  window.__renderQuiz?.();
  window.__rerenderLab?.();      // 内部要保住：quiz 已答态、待答弹窗、当前提示
}
document.getElementById("btn-zh").onclick = () => apply("zh");
document.getElementById("btn-en").onclick = () => apply("en");
apply(localStorage.getItem("<lab>-lang") || "zh");
```

**quiz 已答状态**用一张表保住，重绘时重放：

```javascript
const QUIZ_ANSWERS = {};
function revealAnswer(item, opts, expl, chosen) {
  const right = item.type === "true_false" ? (chosen === 0) === item.answer : chosen === item.answer;
  [...opts.children].forEach((c) => (c.disabled = true));
  opts.children[chosen].classList.add(right ? "correct" : "wrong");
  if (!right) opts.children[item.answer].classList.add("correct");
  expl.classList.add("show");
}
// renderQuiz 里：if (QUIZ_ANSWERS[qi] !== undefined) revealAnswer(...)
```

### H4 网站装配守卫（`assets/_assemble_site.py`）

手工把 `<script>` 尾巴粘到 body 上，闭合标签必然叠成 2–3 组且**不报错**。用脚本：

```python
import re
from pathlib import Path
ROOT = Path(__file__).resolve().parent
CLOSERS = re.compile(r"(?:\s*</body>\s*</html>\s*)+$")

body = CLOSERS.sub("", (ROOT / "_site_template_new.html").read_text(encoding="utf-8"))
tail = CLOSERS.sub("", (ROOT / "_site_script_tail.html").read_text(encoding="utf-8"))
page = body.replace("<!--SCRIPT_TAIL-->", tail + "\n</body>\n</html>\n")
assert page.count("</body>") == 1 and page.count("</html>") == 1, "duplicated closers"
(ROOT / "_site_template.html").write_text(page, encoding="utf-8")
```

拆成 `_site_template_new.html`（正文）+ `_site_script_tail.html`（实验 JS）的好处：
改文案不用碰 JS，改实验不用碰文案。

### H5 机器门里"新增功能"的三条自查

加任何新功能（双语、挑战、提示系统）后，先自己按**入口清单**过一遍，再交审：

1. **所有可见入口**：按钮 / 阶段名 / 提示 / 报错 / 弹窗 —— 每个都切一次语言或换一次状态；
2. **已生成的 DOM**：章节、quiz、进度列表是 JS 建好后不更新的，切语言是否重建；
3. **状态保活**：已答的题、已用的提示、进行到一半的挑战，切换后是否还在。

---

## I. 动效片段（视频与站点）

> 原则见 SKILL §4.5：**只给"因果关系"做动画**，不为热闹做动画。

### I1 视频：焦点框滑动（帧内动效，不改讲稿）

一句话换焦点时，红框从上一句的位置**滑过去**，比硬切更不容易让人跟丢。做法是把两个焦点框
按 `ease-out` 插值出 3–4 个中间框，各出一帧：

```python
def ease_out(t: float) -> float:
    return 1 - (1 - t) ** 3

def lerp_box(a, b, k, n):
    t = ease_out(k / (n - 1)) if n > 1 else 1.0
    return tuple(round(a[i] + (b[i] - a[i]) * t) for i in range(4))

# 在 _make_assets.py 里：每页的 stage 函数返回 (img, box)，
# 由外层统一 finish(img, box)；要动效就额外产出 lerp_box(prev, cur, k, n) 的变体
```

成本：每页多 3–4 帧、渲染慢一点；**句子数不变**，`slide_timings.json` 也不用动
（新帧只是插在同一句的时间里，`from_local` 依次递进）。

### I2 视频：页间过场（经底色，不要直接叠两页）

硬切会让 12 页像 PPT，但**不要用交叉淡入**：两页版式不同，叠在一起会出现两套标题、
两行红框，静止看像重影（lab08 实际做出来就是这样）。正确做法是**经底色过场**：
上一页淡出到页背景色，再从背景色淡入新页。

```python
from PIL import Image

BG = Image.new("RGB", (1920, 1080), "#0b1220")   # 与幻灯片底色一致

def dip(prev: Image.Image, nxt: Image.Image, half: int = 3):
    out = [Image.blend(prev, BG, j / (half + 1)) for j in range(1, half + 1)]
    out += [Image.blend(BG, nxt, j / (half + 1)) for j in range(1, half + 1)]
    return out          # 6 帧，总 0.24 s
```

注意：这些帧属于**新页**的时间窗（`from_local` 从 0 开始），否则机器门的
"帧窗口铺满且首尾相接"会挂。总时长不变，只是新页前 0.24 s 是过场。

### I3 站点：SVG 入场 / 判定脉冲 / 指标条

```css
/* 模块落位：缩放 + 淡入，0.18s */
@keyframes pop { from { opacity: 0; transform: scale(.92); } to { opacity: 1; transform: scale(1); } }
.fp-module { animation: pop .18s ease-out; transition: transform .18s ease-out; }

/* 非法冲突：描边脉冲两次 */
@keyframes alert { 0%,100% { stroke: #ef4444; stroke-width: 1.5 } 50% { stroke: #fca5a5; stroke-width: 4 } }
.fp-bad { animation: alert .45s ease-in-out 2; }

/* 压紧度条：宽度随 bbox 变化 */
.tight-bar { height: 6px; background: var(--teal); transition: width .25s ease-out; }

@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !important; }
}
```

```javascript
// bbox 用 SVG 属性动画（SMIL），元素重建也能播
const r = document.createElementNS(SVGNS, "rect");
r.innerHTML = `<animate attributeName="width" from="0" to="${w}" dur="0.25s" fill="freeze"/>`;
```

**判定要"能看见"**：非法时给冲突的两个模块加 `.fp-bad`（描边脉冲），而不是只把 reason 变红。
颜色变化在余光里看不见，描边脉冲看得见。

### I4 站点：拖拽（必须给非拖拽替代）

```javascript
let drag = null;
svg.addEventListener("pointerdown", (ev) => {
  const id = hitModule(ev);                 // 用 canvasToCell 反向算格子
  if (!id) return;
  selected = id;
  drag = { id, start: cellOf(ev), moved: false };
  svg.setPointerCapture(ev.pointerId);
  render();
});
svg.addEventListener("pointermove", (ev) => {
  if (!drag) return;
  const c = cellOf(ev);
  if (c.x === pack[drag.id].x && c.y === pack[drag.id].y) return;
  pack[drag.id] = { ...pack[drag.id], x: c.x, y: c.y };
  drag.moved = true;
  render();                                  // 5 个模块，整页重绘够快
});
svg.addEventListener("pointerup", (ev) => {
  if (!drag) return;
  svg.releasePointerCapture(ev.pointerId);
  if (drag.moved) afterChange(`${drag.id} → (${pack[drag.id].x},${pack[drag.id].y})`);
  drag = null;
});
```

- `touch-action: none` 写在 SVG 上，否则手机拖动会带动页面滚动。
- **必须保留**：点芯片 → 点格子（拖不了的时候用）；方向键 nudge（键盘用户）。
- 拖拽过程中**每次都算 legality**，让用户边拖边看到 reason 变红变绿 —— 这是拖拽最大的教学价值。

### I6 内容动画：对模型插值（**优先做这个**）

转场只是拼接；**内容动画指的是被讲的东西本身在动**。判据：把这一段静音看，
观众能不能只看画面就说出"发生了什么"。

做法是让绘制函数从全局状态取数据，然后在两套"正确状态"之间插值：

```python
# --- 绘制侧 ---
PACK_OVERRIDE = None          # 非 None 时，页面按这个 pack 画
VERDICT_VISIBLE = True        # 动画中先别下结论

def lerp_pack(a: dict, b: dict, t: float) -> dict:
    return {k: tuple(a[k][i] + (b[k][i] - a[k][i]) * t for i in range(4)) for k in a}

def page(stage):
    pack = PACK_OVERRIDE or SOFT_GOLDEN     # ← 唯一改动：不再写死
    fp(d, 128, 268, 50, pack)
    coord_rows(d, (792, 262), pack)         # 坐标表跟着同一份数据走
    if VERDICT_VISIBLE:
        text(d, ..., "legal: true")
    return finish(img, box)

# --- 成片侧 ---
TWEENS = {
    (7, 1): {"packs": ("GOLDEN", "NAIVE"), "secs": 0.70, "frames": 8},   # A 原地长高压到 D
    (8, 0): {"packs": ("NAIVE", "SOFT"),   "secs": 0.90, "frames": 10},  # B/C/D 滑到新位置
}
for j in range(1, n + 1):
    u = 1 - (1 - j / n) ** 2               # ease-out
    A.PACK_OVERRIDE = lerp_pack(pack_a, pack_b, u)
    A.VERDICT_VISIBLE = (j == n)           # 结论最后才出现
    frame = render(slide, stage)
```

要点：
- **帧时长从该句已有的窗口里切**，不是新增时间 —— 这样字幕时间轴、总时长都不用动。
- **和动画同源的文字要一起动**：坐标表、指标数字、进度条读同一份 pack/state。
- **判定延后**：动画中显示"watching…"，停下才出 `legal: false`，否则画面自相矛盾。
- 起步状态最好是**上一个画面的终态**（第 7 页从 GOLDEN 开始变形，第 8 页从 NAIVE 开始重摆），
  观众才能接上"我刚才看到的就是它"。

### I7 逐句揭示：文字/算式跟着旁白出现

比补间更便宜、效果很实：一页里如果有多条并列信息（算式、指标、结论），
**按旁白逐条揭示**，不要让它们一次性砸出来。

```python
MATH_REVEAL = 3            # 1/2/3 表示显示到第几条；静态图默认 3

# 绘制侧：每条内容按级别守卫
if MATH_REVEAL >= 1: text(... "moduleArea 23   outlineArea 80")
if MATH_REVEAL >= 2: text(... "deadspace 80 − 23 = 57")
if MATH_REVEAL >= 3: text(... "density 23 / 80 = 0.2875 = 28.75%")

# 成片侧：用句子起点当切点（不是时间比例）
STEP_REVEALS = {(6, 3): {5: 2, 6: 3}}   # 第 6 页 step3：第 5 句起显示 2 条，第 6 句起 3 条
```

要点：
- 切点用**句子 `t0`**，不要按"平均分"，否则文字会比声音早/晚。
- 揭示顺序要和句子顺序一致；每一级只加内容、不改已显示的内容（避免闪回）。
- 静态导出（slides.pdf / 网页图集）用最高级，保证图和稿一致。
- 适用范围：算式推导、指标清单、对照表、"三个条件"这种并列信息。

### I8 状态演示：让"判定"跟着旁白翻

读面板、读状态栏这类页，最有效的动画不是数字滚动（总量往往不变，滚了反而假），
而是**让判定翻转**：同一页里 `legal: true → false`、`reason: ok → A overlaps D`，
同时把四个总量钉死不动 —— 观众自己就得出"总量不变、只有判定会变"。

```python
PANEL_STATE = 0     # 0 = legal:true / reason:ok；1 = legal:false / reason:A overlaps D

if PANEL_STATE == 0:
    legal_line, reason_line = ("legal: true", GREEN), ("reason: ok", MUTED)
else:
    legal_line, reason_line = ("legal: false", RED), ("reason: A overlaps D", RED)
```

配 `STEP_STATES`（§I7）在第 6 句的起点切换即可。**前提**：那一刻焦点框必须落在这两行上，
否则变化发生在暗区，观众看不见 —— 这是 lab08 实际返工过一次的地方。

### I5 动效预算

| 项 | 上限 | 超了会怎样 |
|---|---|---|
| 视频帧数 | ≤ 句数 × 2.5 | 渲染慢、成片大、机器门抽帧变慢 |
| 单次动效时长 | 0.15–0.3 s | 超过 0.4 s 用户开始等 |
| 同屏同时动画元素 | ≤ 6 | 多了像故障 |
| 站点首屏 | 无自动动画 | 自动播放会抢注意力、也不符合 reduced-motion |
