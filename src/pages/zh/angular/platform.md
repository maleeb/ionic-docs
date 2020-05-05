---
previousText: '配置'
previousUrl: '/docs/angular/config'
nextText: '测试'
nextUrl: '/docs/angular/testing'
contributors:
  - liamdebeasi
---


# 设备平台

平台服务能用于获取你当前的设备信息， 你可以通过`platforms`方法获取到所支持的所有平台。包括是否在平板上查看，如果是在移动设备浏览器上，还能获取到确切的平台（iOS、Android等）。 你还能获取到设备的方向，如果语言书写方向是从右到左也能获取到，以及其他更多的信息。 利用这些信息，你可以让你的应用完全适配所有设备。

## 用法

```typescript
import { Platform } from '@ionic/angular';

@Component({...})
export class MyPage {
  constructor(public platform: Platform) {

  }
}
```

## 方法

### `is(platformName: Platforms) => boolean`

根据用户所使用的平台，`is(platformName)`会返回true或者false。 请注意，同一个应用可以为多个平台的名称都返回true。 举个例子，当一个应用运行在iPad的时候，`mobile`, `ios`, `ipad`, and `tablet`都会返回true。 此外，如果应用是运行在Cordova的话，`cordova`也会返回true。

#### 参数

| 名称             | 类型          | 描述                                                                                                                |
| -------------- | ----------- | ----------------------------------------------------------------------------------------------------------------- |
| `platformName` | `Platforms` | 平台名称， 可选项有android, capacitor, cordova, desktop, electron, hybrid, ios, ipad, iphone, mobile, phablet, pwa, tablet |

#### Platforms

以下表格列举了`Platforms`可选项以及对应描述。

| 平台名称      | 描述                     |
| --------- | ---------------------- |
| android   | 设备运行在Android           |
| capacitor | 设备运行在Capacitor         |
| cordova   | 设备运行在Cordova           |
| desktop   | 设备运行在桌面端               |
| electron  | 设备运行在Electron          |
| hybrid    | 设备运行在Capacitor或Cordova |
| ios       | 设备运行在iOS               |
| ipad      | iPad设备                 |
| iphone    | iPhone设备               |
| mobile    | 移动设备                   |
| phablet   | 平板手机                   |
| pwa       | 渐进式应用                  |
| tablet    | 平板电脑                   |

### `platforms() => string[]`

根据你当前的设备，`platforms`会返回多个值。 每个都是平台不同层面的值。 例如说，在一部iPhone上，会返回`mobile`, `ios`和`iphone`。

### `ready() => Promise<string>`

当平台准备就绪并且原生功能可以被调用的时候，会返回一个promise。 如果应用是运行在web浏览器的时候，那么当DOM准备就绪的时候，promise就会解析。 当应用运行在例如Cordova这样的引擎的时候，promise会在Cordova触发`deviceready`事件的时候解析。 解析的结果是`readySource`，代表正在使用的平台。

例如，当Cordova准备就绪时，解析出来的结果是`cordova`， 默认值是`dom`。 如果应用某些逻辑需要根据平台差异而不同，`readySource`是有作用的。 For example, only Capacitor and Cordova can execute the status bar plugin, so the web should not run status bar plugin logic.

### `isRTL() => boolean`

Returns if this app is using right-to-left language direction or not. We recommend the app's `index.html` file already has the correct `dir` attribute value set, such as `<html dir="ltr">` or `<html dir="rtl">`. [W3C: Structural markup and right-to-left text in HTML](http://www.w3.org/International/questions/qa-html-dir)

### `isLandscape() => boolean`

Returns `true` if the app is in landscape mode.

### `isPortrait() => boolean`

Returns `true` if the app is in portrait mode.

### `width() => number`

Gets the width of the platform's viewport using `window.innerWidth`.

### `height() => number`

Gets the height of the platform's viewport using `window.innerHeight`.

### `url() => string`

Get the current url.

### `testUserAgent(expression: string) => boolean`

Returns `true` if the expression is included in the user agent string.

### Parameters
| Name       | Type   | Description                           |
| ---------- | ------ | ------------------------------------- |
| expression | string | The string to check in the user agent |

## Events

### `pause`

The `pause` event emits when the native platform puts the application into the background, typically when the user switches to a different application. This event emits when a Cordova/Capacitor app is put into the background but doesn't fire in a standard web browser.

#### Usage

```typescript
this.platform.pause.subscribe(async () => {
  alert('Pause event detected');
});
```

### `resize`

The `resize` event emits when the browser window has changed dimensions. This could be from a browser window being physically resized, or from a device changing orientation.

#### Usage

```typescript
this.platform.resize.subscribe(async () => {
  alert('Resize event detected');
});
```

### `resume`

The `resume` event fires when the native platform pulls the application out from the background. This event emits when a Cordova/Capacitor app comes out from the background but doesn't fire in a standard web browser.

#### Usage

```typescript
this.platform.resume.subscribe(async () => {
  alert('Resume event detected');
});
```