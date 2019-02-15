# babel使用

## babel是一个javascript编译器

Babel 是一个工具链，主要用于在旧的浏览器或环境中将 ECMAScript 2015+ 代码转换为向后兼容版本的 JavaScript 代码

- 转换语法
- Polyfill 实现目标环境中缺少的功能 
- 源代码转换 (codemods)
- 更多！

Babel 通过语法变换器支持最新版本的 JavaScript。

这些 plugins 允许你现在就使用新语法，而无需等待浏览器的支持。查看我们的使用指南以开始使用。


## 核心库 @babel/core
Babel 的核心功能在 @babel/core 模块。

## CLI 工具 @babel/cli
@babel/cli 是一个允许你从终端使用 babel 的工具

## Plugins & Presets
代码转换以插件的形式出现，插件是小型 JavaScript 程序，它指示 Babel 如何对代码进行转换。

如果想要转换代码中还有其他 ES2015+ 功能。我们可以使用 "preset" 来代替预先设定的一组插件，而不是逐一添加我们想要的所有插件。

这个 preset 包括支持现代 JavaScript（ES2015，ES2016 等）的所有插件。但是 presets 也可以选择。我们不从终端传入 cli 和 preset 选项，而是通过另一种传入选项的方式：配置文件。


## Polyfill
@babel/polyfill 模块包括 core-js 和自定义 regenerator runtime 来模拟完整的 ES2015+ 环境。

如果你不需要像 Array.prototype.includes 这样的实例方法，可以使用 transform runtime 插件而不是污染全局的 @babel/polyfill。

幸运的是，对于我们来说，我们使用的是 env preset，其中有一个 "useBuiltIns" 选项，当设置为 "usage" 时，实际上将应用上面提到的最后一个优化，只包括你需要的 polyfill。



我们使用 @babel/cli 从终端运行 Babel，@babel/polyfill 来实现所有新的 JavaScript 功能，env preset 只包含我们使用的功能的转换，实现我们的目标浏览器中缺少的功能。


## 配置babel

- babel.config.js
- .babelrc
- .babelrc.js
- package.json