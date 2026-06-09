# ∅M〇z Present

一个轻量、可独立分发的演示文稿（Slides）框架。

每一页 slide 都是一份独立的 HTML 文件 —— 既能被入口页 `index.html` 串成完整 Present，也能单独打开访问。原生 ES Modules + importmap。

## ✨ 特性

- **Slide 即文件**：`slides/*.html` 每页一个文件，单独打开即为单页演示
- **Arrow Popover**：`class="pop"` + `data-pop` 一键挂载箭头气泡，自动 east/west/north/south 定位
- **importmap 合并**：入口与各 slide 的 importmap 在加载时自动合并
- **lazy 懒加载**：`data-lazy="key"` × `lazies.slide(key, fn)` 按需加载脚本/资源
- **离/在线感知**：`web-or-not` 属性切换在线/离线分支
- **小工具 API**：`window._0xMOz` 提供 `q$ / q$$ / lazy / lazies`

## 📖 使用指引

完整使用指引：

```
http://localhost:3000/tour.html
```

涵盖：
1. 框架简介与特性
2. 如何编写 `index.html`
3. 如何编写 slide 内容页（importmap、`data-lazy`、`lazies.slide`、`window._0moz0_`）
4. 如何配置 Arrow Popover

## 📂 目录结构

```
src/
├─ assets/                 静态资源（CSS / 字体 / SVG）
├─ slides/                 各演示页
│  └─ tour/                指引子页（00-cover ~ 04-popover）
├─ present.n8e91kk6.js     核心运行时
└─ tour.html               使用指引入口
```

## 🧩 核心约定

### `index.html`

```html
<script src="./present.n8e91kk6.js"></script>
<slide topic="封面" data-src="./slides/about.html"></slide>
<slide topic="更多" data-src="./slides/more.html"></slide>
```

### slide 内容页骨架

```html
<!doctype html>
<html>
  <head>
    <script type="importmap">{ "imports": { /* ... */ } }</script>
    <script src="../present.n8e91kk6.js"></script>
  </head>
  <body>
    <slide topic="slide-center pop" data-pop="#tip"></slide>
    <div id="tip" class="arrow" popover>...</div>
  </body>
</html>
```

### Arrow Popover

- 触发：宿主元素加 `class="pop"`，`data-pop="#popoverId"`
- 锚点：`<div id="popoverId" class="arrow" popover>...</div>`
- 自动定位：`east` / `west` / `north` / `south`，可用 CSS 变量 `--pop-x / --pop-y / --pop-alpha` 微调

## 📜 License

MIT
