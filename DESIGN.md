# 看板视觉主题说明（Deep Terminal）

本仓库的页面样式已在 2026-09-06 重设计为「深色金融终端」主题。本文件给后续维护者（人或 Agent）说明：样式在哪里、定时抓取脚本的模板要同步什么、配色对照关系。

## 文件结构

- `styles.css` —— 全部视觉样式，独立文件，抓取脚本**不会**触碰它
- `index.html` —— 由本地抓取脚本每天重新生成；其中通过 `<link rel="stylesheet" href="styles.css">` 引用样式
- `echarts.min.js` —— 图表库

## ⚠️ 抓取脚本模板必须同步的三处

抓取脚本重新生成 `index.html` 时，若仍用旧模板，新设计会被覆盖。模板需改为：

### 1. 样式引用（替换整个内嵌 `<style>...</style>` 块）

```html
<link rel="stylesheet" href="styles.css">
```

### 2. 页头结构（`<header>` 内）

```html
  <div>
    <div class="kicker">MACRO MONITOR · CN / US</div>
    <h1>宏观经济数据看板</h1>
    <div class="sub">中国 · 美国 关键宏观指标实时跟踪</div>
  </div>
  <div class="updated"><span class="live"></span>数据更新时间<br><b id="updatedAt">—</b></div>
```

`id="updatedAt"` 必须保留（JS 用它写入更新时间）。

### 3. JS 图表配色常量

| 用途 | 旧值 | 新值 |
|------|------|------|
| `ACCENT`（主色/折线） | `#4d9fff` | `#3ec6e0` |
| `GRID`（网格线/边框） | `#1e2836` | `#1a2636` |
| `MUTED`（次要文字） | `#7d8a99` | `#6b7f96` |
| `BOND_COLORS[0]` | `#4d9fff` | `#3ec6e0` |
| tooltip `backgroundColor` | `#1a2330` | `#0c1420` |
| dataZoom 滑块 `backgroundColor` | `#0f1520` | `#091019` |
| 渐变/填充 `rgba(77,159,255,.15)` | — | `rgba(62,198,224,.15)` |
| 渐变 `rgba(77,159,255,.28)` | — | `rgba(62,198,224,.22)` |
| 渐变 `rgba(77,159,255,0)` | — | `rgba(62,198,224,0)` |

`UP #f0453a` / `DOWN #2ebd6b`（红涨绿跌）保持不变。

## 设计约束（改样式时遵守）

- 深色底 `#060b13`，单一青色强调色 `#3ec6e0`，不要再引入第二强调色
- 数字、日期、英文标签用等宽字体栈：`"JetBrains Mono", "SF Mono", Consolas, monospace`
- 卡片左上角保留 2px 青色"信号刻度"（`.card::before`），悬停仅做边框点亮 + 轻微上浮
- 不要加滚动出现动画、彩色渐变边框、玻璃拟态等花哨效果

## 上线方式

```bash
git push   # commit 已打好，直接推送即可，GitHub Pages 即时生效
```
