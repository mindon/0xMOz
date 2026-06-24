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

本項目是使用 <https://mindon.dev/biu/> 工具編譯的結果。

可以安裝 **biu** 之后運行 ```biu --serve``` 提供網頁服務，其他任何支持靜態html服務的工具也都可以。

然後訪問以下網址：
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
├─ present.5d6s8xrx.js     核心运行时
└─ tour.html               使用指引入口
```

## 🧩 核心约定

### `index.html`

```html
<!DOCTYPE html>
<html lang="zh_CN">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>零末之翎（∅M〇ᶻ）</title>
    <script type="importmap">{
      "imports":{
        "@lit/reactive-element/":"https://cdn.jsdelivr.net/npm/@lit/reactive-element@2.1.1/"
      }
    }</script>
    <link href="./assets/present.css" rel="stylesheet">
    <script src="./present.5d6s8xrx.js"></script>
  </head>
  <body>
    <div class="scroll-snap">
<slide topic="封面" data-src="./slides/about.html"></slide>
<slide topic="更多" data-src="./slides/more.html" data-lazy="more"></slide>
    </div>
    <!-- scroll-snap -->
    <div id="snap-points"></div>
  </body>
</html>
```

### slide 内容页骨架

```html
<!doctype html>
<html>
  <head>
    <script type="importmap">{ "imports": { /* ... */ } }</script>
    <link href="../assets/present.css" rel="stylesheet">
    <script src="../present.5d6s8xrx.js"></script>
  </head>
  <body>
    <slide topic="..." class="slide-center pop" data-pop="...">
        <style>/* slide body css styles */</style>
        <div>
            <!-- 内容 -->
        </div>
    </slide>
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
