# switch-ui

一个轻量、零依赖、无障碍友好的开关（Switch / Toggle）组件库，开箱即用的 HTML/CSS/JS 实现。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 特性

- **零依赖**：纯原生 HTML / CSS / JavaScript，无框架、无构建步骤
- **无障碍**：`role="switch"` + `aria-checked`，支持 Space / Enter 键操作
- **可定制**：通过 CSS 变量调整尺寸、颜色和动画时长
- **受控与非受控**：既可自动切换，也可完全交由业务侧决定状态
- **体积小**：未压缩约 3KB

## 快速开始

### 1. 引入文件

```html
<link rel="stylesheet" href="switch.css">
<script src="switch.js"></script>
```

### 2. 编写结构

```html
<button class="sw" role="switch" aria-checked="false" aria-label="开启通知">
  <span class="sw-thumb"></span>
</button>
```

### 3. 初始化

```html
<script>
  // 自动绑定页面上所有 .sw 元素
  SwitchUI.init();
</script>
```

## 用法

### 非受控模式

```js
const sw = SwitchUI.create({
  el: '#my-switch',
  checked: true,
  onChange(state) {
    console.log('当前状态：', state);
  }
});
```

### 受控模式

```js
const sw = SwitchUI.create({
  el: '#controlled',
  controlled: true, // 点击时不自动改变，由业务决定
  onChange(state) {
    fetch('/api/setting', {
      method: 'POST',
      body: JSON.stringify({ on: state })
    }).then(() => sw.set(state));
  }
});
```

## API

| 方法 | 说明 |
| --- | --- |
| `SwitchUI.init(root?)` | 初始化 root 内所有 `.sw` 元素 |
| `SwitchUI.create(options)` | 创建实例并返回实例对象 |

实例方法：

| 方法 | 说明 |
| --- | --- |
| `on()` | 打开 |
| `off()` | 关闭 |
| `toggle()` | 切换 |
| `set(state)` | 设置指定状态 |
| `get()` | 读取当前状态 |
| `destroy()` | 解绑事件 |

### 选项

| 选项 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `el` | Element \| string | - | 目标元素或选择器 |
| `checked` | boolean | `false` | 初始状态 |
| `controlled` | boolean | `false` | 是否受控模式 |
| `disabled` | boolean | `false` | 是否禁用 |
| `onChange` | function | - | 状态变化回调，参数为最新状态 |

## 主题定制

```css
.sw {
  --sw-width: 48px;
  --sw-height: 26px;
  --sw-bg: #d0d5dd;
  --sw-bg-on: #16a34a;
  --sw-thumb: #ffffff;
  --sw-duration: 200ms;
}
```

## 事件

状态变化时会在元素上派发可冒泡的 `switch:change` 事件：

```js
document.querySelector('#my-switch').addEventListener('switch:change', (e) => {
  console.log(e.detail.checked);
});
```

## 浏览器支持

Chrome / Edge / Firefox / Safari 最近两个大版本，以及 iOS Safari 15+。

## 本地预览

直接用浏览器打开 `index.html` 即可查看示例，无需安装任何依赖。

## 贡献

欢迎提交 Issue 和 Pull Request。提交前请确保示例页面在主流浏览器中表现一致。

## 许可证

[MIT](LICENSE)
