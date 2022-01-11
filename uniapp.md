# uniapp

## 原生插件踩坑笔记

### ios

- 插件在 M1 版本的 mac 上启动模拟器抛错： `building for iOS Simulator, but linking in an object file built for iOS, for architecture 'arm64'`。
    * 修改打包配置，`根目录` -> `targets` -> `HBuilder` -> `build settings` -> `Architectures` -> `Excluded Architectures` -> `Debug` 下添加 `Any IOS Simulator` 配置项，值为 `arm64` 。

- 启动 app 后提示：**未配置appkey或配置错误**。
    * `HBuilder-Hello` -> `control.xml` 中的 `appid` 为 `uni` 项目中的 `manifest.json` 中的 `appid`。
    * `HBuilder-Hello` -> `HBuilder-uniPlugin-info.plist` （**uni官方文档中写的是 `info.plist` 😱😓**） 文件中的 `dcloud_appkey` 值修改为 `uni` 开发者后台中申请的 `ios` `appkey` ，参见：[申请appkey](https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey)。