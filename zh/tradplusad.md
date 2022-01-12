# TradPlus（聚合广告）快速入门

[TradPlus 聚合广告平台](https://www.tradplusad.com)，为开发者提供专业、便捷和高效的广告变现解决方案。集成了40+ 国内外主流广告平台，支持自动优化、Bidding、用户级数据报表、交叉推广等功能。TradPlus 提供完善的广告漏斗模型，帮助开发者透视广告变现全过程，精准优化广告变现每个环节，实现广告收益最大化。

### 版本更新说明（Cocos Creator 2.x）

- 当前版本：0.5.5_6.4.4.1_5.7.1

    -  修复构建iOS平台时，如果服务处于禁用状态会报错的问题。

- 0.5.3_6.4.4.1_5.7.1

    -  新增 TradPlus 广告聚合平台。

### 版本更新说明（Cocos Creator 3.x）

- 当前版本：2.0.8_7.0.30.1_6.6.10

    -  升级Android SDK到v7.0.30.1
    -  升级iOS SDK到v6.6.10

- 2.0.7_6.4.4.1_5.7.1

    -  修复未开启本插件服务时仍然提示与其他插件服务有冲突的问题。

- 2.0.6_6.4.4.1_5.7.1

    -  修复构建iOS平台时，如果服务处于禁用状态会报错的问题。

- 2.0.5_6.4.4.1_5.7.1

    -  新增 TradPlus 广告聚合平台。

## 一键接入 TradPlus 服务

### 开通服务

- 使用 Cocos Creator 打开需要接入 TradPlus 服务的项目工程。

- 点击菜单栏的 **面板 -> 服务**，打开 **服务** 面板，选择 **TradPlus**，进入服务详情页。然后点击右上方的 **启用** 按钮即可开通服务。详情可参考 [服务面板操作指南](./user-guide.md)。

  ![](tradplusad/tradplusad-panel.png)

- 如果您还没有 TradPlus 聚合广告平台的账号，请前往 [TradPlus](https://developer.tradplusad.com/) 进行注册，并根据[指引文档](https://docs.tradplusad.com/docs/Guide)进行相应的配置，获取服务面板所需要的 `App ID` 等参数。

* <font color="red">注1：构建时，切记填写的包名/bundle ID要和TradPlus后台创建的应用一致。</font>

* <font color="red">注2：TradPlus 聚合广告在 iOS 和 Android 平台上需要创建不同的 App ID，两者不能公用同一个 App ID。</font>

### 验证服务是否接入成功

- 完成 **TradPlus** 服务接入步骤后，我们便可以通过在脚本中添加简单的代码，来验证接入是否成功。

```ts
// 启用调试日志，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setEnableLog(true);
// 初始化SDK
tradplus.tradPlusService.initSdk();
// 启用测试模式，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setNeedTestDevice(true);
```

- 工程运行到手机后，Android平台请在 Android Studio 中查看日志，过滤日志关键字 "TradPlusLog" ，iOS平台请在 Xcode 中查看日志，过滤日志关键字 "TradPlus" 。

## Sample 工程

开发者可以通过 Sample 工程快速体验 TradPlus 服务。

- 点击 TradPlus 服务面板中的 **Sample 工程** 按钮，克隆或下载 TradPlus Sample 工程，并在 Cocos Creator 中打开。

- 参照上文开通 TradPlus 并配置相应参数后，可通过 Creator 编辑器菜单栏的 **项目 -> 构建发布**， 打开 **构建发布** 面板来构建编译工程。

- Sample 工程运行到手机后，即可进入功能界面进行测试。

  ![](tradplusad/tradplusad-sample.png)

## 开发指南

完整的代码请参考 Sample 工程。

### 初始化SDK

首先，我们需要初始化SDK，初始化后才能调用广告相关的API。

初始化SDK代码如下：

```ts
// 初始化SDK，我们不需要传递App ID作为参数，它会自动使用服务面板填写的App ID
tradplus.tradPlusService.initSdk();
```

开发过程中，如果需要查看调试日志，可以调用 `setEnableLog` ，如果需要开启测试模式，可以调用 `setNeedTestDevice` 。

故开发时，我们初始化代码一般如下：

```ts
// 启用调试日志，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setEnableLog(true);
// 初始化SDK
tradplus.tradPlusService.initSdk();
// 启用测试模式，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setNeedTestDevice(true);
```

**需要特别注意的是， `setEnableLog` 和 `setNeedTestDevice` 仅测试时使用，上线前请记得注释掉。**

### 横幅广告

横幅广告使用步骤如下：

1. 传入广告位ID给 `getBanner` 以获取该广告位ID对应的横幅广告对象。

2. 调用 `banner.setAdListener` 设置该横幅广告对象的事件监听器，以在该横幅广告相关事件发生时采取相应的动作。

3. 调用 `banner.loadAd` 加载并显示横幅广告。

完整代码如下：

```ts
const adUnitId = '您的横幅广告位ID';

const banner = tradplus.tradPlusService.getBanner(adUnitId);

banner.setAdListener({
  onAdLoaded: (adSourceName) => {
    // 在广告加载完成的时候触发，adSourceName为广告源名称
  },

  onAdClicked: () => {
    // 在广告被点击的时候触发
  },

  onAdLoadFailed: (adError) => {
    // 在广告加载失败的时候触发，adError包含了错误信息
  },

  onAdImpression: () => {
    // 在广告被展示的时候触发
  },

  onAdShowFailed: (adError) => {
    // 在广告显示失败的时候触发
    // 注：这个回调仅在Android平台下会触发
  },

  onAdClosed: () => {
    // 在广告被关闭后触发
    // 注：这个回调仅在Android平台下会触发
  },

  onBannerRefreshed: () => {
    // 在广告自动刷新时触发
    // 注：这个回调仅在Android平台下会触发
  },
});

// 在屏幕上方加载并显示横幅广告
this.banner.loadAd('top');
```

### 激励视频、插屏广告

激励视频和插屏广告的使用和横屏广告类似，请参考 Sample 工程及 [TradPlus - API 文档](https://service.cocos.com/document/api/modules/tradplus.html)。

### 隐私规范

隐私规范涉及 GDPR、CCPA、COPPA，可以参考 TradPlus 官方文档：[隐私规范（Android）](https://docs.tradplusad.com/docs/tradplussdk_android_doc_v6/ios_sdk_privacy) 或者 [隐私规范（iOS）](https://docs.tradplusad.com/docs/integration_ios/ios_sdk_privacy/android_sdk_gdpr)。

#### GDPR

如果您的应用需要发到欧盟区域，那需要特别注意下 GDPR 。

为了设置GDPR，我们需要如下步骤：

1. 在初始化SDK前设置GDPR监听器。

2. 在GDPR监听器的onSuccess中，判断GDPR是否适用，如果适用，调用API显示GDPR对话框，让用户自己选择GDPR等级。

完整初始化代码如下：

```ts
// 启用调试日志，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setEnableLog(true);

// 设置GDPR监听器，需要在初始化SDK之前调用
tradplus.privacy.setGDPRListener({
  onSuccess: () => {
    // 已知国家
    if (tradplus.privacy.isGDPRApplicable()) {
      // GDPR适用，此时调用showGDPR显示GDPR对话框，让用户自己选择GDPR等级
      cc.log('GDPR is applicable');
      tradplus.privacy.showUploadDataNotifyDialog();
    } else {
      cc.log('GDPR is not applicable');
    }
  },
  onFailed: () => {
    // 未知国家，让用户自己选择GDPR等级
    cc.log(
      'Unknown country, let the user choose the GDPR level'
    );
    tradplus.privacy.showUploadDataNotifyDialog();
  },
});

// 初始化SDK
tradplus.tradPlusService.initSdk();

// 启用测试模式，仅测试时使用，上线前请注释掉
tradplus.tradPlusService.setNeedTestDevice(true);
```

#### CCPA

如果需要设置CCPA，请调用API `setCCPADoNotSell` ，false 表示加州用户均不上报数据， true 表示接收上报数据。

注意： `setCCPADoNotSell` 需要在初始化SDK之前调用。

```ts
tradplus.privacy.setCCPADoNotSell(false /* 或者 true */);
```

#### COPPA

如果需要设置COPPA，请调用API `setCOPPAIsAgeRestrictedUser` ，false 表明不是儿童， true 表明是儿童。

注意： `setCOPPAIsAgeRestrictedUser` 需要在初始化SDK之前调用。

```ts
tradplus.privacy.setCOPPAIsAgeRestrictedUser(true /* 或者 false */);
```

## API 文档

详细 API 的说明，请参考 [TradPlus - API 文档](https://service.cocos.com/document/api/modules/tradplus.html)。

## 注意事项

### iOS构建

当前，由于我们使用 Cocoapods 来管理 iOS 依赖，如果您构建的目标平台是 iOS ，则在构建完成后，不要直接点击编译，您需要用Xcode打开生成的Xcode工作空间（以.xcworkspace结尾，不要打开.xcodeproj结尾的项目），在Xcode中继续编译本项目，否则编译会失败。

针对Cocos Creator 2.x，生成的 Xcode 工作空间的路径一般是 {您的项目所在目录}/build/jsb-link/frameworks/runtime-src/proj.ios_mac/{游戏名称}.xcworkspace。

针对Cocos Creator 3.x，生成的 Xcode 工作空间的路径一般是 {您的项目所在目录}/build/{构建任务名}/proj/{游戏名称}.xcworkspace。

### iOS 14+

Apple将在2021年实施一个新的规则，在iOS 14+上通过弹窗来获取IDFA，使用IDFA需要征得用户的同意。

如果您需要适配iOS 14+，请在面板中勾选 “适配iOS 14+” ，然后填写相应的参数，注意：这需要您把Xcode版本升级到一个>=12的版本。
