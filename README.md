# Math Enigma | 函数海龟汤生成器

**Math Enigma** 是一个基于 Web 的极简主义数学函数生成引擎。它能随机生成结构复杂、图像优美的**复合函数**，并实时渲染其 LaTeX 公式与函数图像。

不同于普通的随机字符拼接，本项目采用**“逻辑优先”**的生成策略，确保生成的每一个函数都在实数域上有意义、非平凡（非线性/非简单的常数），并具备自动对焦的视觉呈现能力。

---

## ✨ 核心特性

* **🎨 极简主义设计 (Swiss Style)**: 深色模式，大留白，搭配发光曲线与衬线字体，提供画廊般的视觉体验。
* **🧠 AST 驱动生成 (AST-First)**: 基于抽象语法树（Abstract Syntax Tree）构建数学逻辑，而非简单的字符串拼接。这确保了逻辑的严密性。
* **🛡️ 严苛的数值验证管线**:
* **反常数检测**: 通过方差计算过滤掉  这类伪装成复杂函数的常数。
* **反恒等检测**: 自动剔除  或  等过于简单的线性函数。
* **定义域安全**: 自动处理  和  的定义域问题，防止绘图空白。


* **📷 智能自动对焦 (Auto-Scaling)**: 无论函数值域是  还是 ，视图会自动缩放并对焦到图像中心，拒绝“画出画框外”。
* **📋 一键复制 LaTeX**: 点击公式旁的图标即可复制纯 LaTeX 代码，方便与 LLM（如 ChatGPT/Claude）交互。
* **🥚 隐藏彩蛋**: 0.1% 的概率生成关于 `114514` 的特殊函数。

---

## 🛠️ 技术原理

本项目解决了随机生成数学函数时常见的“三大难题”：

### 1. 语法与逻辑分离 (AST Architecture)

我们定义了 `Node`, `Atom`, `UnaryOp`, `BinaryOp` 类。每个节点具备三种输出形态，解决了不同库之间的“方言”障碍：

* `toExec()`: 输出 `Math.sin(Math.PI)`，供 JS 引擎进行数值验证。
* `toPlot()`: 输出 `sin(PI)`，供 function-plot 库绘图。
* `toLatex()`: 输出 `\sin(\pi)`，供 KaTeX 渲染展示。

### 2. Matlab 级验证 (Validation Pipeline)

在渲染之前，生成的 AST 会被编译为可执行函数并在后台进行**数值采样**：

1. **采样**: 在  区间内选取多个关键点（包括无理数点）。
2. **存活测试**: 检查计算结果是否包含过多的 `NaN` 或 `Infinity`。
3. **方差分析**: 计算 Y 值的方差，若小于阈值，判定为“视觉常数”，强制重抽。
4. **MSE 检测**: 计算与  的均方误差，防止生成平凡解。

### 3. 双层渲染 (Dual Rendering)

* **公式渲染**: 使用 [KaTeX](https://katex.org/)，轻量且排版精美。
* **函数绘图**: 使用 [Function Plot](https://github.com/mauriciopoppe/function-plot) (基于 D3.js)，并进行了深度 CSS 定制以适配暗黑风格。

---

## 🚀 快速开始

本项目为**单文件 (Single-File)** 架构，无需 Node.js 环境或构建步骤。

1. 下载 `index.html` 文件。
2. 直接在浏览器（Chrome/Edge/Safari）中打开。
3. 点击 **GENERATE** 按钮体验。

> **注意**: 需要联网以加载 CDN 资源（KaTeX, D3, Function-plot）。

---

## 🎮 操作指南

* **Generate**: 点击生成一个新的函数。算法会尝试最多 200 次以找到一个符合“审美标准”的函数。
* **Copy Latex**: 点击公式右侧的 📋 图标，复制 LaTeX 代码。
* **Zoom/Pan**: 默认禁用交互，以保持“艺术展品”的静态美感（可在代码中修改 `disableZoom: false` 开启）。

---

## 🥚 彩蛋 (Easter Egg)

在生成逻辑的最前端，埋藏了一个极低概率的触发器：

```javascript
if (Math.random() < 0.001) {
    // ???
}

```

一旦触发，系统将无视常规数学逻辑，为你呈现一个独特的数值奇迹。

---

## 📦 依赖库 (CDN)

* [KaTeX v0.16.9](https://katex.org/) - LaTeX 渲染
* [D3.js v3](https://d3js.org/) - 数据可视化基础
* [Function Plot v1](https://github.com/mauriciopoppe/function-plot) - 函数绘图引擎

---

## 📄 License

MIT License. Feel free to use and modify.

---

**Created with ❤️ by Gemini & Cichlid.**