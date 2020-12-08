## 介绍

[vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/)是一个后台前端解决方案，基于 vue 和 element-ui。希望通过学习该框架学习前端知识。

## 目录结构

### 根目录

**package.json** && package-lock.json：

**vue.config.js**：

postcss.config.js：postcss是一个用 JavaScript 工具和插件转换 CSS 代码的工具。配置文件。

jsconfig.json：表示该目录是JavaScript项目的根目录。jsconfig.json文件指定根文件和JavaScript语言服务提供的功能选项。

jest.config.js：Jest 是一个 JavaScript 测试框架。配置文件。

babel.config.json：JavaScript 编译器。

.travis.yml：自动化 CI 配置。Travis CI 提供的是持续集成服务（Continuous Integration，简称 CI）。

.eslintrc.js && .eslintignore：ESLint是一个用来识别 ECMAScript 并且按照规则给出报告的代码检测工具，使用它可以避免低级错误和统一代码的风格。

.editorconfig：可以向项目或基本代码添加 EditorConfig 文件，强制对使用该基本代码的所有人实施一致的编码样式。 EditorConfig 设置优先于全局 Visual Studio 文本编辑器设置。

.env.XXX：环境变量配置

### tests

测试文件

### mock

项目 mock 模拟数据

### build

构建脚本

### public

静态资源

index.html：

favicon.ico：

### src

源代码，基本开发的东西都在这个目录下。

/api：api 向后端发起请求

/asserts：开发时使用的静态资源。？？？为什么不丢到static下，安全问题吗

/components：全局公用组件

/icons：项目所有 svg icons // 其实也相当于静态文件吧，用的 svg 引用，不太了解。

/layout：

/router：

/store：

/styles：

/utils：

/vendor：

/views：

App.vue：vue 基础组件，所有后续 vue 控件都往这个基础组件里挂。

main.js：入口文件，将同目录下 APP.vue 中定义的基础组件挂到静态文件 index.html 中的 app 节点下，并在此之前做一些预处理，比如加载路由和权限。

permission.js：权限管理





