# Simulation

一个单文件 WebGL2 交互背景效果。

它不是粒子系统，而是一个固定网格形变场。页面用 `GL_POINTS` 渲染静态 lattice/grid，鼠标经过时通过平滑跟随、世界坐标噪声、局部密度波带和剪切形变，形成类似流体表面被挤压、呼吸、扩散的视觉效果。

## 效果特点

- 单文件实现：只需要 `index.html`
- 无外部依赖：不需要 npm install
- WebGL2 渲染
- 固定网格背景，不是随机粒子运动
- 鼠标交互带有 0.5 秒平滑延迟
- 不规则呼吸波带，避免标准圆形扩散
- 背景区域保持轻微自主流动

## 拉下来后怎么用

从仓库复制项目：

```bash
git clone https://github.com/cuser-it/Simulation.git
cd Simulation
```

直接本地启动：

```bash
python3 -m http.server 8000
```

然后浏览器打开：

```txt
http://127.0.0.1:8000/
```

如果只是快速预览，也可以直接双击打开 `index.html`。

## 放到别的项目里当背景

最简单的方式是把 `index.html` 放到你的项目静态目录里，例如：

```txt
public/lattice-background.html
```

然后用 `iframe` 引入：

```html
<iframe class="webgl-bg" src="/lattice-background.html"></iframe>

<main class="app-content">
  <!-- Your page content -->
</main>
```

配套 CSS：

```css
.webgl-bg {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  border: 0;
  z-index: 0;
}

.app-content {
  position: relative;
  z-index: 1;
}
```

如果需要鼠标交互，请不要给 `.webgl-bg` 设置 `pointer-events: none`。

## 调整常用参数

在 `index.html` 顶部脚本里可以调整：

```js
const REST_SPACING_PX = 25;
const BASE_POINT_SIZE = 1.15;
const LIFT_POINT_SIZE = 4.6;
const MOUSE_FOLLOW_SECONDS = 0.5;
```

- `REST_SPACING_PX`：基础网格间距
- `BASE_POINT_SIZE`：平静区域点大小
- `LIFT_POINT_SIZE`：交互区域点大小
- `MOUSE_FOLLOW_SECONDS`：鼠标跟随延迟时间

## 文件说明

```txt
index.html   WebGL2 背景完整实现
README.md    项目说明和使用方法
```
