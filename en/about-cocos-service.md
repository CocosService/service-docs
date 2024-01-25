# Cocos Service Introduction

Cocos Creator provides a **Service** panel in the **Menu bar -> Panel**, and developers can quickly integrate services through the **Service** panel for the game.

![](index/cocos_services.jpg)

The **Service** Panel currently supports the integration of third-party services including the following:


  - [Location Kit (HMS Core)](hms-location.md)

  - [Analytics Kit (HMS Core)](hms-analytics.md)

  - [HUAWEI Account Kit（HMS Core）](hms-account.md)

  - [Push Kit（HMS Core）](hms-push.md)

  - [In-App Purchases（HMS Core）](hms-iap.md)

  - [Game Service（HMS Core）](hms-game.md)

  - [APM (AppGallery Connect)](agc-apms.md)

  - [Ads Kit（HMS Core）](hms-ads.md)
    
  - [Cloud Functions（AppGallery Connect）](agc-function.md)

  - [Remote Configuration（AppGallery Connect）](agc-remoteconfig.md)

  - [Online Multiplayer Battles (AppGallery Connect)）](hw-gobe.md)

  - [Game Multimedia (AppGallery Connect)](hw-mmsdk.md)
  
  - [Vungle ](vunglead.md)

  - [Taobao Avatar SDK](taobaoavatar.md)

## Usage

- Open the Cocos Creator, choose **Menu bar -> Panel -> Service** to open the **Service** panel. Click the ![](index/setting.jpg) button above the **Service** panel. Select **Dashboard** and go to the [Cocos Account Center](https://auth.cocos.com/#/) to register your user account.

  ![](index/console.jpg)

  Create Personal/Company games as needed after account registration is complete:

  ![](index/game.jpg)

- After the game is created, return to the Cocos Creator **Service** panel and click the ![](index/setting.jpg) button. After selecting **Set Cocos AppID**, jump to the **Set Cocos AppID** panel. Then select the game and click the **Association** button.

  ![](index/appid.jpg)

  You can create a game by clicking the **Cocos AppID is not found. Click here to create** button to jump to the Cocos Account Center.

- When the AppID setup is complete, it automatically jumps to the **Service** panel, where you can see that the game name and AppID are already displayed at the top left of the panel.

  ![](index/service.jpg)

  If you need to switch games, you can click the ![](index/setting.jpg) button again to select **Unlink**. Then go to the **Set Cocos AppID** panel again and re-select the game.

  ![](index/switch_appid.jpg)
