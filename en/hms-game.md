# Game Service(HMS Core) Quick Start

With [Game Service](https://developer.huawei.com/consumer/en/hms/huawei-game), you will have access to a range of development capabilities. You can promote your game quickly and efficiently to Huawei's vast user base by having users sign in using their HUAWEI IDs. You can also use the service to quickly implement functions such as achievements, game events, and game addiction prevention, build basic game capabilities at a low cost, and perform in-depth operations tailored to your game content and your users.

## Functions

Game Service provides the following functions for your game apps, with which you can quickly build basic game capabilities:

- Basic functions: [initialization](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-start-0000001050123475) | [update](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-update-0000001271748961) | [sign-in](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-login-0000001050121526) | [game addiction prevention](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-anti-indulgence-0000001050123479) | [floating window](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-buoy-0000001050121528)

- Extended functions: [achievements](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-achievement-0000001050123477) | [events](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-events-0000001050121530) | [leaderboards](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-leaderboards-0000001050123481) | [saved games](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-archive-0000001050121532) | [player statistics](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-playerinfo-0000001050123483) | [basic game information](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-baseinfo-0000001050121534) | [GameTurbo engine](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-gameturbo-0000001254626641)

### Version Update Description

- Latest Version：[3.x] 1.1.2_6.14.0.300
    - Remove archives, leaderboards, achievements, event reporting functions
    - Upgrade the SDK to 6.14.0.300

- [3.x] 1.0.2_6.12.0.300
    - Improve internal implementation
    - new PlayersClient. SavePlayerRole interface, abandoned submitAppPlayerInfo interface
    - Upgrade the SDK to 6.12.0.300

- [3.x] 0.0.4_6.10.0.300

    - Android Version：com.huawei.hms:game:6.10.0.300

    - Optimized code.

    - Added the support for Android 13 to the Game Service SDK.

    - Changed **targetSdkVersion 31** and **compileSdkVersion 31** to **targetSdkVersion 33** and **compileSdkVersion 33**, respectively.

## About SDK Dependencies

The SDK of the latest version can be used only on phones running HMS Core (APK) 6.10.0.300 or later.

## Enable Game Service

- Use Cocos Creator to open the project that needs to be connected to Game Service.

- Click on **Panel -> Service** in the menu bar to open the Service panel, select Game Service service to go to the service detail page, and then click on the **Enable** button in the top right to enable the service. 

    ![image.png](hms-game/image.png)

- Refer to the [Configuring App Information in AppGallery Connect](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/android-config-agc-0000001050163815) documentation to complete developer registration, app creation, enable Huawei Analysis Service parameter configuration, and enable the API.

- Fill in **App installation source** in "Params Config" of Analytics Kit service panel. For example, if the installation source of the application is Huawei AppGallery, you can fill in  **AppGallery**. The installation source name can contain up to 128 characters, including letters, digits, underscores (_), hyphens (-), and spaces. The name cannot start or end with a space if it contains only digits.

### Configs HUAWEI Config File

Most of HUAWEI Services need the `agconnect-services.json` configuration file. If there are operations such as newly opened services, please update the file in time.

- Sign in to [AppGallery Connect](https://developer.huawei.com/consumer/en/service/josp/agc/index.html) find your project from the project list and select the app on the project card.

- On the **Project Setting** page, click the configuration file **agconnect-services.json** to download it. The `agconnect-services.json` file **must be copied manually** to the `settings` directory of the project directory after downloading or updating.

    ![image.png](hms-game/image 1.png)

- For Creator v2.4.3 and above, if you want to publish to the [HUAWEI AppGallery Connect](https://docs.cocos.com/creator/manual/en/publish/publish-huawei-agc.html), you can select the downloaded or updated configuration file directly in the **Build** panel, no need to copy it manually.

    ![3b3cf4b6eb63ffd7e1b2dd763ee480b.jpg](hms-game/3b3cf4b6eb63ffd7e1b2dd763ee480b.jpg)

## Sample

Developer can get a quick taste of the Location Kit with the sample project.

- Click on the **Sample** button in the Analytics Kit service panel, clone or download, and open the project in Cocos Creator.

- After enabling the Analytics Kit service and configuring the HUAWEI configuration file as described above, you can open the **Build** panel to compile the project by clicking **Project -> Build** in the Creator editor menu bar. Cocos Creator v2.4.1 and above, you could publish to HUAWEI AppGallery Connect. Below Creator v2.4.1 could publish to the Android platform.

- Need to test on Huawei or Honor brand phones with HMS Core service installed.

- Once the Sample project is running on the phone, click the **Push** button on the homepage for testing.

    ![image.png](hms-game/image 2.png)

## Developer Guide

Most game service apis are asynchronous callbacks. Can use`huawei.hms.game.gameService.once` get single callback, or use `huawei.hms.game.gameService.on` to monitor the callback.

#### Get game service

```TypeScript
private game: typeof huawei.hms.game.gameService = (typeof huawei ===
'undefined'
? null
: huawei?.hms?.game?.gameService)!;
```

#### Game Initialization

`initGame ():void`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-start-0000001050123475)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.initGameCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.initGame();
```

#### Checking for app updates

`checkAppUpdate(forceUpdate: boolean): void;`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-update-0000001271748961)

[API文档](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-References/appupdateclient-0000001050123641#section1113567144514)

parameter description

|parameter|description|
|-|-|
|showUpdateDialog|true: The app update pop-up displays only the update button and the user must update the app.
false: The app update pop-up displays both the update and cancel buttons. The user can tap the cancel button to cancel the update.|

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.checkAppUpdateCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.checkAppUpdate(true);
```

#### Sign-in Solution for New Games

`signIn(useAuthorizationMode: boolean): void;`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-login-0000001050121526)

parameter description

|parameter|description|
|-|-|
|useAuthorizationMode|Whether to use the authorization mode to log in. Otherwise, use the silent mode to log in|

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.signInCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.signIn(true);
```

#### Signing Out of an ID

`logout(): void;`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/logout-0000001050050849)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.logoutCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.logout();
```

#### Canceling Authorization

`cancelAuthorization(): void;`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/cancelauthorization-0000001050050857)

[API文档](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-References/accountauthservice-0000001050199395#section9140325133319)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.cancelAuthorizationCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.cancelAuthorization();
```

#### Gets the current logged-in player object data.

`getCurrentPlayer ():void`

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/playersclient-0000001050121668#section1442582231216)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.getCurrentPlayerCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.getCurrentPlayer();
```

#### Sets the position for displaying the game greeting and achievement unlocking pop-ups on the screen.

`setPopupsPosition(position:number):void`

Note

- If this API is not called, the pop-ups will be displayed at the top of the screen by default.

- Position for displaying the game greeting and achievement unlocking pop-ups on the screen. Currently, only the **1** option is available, indicating that the pop-ups are displayed at the top of the screen.

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/gamesclient-0000001050123611#section66001857175314)

parameter description

|parameter|description|
|-|-|
|position|Position for displaying the game greeting and achievement unlocking pop-ups on the screen. Currently, only the 1 option is available, indicating that the pop-ups are displayed at the top of the screen.|

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.setPopupsPositionCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.setPopupsPosition(1);
```

#### Obtains the app ID of a game

`getAppId ():void`

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/gamesummary-0000001050121662#section13187143319208)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.getAppIdCallback, (result: huawei.hms.game.ApiCbResult) => {
   console.log(result);
});
this.game.getAppId();
```

#### [deprecated]Stores the information about a player in a game, such as the level and region.

`submitAppPlayerInfo (info: { area: string; rank: string; role: string; sociaty: string; }): void;`

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/playersclient-0000001050121668#section183401219425)

Example

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.submitAppPlayerInfoCallback, (result: huawei.hms.game.ApiCbResult) => {
    console.log(result);
});
this.game.submitAppPlayerInfo({
    area: "server region1", rank: "level1", role: "role1", sociaty: "Test guild information1"
});
```

#### Save the player's character information in the game, such as area uniforms, character names, etc.

`savePlayerRole (info: { serverId: string; serverName: string; roleId: string; roleName: string; }): void;`

[References](https://developer.huawei.com/consumer/cn/doc/HMSCore-References/playersclient-0000001050121668#section14448819342)

示例

```TypeScript
this.game.once(huawei.hms.game.API_EVENT_LIST.savePlayerRoleCallback, (result: huawei.hms.game.ApiCbResult) => {
    this.consolePanel.log(result);
});
this.game.savePlayerRole({
    serverId: "123", serverName: "server1", roleId: "321", roleName: "role1"
});
```

#### Show Float Window

`showFloatWindow ():void`

[G](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-buoy-0000001050121528)[uide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-buoy-0000001050121528)

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/buoyclient-0000001050123633)

Example

```TypeScript
this.game.showFloatWindow();
```

#### Hide Float Window

`hideFloatWindow ():void`

[Guide](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/game-buoy-0000001050121528)

[References](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References/buoyclient-0000001050123633)

Example

```TypeScript
this.game.hideFloatWindow();
```
