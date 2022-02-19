# uniapp插件开发

## 概述

`uniapp` 中有两种页面类型：`vue` 和 `nvue`。
 - `vue` 页面是基于 `webview` 和客户端原生混合渲染机制实现页面布局，即页面元素部分是html、部分是原生。原生部分只能是官方提供的一些基础组件（如 `video`、`cover-view`），详情参见 [原生组件说明](https://uniapp.dcloud.io/component/native-component)。
 - `nvue` 是纯原生渲染，即所有的页面元素都是原生层实现，详情参见 [nvue介绍](https://uniapp.dcloud.io/nvue-outline)。

 目前 `uniapp` 提供了两种原生插件类型：`module` 和 `component`。
 - `module` 类型插件只扩展api能力，不提供嵌入视图层的功能。例如，在页面中需要调用原生 `toast`，通过插件实现了调用此功能的能力，在页面中这样调用：
    ```javascript
        const PluginName = uni.requireNativePlugin(PluginName);
        PluginName.toast('success');
    ```
- `component` 类型插提供嵌入视图的能力，使用方式和 `vuejs` 的 `component` 一样，需要在模版中作为标签使用，例如：
    ```html
        <!-- 此处不用和 `module` 类型组件一样需要 `requireNativePlugin`先引入，直接使用就可以了 -->
        <PluginComponent></PluginComponent>
    ```

`vue` 页面中只能使用 `module` 类型的插件，不能使用 `component` 类型的插件（因为混合渲染的机制，webview 层和原生层混排有很大的局限性）。`nvue` 页面中两种类型的插件都可以使用。

## 准备工作

技能储备：
- 前端方面，有过 `vue` 开发经验，阅读过 `uniapp` 官方开发文档，能够构建出一个可在移动设备（`andorid` 或 `ios`）上正常运行的安装包，就可以进行后续的插件开发和调试。
- 基本的 `android` 开发经验。开发语言为 `java`，插件开发暂时不支持 `kotlin`；`ide` 使用 `android studio`。我这里通过 **《java核心技术卷1（第10版）》** 和 **《第一行代码：Android（第2版）》** 来学习 `android` 开发基础。
- 基本的 `ios` 开发经验。开发语言 `objective-c` 或 `swift`，官方更新日志中说支持 `swift`，具体还没有实践过；`ide` 使用 `xcode`（槽点：xcode非常难用，尤其是用过vscode或jetbrains系列的ide，不过也没有其它选择）。我这里选择了 **《Objective-c 2.0 程序设计》** 和 **《精通IOS开发（第8版）》** 两本书来学习。

物料准备：
- `android` 端：包名（形如 `com.dykt.demo`）; 打签名包需要用到 `keystore文件`、`keystore password`、`key alias`、`key password`，去 [uni开发者后台](https://dev.dcloud.net.cn) 申请。
- `ios` 端：`Certificates`、`Identifiers`、`Profiles`，去 [苹果开发者后台](https://developer.apple.com/account/resources/certificates/list) 申请。
- 双端都需要：`appKey`，uni开发者后台申请。

## 如何解决问题

官方已经给出了详细的 [教程](https://nativesupport.dcloud.net.cn/NativePlugin/README)，最好先整体过一遍，然后按照文档的步骤进行，一步都不要少或者配错。官方教程中也列出了一些注意事项和常见问题，并给出了解决方案，一定不要忽略。

开发插件的过程中遇到问题，可以按照以下几种途径定位并解决：
- 错误日志
- 文档
- 社区
- 搜索引擎
- 根据经验推断，并逐一尝试
- 回退到上一个可运行的状态重新来过

## 问题归纳

### android 端

`android` 端问题大都集中在包依赖、包版本、编译和打包这几部分。出错基本都有详细的日志，日志可阅读性也比较强，可以很容易定位问题并找到解决方案，而且大部分是 `android` 原生问题，在社区或搜索引擎都能找到答案。

### ios 端

相比 `android` 端，`ios` 端日志或抛错则过于模糊，对于新手来说不容易定位问题，可能需要精通ios才能完全驾驭。

以下列出了几个我遇到的问题和解决方案：
* 插件在 M1 版本的 mac 上启动模拟器抛错： `building for iOS Simulator, but linking in an object file built for iOS, for architecture 'arm64'`。
  * 修改打包配置，`根目录` -> `targets` -> `HBuilder` -> `build settings` -> `Architectures` -> `Excluded Architectures` -> `Debug` 下添加 `Any IOS Simulator` 配置项，值为 `arm64` 。所有 `project` 都应该添加此配置，不然在 M1 版本的 macbook 上模拟器运行时该 project 不会被打包。
* 启动 app 后提示：**未配置appkey或配置错误**。
  * `HBuilder-Hello` -> `control.xml` 中的 `appid` 为 `uni` 项目中的 `manifest.json` 中的 `appid`。
  * `HBuilder-Hello` -> `HBuilder-uniPlugin-info.plist` （**uni官方文档中写的是 `info.plist` 😱** ） 文件中的 `dcloud_appkey` 值修改为 `uni` 开发者后台中申请的 `ios` `appkey` ，参见：[申请appkey](https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey)。
  * `根目录` -> `targets` -> `HBuilder` -> `Signing & Capabilities` 面板中配置正确的 `Bundle identifier` 和 `Provisioning Profile` （在苹果开发者后台中申请）。
* 打自定义基座时抛错 `[TXCStreamUploader getDNSServers] in TXLiteAVSDK_Player(TXCStreamUploader.o)` 。
  * 插件包 `package.json` -> `ios.frameworks` 配置项中添加 `libresolv.9.tbd` 系统库依赖。

## 案例

### 需求
在 uniapp 中使用 [腾讯云点播超级播放器](https://cloud.tencent.com/document/product/266/46217) 播放腾讯云视频，并提供功能配置项和 api 供 app 层调用。

### 插件能力
- 传入视频资源地址或腾讯云视频id播放对应的视频
- 支持传入视频标题
- 支持传入视频封面
- 支持视频加密播放
- 控制是否自动播放
- 支持倍速选项定制化
- 视频全屏状态改变通知
- 播放进度变化通知
- 播放动作通知
- 暂停动作通知
- 播放完成通知
- 移动到

### 


