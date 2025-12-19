# 🧮 Math Enigma | Function Synthesis Engine

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Tech](https://img.shields.io/badge/HTML5-KaTeX-green)
![Style](https://img.shields.io/badge/Style-Minimalist-black)

> 一个基于 Web 的极简主义数学函数生成器。它不仅能“写”出复杂的复合函数，还能“画”出优美的函数曲线。

---

## 🖼️ 预览 (Preview)

### ✨ 深色模式 (Dark Mode)
> 极客风格，发光曲线，适合夜间沉浸体验。

![Dark Mode Preview](PLACEHOLDER_FOR_DARK_MODE_IMAGE)

### ☀️ 浅色模式 (Light Mode)
> 经典教科书风格，白底黑字，清晰锐利。

![Light Mode Preview](PLACEHOLDER_FOR_LIGHT_MODE_IMAGE)

---

## 🚀 核心特性 (Features)

* **🎨 极简美学 UI**: 采用 Swiss Style 排版，配合 CSS 变量实现的平滑深/浅色主题切换。
* **📐 专业公式渲染**: 使用 **KaTeX** 的 `aligned` 环境与 `\displaystyle` 模式，呈现如教科书般完美的数学排版。
* **🧠 AST 驱动生成**: 抛弃简单的字符串拼接，采用**抽象语法树 (AST)** 构建数学逻辑，确保生成的函数结构严谨。
* **🛡️ 智能验证管线**: 内置“Matlab 级”数值验证：
    * **反常数**: 自动过滤 $f(x) = \cos(e^\pi)$ 这类伪装成函数的常数。
    * **反平凡**: 自动剔除 $f(x)=x$ 等过于简单的线性函数。
    * **定义域保护**: 自动处理 $\ln(x), \sqrt{x}$ 的定义域问题，防止绘图空白。
* **📷 自动对焦 (Auto-Scaling)**: 无论函数值域在 $[0,1]$ 还是 $[1000, 1200]$，镜头自动对焦至图像中心。
* **📋 一键复制**: 点击复制纯 LaTeX 代码，方便与 LLM (ChatGPT/Claude) 交互。
* **🥚 隐藏彩蛋**: 0.1% 概率触发神秘的 `114514` 特殊函数。

---

## 🛠️ 技术原理 (How it Works)

本项目解决了随机生成数学函数时的“方言不通”问题。

### 1. 双模 AST 节点 (Dual-Mode AST)
我们定义了 `Node` 类，每个数学节点具备三种输出形态：
* **`toExec()`**: 输出 `Math.sin(Math.PI)` —— 供 JS 引擎后台验证。
* **`toPlot()`**: 输出 `sin(PI)` —— 供 Function-plot 绘图库解析。
* **`toLatex()`**: 输出 `\sin(\pi)` —— 供 KaTeX 前端展示。

### 2. 验证与优选 (Validation Loop)
生成器会在后台进行最多 200 次的快速迭代：
1.  **构建**: 随机生成一棵深度为 2-4 的语法树。
2.  **采样**: 在 $[-5, 5]$ 区间内进行数值采样。
3.  **分析**: 计算方差、均方误差 (MSE) 和有效点数量。
4.  **决策**: 只有通过所有测试（非 NaN、非直线、非点）的函数才会被渲染。

---

## 📦 快速开始 (Quick Start)

本项目为**单文件 (Single-File)** 架构，无需 Node.js 环境或构建步骤。

1.  克隆或下载本项目。
2.  确保电脑联网（需要加载 CDN 资源）。
3.  直接双击打开 `index.html`。

### 依赖库 (CDN)
* [KaTeX](https://katex.org/) - LaTeX 渲染
* [D3.js v3](https://d3js.org/) - 数据可视化核心
* [Function Plot](https://github.com/mauriciopoppe/function-plot) - 函数绘图引擎

---

## 🤝 贡献与版权 (License)

Copyright (c) 2025 **Cichlier**.
Licensed under the MIT License.

---
