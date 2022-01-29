# uniapp

## 原生插件

### ios

#### 构建问题

* 插件在 M1 版本的 mac 上启动模拟器抛错： `building for iOS Simulator, but linking in an object file built for iOS, for architecture 'arm64'`。
  * 修改打包配置，`根目录` -> `targets` -> `HBuilder` -> `build settings` -> `Architectures` -> `Excluded Architectures` -> `Debug` 下添加 `Any IOS Simulator` 配置项，值为 `arm64` 。所有project都应该添加此配置，不然在 M1 版本的 macbook 上模拟器运行时该 project 不会被打包。
* 启动 app 后提示：**未配置appkey或配置错误**。
  * `HBuilder-Hello` -> `control.xml` 中的 `appid` 为 `uni` 项目中的 `manifest.json` 中的 `appid`。
  * `HBuilder-Hello` -> `HBuilder-uniPlugin-info.plist` （**uni官方文档中写的是 `info.plist` 😱 😓** ） 文件中的 `dcloud_appkey` 值修改为 `uni` 开发者后台中申请的 `ios` `appkey` ，参见：[申请appkey](https://nativesupport.dcloud.net.cn/AppDocs/usesdk/appkey)。
  * `根目录` -> `targets` -> `HBuilder` -> `Signing & Capabilities` 面板中配置正确的 `Bundle identifier` 和 `Provisioning Profile` （在苹果开发者后台中申请）。

#### 生命周期执行顺序

1. `onCreateComponentWithRef`
2. `loadView`
3. `viewDidLoad`

### superPlayer

```typescript
interface LitePlayerProps {
    /** 腾讯云 appId */
    appId: number
    /** 视频标题 */
    title?: string
    /** 
     * 直接使用URL播放
     * 支持 RTMP、FLV、MP4、HLS 封装格式
     */
    url?: string
    /**
     * 腾讯云点播 File ID 播放参数
     */
    videoId?: {
        /** 腾讯云视频fileId */
        fileId: string
        /** v4 开启防盗链必填 */
        pSign: string
        /** HLS EXT-X-KEY 加密key */
        overlayKey?: string
        /** HLS EXT-X-KEY 加密Iv */
        overlayIv?: string
    }
    /** 是否自动播放 */
    autoPlay?: boolean
    /** 倍速选项 */
    speeds?: number[]
    /** 视频封面 */
    poster?: string
    /**.全屏状态改变 */
    fullscreenchange?: (event: {
        detail: {
            active: boolean
        }
    }) => void
    /** 播放进度回调 */
    timeupdate?: (event: {
        detail: {
            /** 当前播放时间点（秒） */
            current: number
            /** 视频总时长（秒） */
            duration: number
        }
    }) => void
    /** 播放回调 */
    play?: () => void
    /** 暂停回调 */
    pause?: () => void
    /** 播放完成回调 */
    end?: () => void
}

interface LitePlayerMethods {
    /** 退出全屏 */
    exitFullscreen: () => void
    /**
     * 移动到指定位置播放
     * @param position 秒
     */
    seek: (position: number) => void
}
```