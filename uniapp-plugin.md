# uniapp插件开发

## 概述

`uniapp` 中有两种页面类型：`vue` 和 `nvue`。

 - `vue` 页面是基于 `webview` 和客户端原生混合渲染机制实现页面布局，原生部分只能是官方提供的一些基础组件（如 `video`、`cover-view`），详情参见[原生组件说明](https://uniapp.dcloud.io/component/native-component)。
 - `nvue` 是纯原生渲染，详情参见 [nvue介绍](https://uniapp.dcloud.io/nvue-outline)。

 目前 `uniapp` 提供了两种原生插件类型：`module` 和 `component`。
 
 - `module` 类型插件只扩展api能力，不提供嵌入视图层的功能。例如，在页面中需要调用原生 `toast`，通过插件实现了调用此功能的能力，在页面中：
    ```javascript
        const PluginName = uni.requireNativePlugin(PluginName);
        PluginName.toast('success');
    ```
- `component` 类型插提供嵌入视图的能力，使用方式和 `vuejs` 的 `component` 一样，需要在模版中作为标签使用，例如：
    ```html
        <!-- 此处不用和 `module` 类型组件一样需要 `requireNativePlugin`先引入，直接使用就可以了 -->
        <PluginComponent></PluginComponent>
    ```

`vue` 页面中只能使用 `module` 类型的插件，不能使用 `component` 类型的插件（因为混合渲染的机制，webview层和原生层混排有很大的局限性）。`nvue` 页面中两种类型的插件都可以使用。


