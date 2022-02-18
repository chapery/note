# uniapp插件开发

## 使用场景

uniapp 中有两种页面类型：`vue` 和 `nvue`。

 - `vue` 页面是基于 `webview` 和客户端原生混合渲染机制实现页面布局，原生部分只能是官方提供的一些基础组件（如 `video`、`cover-view`），详情参见[原生组件说明](https://uniapp.dcloud.io/component/native-component)。
 - `nvue` 是纯原生渲染，详情参见 [nvue介绍](https://uniapp.dcloud.io/nvue-outline)。

 目前 `uniapp` 提供了两种原生插件类型：`module` 和 `component`。
 
 - `module` 类型插件只扩展api能力，不提供嵌入视图层的功能。例如，在页面中需要


