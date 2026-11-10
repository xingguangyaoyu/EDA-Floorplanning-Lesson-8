# Lab 08 — Soft module aspect sizing · 软模块宽高比变形

Floorplanning for EDA 课程第 8 课的可交付包：**视频 + 可切换语言的网站 + 动手实验 + 自测**。

Open the lesson: **[index.html](index.html)** （GitHub Pages 会直接把它作为首页）

---

## 这一课讲什么

一块电路的面积是定的，长和宽却可以换。在「面积不变（w·h = 6）＋ 宽高比落在 [0.5, 2]」的前提下给软模块换形状，
再把周围的硬模块重摆一遍，让整块芯片塞得更紧。

真实芯片里 SRAM、模拟电路、第三方 IP 是**硬模块**（厂家定形状），普通逻辑是**软模块**（门数定面积、形状可弯）——
商用布图工具就是靠变形这些软模块去收缝隙。这一课把同一个循环缩到能用手指数格子的规模。

## 本算例的数字（全部可手算核对）

| 项 | 值 |
|---|---|
| 外框 | 10 × 8 = **80** |
| 模块 | A 3×2（soft，aspect 0.5–2）· B 2×3 · C 2×2 · D 3×1 · E 2×2 |
| 面积和 | 6 + 6 + 4 + 3 + 4 = **23** |
| 死区 | 80 − 23 = **57** |
| 密度 | 23 / 80 = **0.2875（28.75%）** |
| 硬布局（golden） | A(0,0) B(3,0) C(5,0) D(0,2) E(7,0) |
| 软布局（golden） | A(0,0, 2×3) B(2,0) C(4,0) D(4,2) E(7,0) |
| 面积 6 的合法形状 | 只有 2×3 与 3×2（1×6、6×1 越界） |
| 最紧外接矩形 | 6×4 = **24**（23 是质数，零浪费不可达） |

## 包里有什么

| 文件 | 说明 |
|---|---|
| `index.html` | 网站：12 区块，中英可切换，内嵌实验与自测 |
| `video.mp4` | 7:00，1920×1080，英文讲解，**无烧录字幕** |
| `subs-en.vtt` / `subs-zh.vtt` | 软字幕双轨（另附 `.srt` 备份） |
| `slides.pdf` | 12 页幻灯片 |
| `slides/01.png` … `12.png` | 单页图 |
| `transcript.md` | 完整口播稿（12 页 73 句） |
| `quiz.json` | 8 道自测题（中英双语，含解析） |
| `poster.png` | 视频封面 |

## 怎么用

**在线看**：部署到 GitHub Pages 后直接打开仓库地址。

**本地看**：`video.mp4` 要能拖进度条，所以需要一个支持 Range 的静态服务：

```bash
python -m RangeHTTPServer -b 127.0.0.1 8080
# 打开 http://127.0.0.1:8080/
```

（用 `python -m http.server` 也行，但拖动视频可能不顺畅。）

## 实验（L2 + L3）

- 自由摆放：点芯片选中 → 点格子落位；非法操作**不拦**，reason 行会说明错在哪
- 实时指标：moduleArea / outlineArea / deadspace / density / legal + reason / bbox
- 三级提示、撤销、重置、标准答案对照（仅参考，不给「独立完成」徽章）
- 挑战 1：把 D 钉死在原点，仍然摆出合法布局
- 挑战 2：把外接矩形压到 24 以内（只浪费 1 格）

## 数字出处

全部实测自课程平台源码，不是抄来的：

- `platform/assets/floorplanning-core.js` —— 外框、模块、两组 golden、合法性判定
- `platform/tools/soft-module-sizing/soft-module-sizing.js` —— 10 张挑战卡
- 最紧外接矩形 24 与「D 钉死仍可行」由穷举验证

---

课程模块：`module03-03-soft-module-sizing`（learn_floorplanning）

## 仓库结构

```
index.html            ← 课程页（GitHub Pages 首页，打开这个）
video.mp4             7:00，1920×1080，无烧录字幕
poster.png            视频封面
subs-en|zh.vtt/.srt   软字幕双轨
slides.pdf            12 页幻灯片
slides/01..12.png     单页图（页面图集用）
transcript.md         完整口播稿
quiz.json             8 道自测题（中英双语）
skill/                制作这套内容的 skill，不属于课程页
  └── course-lesson-pack/{SKILL.md, reference.md}
```

> 根目录不留散图：幻灯片只在 `slides/` 里放一份。
