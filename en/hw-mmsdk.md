# Quick Start for Game Multimedia (AppGallery Connect)

The [Game Multimedia Service](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-introduction-0000001226565909) is a service launched by Huawei Game Center that quickly implements real-time voice intercom and IM chat (Instant Messaging) features in games. You only need to integrate the Game Multimedia Service SDK to provide your games with real-time voice intercom, voice-to-text, instant messaging capabilities, reduce development difficulty, and enhance the player's gaming experience.

## Main Features

| Main Features | Feature Description |
| --- | --- |
| Real-Time Voice | The real-time voice function is mainly used to achieve real-time voice intercom capabilities between different clients. With the help of the "voice room", a virtual audio space, different players can be added to the same voice room for real-time voice calling. During real-time voice, microphone status can be set, and muting and blocking functions can be implemented. The game multimedia SDK also supports range voice capabilities and 3D sound effects, simulating spatial sound effects of the real world for immersive sound effects. |
| Real-Time Signaling | The real-time signaling (Real-time Messaging, RTM) function provides a TypeScript SDK suitable for the Cocos engine and a server-side REST API. The function is based on Huawei's RTN network, supporting real-time sending and receiving of messages over the network, and providing stable, reliable, low-latency, and high-concurrency communication services. The RTM client SDK provides point-to-point message sending and receiving, channel subscription, and channel message sending and receiving, useful for real-time communication, global chat, game notification, command synchronization and other game scenarios. The RTM server-side API provides point-to-point message and channel message sending, useful for game announcements, message notifications, and other game scenarios. |
| Voice Messages | The game multimedia SDK provides voice message recording, recording file upload and download, and playback capabilities. Players can record a voice message and upload the recording file to the cloud. The file ID can be sent to other players through the IM channel, allowing them to download and play the voice message. |
| Sound Effects Playback | In game or live broadcast scenarios, it's often necessary to play short sound effects like bullet sounds or applause to enhance the sense of reality or set the scene atmosphere. The game multimedia SDK provides related interfaces for sound effect playback, useful for managing the playback of short sound effects and volume coefficients. |
| Voice to Text | The voice-to-text function can quickly recognize real-time voice and transcribe it into text content, useful for scenarios like voice input. |

### Operational Mechanism

Clients integrated with the Game Multimedia Service SDK input voice information into the Huawei Game Multimedia Server. The server receives and processes this information, subsequently outputting the voice data to all clients within the room. Simultaneously, the Game Multimedia Service SDK provides an Instant Messaging (IM) feature for message conversations between different clients. By integrating the Game Multimedia Service SDK into your game and conducting simple feature development, you can swiftly build voice chat and instant messaging capabilities for your game.

![https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20230811185002.93436547234333337127849612796014:50001231000000:2800:F2DBDC5E8A8BF9714CD86AE106AC9F9644527E6F58345A474E8A3BE4EB36E1A2.png?needInitFileName=true?needInitFileName=true](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20230811185002.93436547234333337127849612796014:50001231000000:2800:F2DBDC5E8A8BF9714CD86AE106AC9F9644527E6F58345A474E8A3BE4EB36E1A2.png?needInitFileName=true?needInitFileName=true)


## Version Update Instructions

- Current version:[3.x]1.2.0_14.0.1.300

    - Upgrade the SDK to 14.0.1.300
    - The GameMediaEngine class adds the startDetectAudioFile method, which supports risk control sending of voice message files.

- [3.x]1.1.0_1.13.1.300

    - Upgrade the SDK to 1.13.1.300

- [3.x]1.0.12_1.12.2.300

    - Improve internal implementation
    - Upgrade the SDK to 1.12.2.300
    
- Version: [3.x] 1.0.7_1.12.1.300
    - Fixed setting microphone callback error

- Version: [3.x] 1.0.6_1.12.1.300
    - Fixed an error reporting the listening channel property change callback
    - Fixed errors when updating other player positions

- Version: [3.x] 0.0.4_1.11.1.300
    - Initial release

    
## Quick Integration of Game Multimedia

### Service Activation

- You need to activate the game multimedia feature in the Huawei AGC backend, and turn on the "Voice to Text" and "IM Chat" features. (In addition to manually enabling the IM Chat feature on the AGC console, a secondary application is required, please refer to [Service Management](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-console-servicemanagement-0000001255134391)).

- Open the project that needs to integrate game multimedia with Cocos Creator.

- Click on the **Panel -> Service** in the menu bar, open the **Service** panel, select **Game Multimedia** in **HUAWEI AppGallery Connect**, enter the service detail page. Then click the **Enable** button at the top right to activate the service.

### Verify If the Service Is Successfully Activated

- After activation, if you see hwmmsdk related files in the cs-huawei folder under assets in the project, if this folder is not available, please check the log information of the editor console.

- You can refer to the Sample project, initialize, package into "Android" or "HUAWEI AppGallery Connect" platform, run on an Android phone, observe whether the callback can be initialized successfully, if it fails, please check whether the initialization parameters are correct and whether the package name is consistent with the AGC backend.

## Sample Project

Developers can quickly experience the online battle service through the Sample project.

- Click the **Sample Project** button in the analysis service panel, Clone or download HUAWEI Sample Project, and open it in Cocos Creator.

- You need to find the hwmmsdk.ts script and modify the data to the information of the application you created.

- After the Sample project runs on the phone, click the **Hwmmsdk** button on the homepage to enter the function interface for testing.

## Development Guide

All APIs of Game Multimedia are asynchronous callbacks. You can use `huawei.game.mmsdk.mmsdkService.once` to get a single callback, or use `huawei.game.mmsdk.mmsdkService.on` to listen to callbacks. You can use `huawei.game.mmsdk.mmsdkService.off` to remove callbacks.

#### Request Permissions

`requestPermissions(guideUser: boolean, guideUserTipsText?: string, guideUserBtnText?: string): void;`

Parameter Description

| Parameter | Description |
|-----------|-------------|
| guideUser | Whether to show the guidance popup if the user has not granted permissions |
| guideUserTipsText | The content displayed in the guidance popup |
| guideUserBtnText | The text of the button in the guidance popup |

Code Example:

```TypeScript
requestPermissions () {
    huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.requestPermissionsCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
        console.log(result);
    })
    this.mmsdkService.requestPermissions(true, "Permission is required to use this feature", "Go to enable");
}
```

#### Initialization (Instance Creation)

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-engine-android-0000001193958984)

```TypeScript
init(info: {
    openId: string;
    agcAppId: string;
    agcClientId: string;
    agcClientSecret: string;
    agcApiKey: string;
    logEnable: boolean;
    logSize: number;
    countryCode: string;
    useSign: boolean;
    sign: string;
    nonce: string;
    timeStamp: string;
}): void;
```

Parameter Description

|Parameter|Description|
|-|-|
|openId|Unique identifier of the user, compulsory|
|agcAppId|Procured from AGC backend, compulsory|
|agcClientId|Procured from AGC backend, compulsory|
|agcClientSecret|Procured from AGC backend, compulsory|
|agcApiKey|Procured from AGC backend, compulsory|
|logEnable|	Activation of logs, compulsory|
|logSize|Capacity of log storage, compulsory|
|countryCode|Country code designated for gateway routing, default is 'CN', compulsory|
|useSign|Activation of security fortification, compulsory, true or false|
|sign|Access signature created by developer, compulsory, pass "" if security fortification is not utilized|
|nonce|Random number of the access signature created by developer, compulsory, pass "" if security fortification is not utilized|
|timeStamp|Timestamp of the access signature created by developer, compulsory, pass "" if security fortification is not utilized|



Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.initCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
let info = {
    openId: "",
    agcAppId: "",
    agcClientId: "",
    agcClientSecret: "",
    agcApiKey: "",
    logEnable: true,
    logSize: 10240,
    countryCode: "CN",
    useSign: false,
    sign: "",
    nonce: "",
    timeStamp: "",
}
this.mmsdkService.init(info);
```

#### Destroy instance

`destroy(): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-engine-android-0000001193958984)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onDestroyCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.destroy();
```

### Real-time vocal

#### Join the Team Room

`joinTeamRoom(roomId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-joinroom-roomid-android-0000001268934473)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onJoinTeamRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.joinTeamRoom("XXX");
```

#### Join the National War Room


`joinNationalRoom(roomId: string, roleType: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-joinroom-roomid-android-0000001268934473#section429414312194)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|
|roleType|Player role, 1 represents the commander, 2 represents the crowd|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onJoinNationalRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.joinNationalRoom("XXX", 1);
```

#### Switch Room

`switchRoom(roomId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-switchroom-android-0000001215529668)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onSwitchRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.switchRoom("XXX");
```

#### Transfer Room Owner Identity

`transferOwner(roomId: string, ownerId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-transferowner-android-0000001271687137)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|
|ownerId|New Room Owner ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onTransferOwnerCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.transferOwner("XXX", "XXX");
```

#### Get Specific Room Information

`getRoom (roomId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-getroom-android-0000001245095829)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.getRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
      console.log(result);
})
huawei.game.mmsdk.mmsdkService.getRoom("XXX");
```

#### Leave Room

`leaveRoom (roomId: string, ownerId?: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-leaveroom-android-0000001233098849)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Custom Room ID|
|ownerId|New Room Owner ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onLeaveRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.leaveRoom("XXX", null);
```

#### Set Microphone Status

`enableMic (isEnabled: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-enablemic-android-0000001197485354)

Parameter Description

|Parameter|Description|
|-|-|
|isEnabled|true indicates on, false indicates off|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.enableMicCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.enableMic(true);
```

#### Mute/Unmute Specific Player

`forbidPlayer (roomId: string, openId: string, isForbidden: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-forbidplayer-android-0000001242285225)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|openId|Player ID|
|isForbidden|true indicates mute, false indicates unmute|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onForbidPlayerCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
      console.log(result);
  })
huawei.game.mmsdk.mmsdkService.forbidPlayer("XXX", "XXX", true);
```

#### Mute/Unmute All Players

`forbidAllPlayers (roomId: string, isForbidden: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-forbidplayer-android-0000001242285225)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|isForbidden|true indicates mute, false indicates unmute|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onForbidAllPlayersCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
      console.log(result);
  })
huawei.game.mmsdk.mmsdkService.forbidAllPlayers("XXX",true);
```

#### Block/Unblock Specific Player's Voice

`mutePlayer (roomId: string, openId: string, isMuted: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-muteplayer-android-0000001197645332)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|openId|Player ID|
|isMuted|true indicates block voice, false indicates unblock|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onMutePlayerCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.mutePlayer("XXX", "XXX", true);
```

#### Block/Unblock Other All Players' Voice

`muteAllPlayers (roomId: string, isMuted: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-muteplayer-android-0000001197645332)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|isMuted|true indicates block voice, false indicates unblock|

Code Example

```TypeScript
 huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onMuteAllPlayersCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.muteAllPlayers(this._teamRoomId, true);
```

#### Get Current Speaking Players List


[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-enablespeakersdetection-android-0000001242224953)

`enableSpeakersDetection (roomId: string, interval: number): void;`

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|interval|Current speaking players list callback interval, valid range is [100, 10000], unit: ms, when input is 0, it means to close the volume callback|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.enableSpeakersDetection("XXX", 1000);
```

#### Initialize 3D Sound Effect

`initSpatialSound (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section1685641114101)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.initSpatialSoundCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.initSpatialSound();
```

#### Enable/Disable 3D Sound Effect


`enableSpatialSound (roomId: string, enable: boolean): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section1496016465103)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|enable|Whether to enable 3D sound effect, true indicates enable, false indicates disable|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.enableSpatialSoundCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.enableSpatialSound("XXX", true);
```

#### Set Voice Receiving Range

`setAudioRecvRange (range: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section35878131182)

Parameter Description

|Parameter|Description|
|-|-|
|range|Range Integer|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.setAudioRecvRangeCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.setAudioRecvRange(10);
```

#### Update Self Position

`updateSelfPosition (forward: number, right: number, up: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section11572124810519)

Parameter Description

|Parameter|Description|
|-|-|
|forward|The player's coordinate value on the front axis (Z axis) of the world coordinate system.|
|right|The player's coordinate value on the right axis (X axis) of the world coordinate system.|
|up|The player's coordinate value on the upper axis (Y axis) of the world coordinate system.|	

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.updateSelfPositionCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.updateSelfPosition(1, 2, 3);
```

#### Update Other Player's Position


`updateRemotePosition (openId: string, forward: number, right: number, up: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section3976836369)

Parameter Description

|Parameter|Description|
|-|-|
|openId|Target Player ID|
|forward|The player's coordinate value on the front axis (Z axis) of the world coordinate system.|
|right|The player's coordinate value on the right axis (X axis) of the world coordinate system.|
|up|The player's coordinate value on the upper axis (Y axis) of the world coordinate system.|	


Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.updateRemotePositionCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.updateRemotePosition("XXX", 1, 2, 3);
```

#### Clear Other Player's Position


`clearRemotePlayerPosition (openId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section185619282094)

Parameter Description

|Parameter|Description|
|-|-|
|openId|Target Player ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.clearRemotePlayerPositionCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
      console.log(result);
})
huawei.game.mmsdk.mmsdkService.clearRemotePlayerPosition("XXX");
```

#### Clear Other All Players' Position Information


`clearAllRemotePositions (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section859216551087)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.clearAllRemotePositionsCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.clearAllRemotePositions();
```

#### Query 3D Sound Effect On State


`isEnableSpatialSound (roomId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section188399396116)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.isEnableSpatialSoundCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.isEnableSpatialSound("XXX");
```

#### Turn on/off voice changes

`enableVoiceConversion (roomId: string, voiceType: number): int;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-voiceconversion-android-0000001772670850)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|
|voiceType|Sound change type: Original sound type: Disable sound change|

Code Example

```TypeScript
let result = huawei.game.mmsdk.mmsdkService.enableVoiceConversion(this._teamRoomId, huawei.game.mmsdk.VoiceType.LOLITA);
```

#### Query the type of sound change

`getVoiceConversionType (roomId: string): int;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-voiceconversion-android-0000001772670850)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|

Code Example

```TypeScript
let result = huawei.game.mmsdk.mmsdkService.getVoiceConversionType(this._teamRoomId);
```

#### Test the sound effect

`enableEarsBack (enable: boolean): int;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-voiceconversion-android-0000001772670850)

Parameter Description

|Parameter|Description|
|-|-|
|enable|Turn on/off|

Code Example

```TypeScript
let result = huawei.game.mmsdk.mmsdkService.enableEarsBack(true);
```

#### Check the status of the in-ear monitors

`isEarsBackEnable (): boolean;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-voiceconversion-android-0000001772670850)


Code Example

```TypeScript
let result = huawei.game.mmsdk.mmsdkService.isEarsBackEnable();
```


#### Join Range Voice Room


`joinRangeRoom (roomId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-gmme-gamemediaengine-android-0000001238323625#section55155121859)

Parameter Description

|Parameter|Description|
|-|-|
|roomId|Room ID|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onJoinRangeRoomCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.joinRangeRoom("XXX");
```

### Real-time Signaling


#### Peer-to-peer Send Message


`publishRtmPeerMessage ({peerId: string, type: number, messageString: string, messageByte: Uint8Array}): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-peermessage-publish-android-0000001744761245)

Parameter Description

|Parameter|Description|
|-|-|
|peerId|Peer ID|
|type|Message type: 1 indicates text, 2 indicates binary|
|messageString|Information|
|messageByte|Information|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onPublishRtmPeerMessageCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.publishRtmPeerMessage(this._selfOpenId == "A" ? "B" : "A", 1, "xxxxx");
```

#### Subscribe Channel


`subscribeRtmChannel (channelId: string, playerProperties: {}): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channel-subscribe-android-0000001744760273)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|playerProperties|User properties|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onSubscribeRtmChannelCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.subscribeRtmChannel("123", {name: "xxxxx", age: "18"});
```

#### Cancel Channel


`unSubscribeRtmChannel (channelId: string): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channel-subscribe-android-0000001744760273)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onUnSubscribeRtmChannelCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.unSubscribeRtmChannel("123");
```

#### Publish Channel Message

```
publishRtmChannelMessage (jsonInfo: {
    channelId: string,
    messageType: number,
    allowCacheMsg: boolean,
    contentIdentify: boolean,
    adsIdentify: boolean,
    messageString: string,
    messageBytes: Uint8Array,
    receivers: string[],
}): void`
```
[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelmessage-publish-android-0000001697080110)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|messageType|Type of message: 1 indicates text, 2 indicates binary|
|allowCacheMsg|Indicates whether historical messages are cached: true means cached, false means not cached|
|contentIdentify|Indicates whether content risk control review is conducted: true means review is conducted, false means review is not conducted|
|adsIdentify|Indicates whether ad recognition is conducted: true means ad recognition is conducted, false means ad recognition is not conducted|
|messageString|String representing the message|
|messageBytes|Binary representation|
|receivers|List of recipients|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onPublishRtmChannelMessageCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.publishRtmChannelMessage({
    channelId: "123",
    messageType: 1,
    allowCacheMsg: true,
    contentIdentify: true,
    adsIdentify: true,
    messageString: "xxxxx",
    receivers: ["A", "B"]
});
```

#### Establish Player Properties

`setRtmChannelPlayerProperties (channelId: string, playerProperties: {}): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelplayerproperties-android-0000001748204089)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|playerProperties|Properties of the player |
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onSetRtmChannelPlayerPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.setRtmChannelPlayerProperties("123", {name: "xxxxx", age: "18"});
```

#### Query Player Properties


`getRtmChannelPlayerProperties (channelId: string, openIds: string[])`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelplayerproperties-android-0000001748204089)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|openIds|List of player ids |
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onGetRtmChannelPlayerPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.getRtmChannelPlayerProperties("123", ["A"]);
```

#### Delete Player Properties


`deleteRtmChannelPlayerProperties (channelId: string, keys: string[]): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelplayerproperties-android-0000001748204089)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|keys|Indexes of properties|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onDeleteRtmChannelPlayerPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.deleteRtmChannelPlayerProperties("123", ["name", "age"]);
```


#### Establish Channel Properties


`setRtmChannelPlayerProperties (channelId: string, playerProperties: {}): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelproperties-android-0000001697081086)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|playerProperties|map of channel properties|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onSetRtmChannelPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.setRtmChannelProperties("123", {name: "xxxxx", age: "18"});
```

#### Query Channel Properties


`getRtmChannelProperties (channelId: string): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelproperties-android-0000001697081086)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onGetRtmChannelPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.getRtmChannelProperties("123");
```

#### Delete Channel Properties

`deleteRtmChannelProperties (channelId: string, keys: string[])`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-channelproperties-android-0000001697081086)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|keys|Indexes of properties|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onDeleteRtmChannelPropertiesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.deleteRtmChannelProperties("123", ["name", "age"]);
```


#### Query Channel Details

`getRtmChannelInfo (channelId: string, returnMembers: boolean): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-getrtmchannelinfo-android-0000001752146193)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|returnMembers|Indicates whether member information is included|
Code Example

```TypeScript
 huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onGetRtmChannelInfoCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.getRtmChannelInfo("123", true);
```

#### Query Subscribed Channel List

`getRtmSubscribedChannelInfo ():void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-getrtmsubscribedchannelinfo-android-0000001752225993)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onGetRtmSubscribedChannelInfoCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.getRtmSubscribedChannelInfo();
```

#### Query Channel Historical Messages


`getRtmChannelHistoryMessages (channelId: string, startTime: number, count: number): void`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-getrtmchannelhistorymessages-android-0000001704306792)

Parameter Description

|Parameter|Description|
|-|-|
|channelId|Channel ID as a numeric string|
|startTime|Indicates the start time|
|count|Indicates the limit on the number of messages|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onGetRtmChannelHistoryMessagesCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
});
huawei.game.mmsdk.mmsdkService.getRtmChannelHistoryMessages("123", 1700119845015, 10);
```

### Voice Messages

#### Record Voice


`startRecordAudioMsg (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-record-play-audio-msg-android-0000001550814805)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.startRecordAudioMsgCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
})
huawei.game.mmsdk.mmsdkService.startRecordAudioMsg();
```

#### Stop Recording Voice

`stopRecordAudioMsg (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-record-play-audio-msg-android-0000001550814805)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onRecordAudioMsgCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    this.console.log(result);
})
huawei.game.mmsdk.mmsdkService.stopRecordAudioMsg();
```
#### Upload Audio File to Game Multimedia Server


`uploadAudioMsgFile (filePath: string, msTimeOut: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-record-play-audio-msg-android-0000001550814805)

Parameter Description

|Parameter|Description|
|-|-|
|filePath|Pathway to the audio file information|
|msTimeOut|Timeout period in milliseconds, range [3000, 7000].|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onUploadAudioMsgFileCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.uploadAudioMsgFile("XXX", 5000);
```

#### Download Audio File

`downloadAudioMsgFile (fileId: string, filePath: string, msTimeOut: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-record-play-audio-msg-android-0000001550814805#section124701481487)

Parameter Description

|Parameter|Description|
|-|-|
|fileId|Unique identifier for the file to be downloaded, i.e., file ID.|
|filePath|Storage address for the downloaded file.|
|msTimeOut|Timeout period in milliseconds, range [3000, 7000].|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onDownloadAudioMsgFileCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.downloadAudioMsgFile("XXX", "XXX", 3000);
```

#### Detect Audio File

`startDetectAudioFile (fileId: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-record-play-audio-msg-android-0000001550814805#section124701481487)

Parameter Description

|Parameter|Description|
|-|-|
|fileId|Unique identifier for the file to be downloaded, i.e., file ID.|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onStartDetectAudioFileCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.startDetectAudioFile("XXX");
```

#### Play Voice Message


`playAudioMsg (filePath: string): void;`

Parameter Description

|Parameter|Description|
|-|-|
|filePath|Pathway to the audio file information|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onPlayAudioMsgCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.playAudioMsg("XXX");
```

#### Stop Playing Voice Message


`stopPlayAudioMsg (): void;`

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onPlayAudioMsgCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.stopPlayAudioMsg();
```

#### Obtain Audio File Information


`getAudioMsgFileInfo (filePath: string): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-References/gamemme-model-audiomsgfileinfo-android-0000001499283292#section1515222884713)

Parameter Description

|Parameter|Description|
|-|-|
|filePath|The file pathway pertaining to the audio file information.|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.getAudioMsgFileInfoCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.getAudioMsgFileInfo(filePath);
```

### Initiation of sound effect playback.
#### Play

`playLocalAudioClip (soundId: number, volume: number, filePath: string, loop: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
|volume|The coefficient of sound effect volume ranges between [0, 100], with the default value being 100.|
|filePath|The pathway for the sound effect file, which may be either a local pathway or a network URL.|
|loop|The number of cyclical plays, greater than or equivalent to zero, with a default value of zero denoting infinite repetition.|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.playLocalAudioClip(1, 100, "http://music.163.com/song/media/outer/url?id=25906124.mp3", 1);
```
    
#### Pause

`pauseLocalAudioClip (soundId: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.pauseLocalAudioClip(1);
```  
  
#### Pause all local audio clips

`pauseAllLocalAudioClips (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.pauseAllLocalAudioClips();
```  
#### Resume

`resumeLocalAudioClip (soundId: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.resumeLocalAudioClip(1);
```  
    
#### Resume all local audio clips

`resumeAllLocalAudioClips (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.resumeAllLocalAudioClips();
```

#### Stop

`stopLocalAudioClip (soundId: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.stopLocalAudioClip(1);
```  
    
#### Stop all local audio clips

`stopAllLocalAudioClips (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.stopAllLocalAudioClips();
```

#### Designate the volume coefficient for a specific sound effect or for all sound effects.

`setVolumeOfLocalAudioClip (soundId: number, volume: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
|volume|The coefficient of sound effect volume ranges between [0, 100], with the default value being 100.|

Code Example

```TypeScript
    huawei.game.mmsdk.mmsdkService.setVolumeOfLocalAudioClip(1, 50);
```

#### Establish the volume coefficient for all local sound effects

`setVolumeOfLocalAudioClip (volume: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|volume|The coefficient of sound effect volume ranges between [0, 100], with the default value being 100.|

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.setLocalAudioClipsVolume(80);
```

#### Procure the volume coefficient of a specified sound effect or all sound effects.

`getVolumeOfLocalAudioClip (soundId: number): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Parameter Description

|Parameter|Description|
|-|-|
|soundId|Sound effect ID, greater than or equivalent to 0.|
|volume|The coefficient of sound effect volume ranges between [0, 100], with the default value being 100.|

Code Example

```TypeScript
    huawei.game.mmsdk.mmsdkService.getVolumeOfLocalAudioClip(1);
```

#### Acquire the volume coefficient of all local sound effects.

`getLocalAudioClipsVolume (): void;`

[Guide](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-playlocalaudioclip-android-0000001604797460)

Code Example

```TypeScript
huawei.game.mmsdk.mmsdkService.getLocalAudioClipsVolume();
```

### Speech to Text
#### Speech to Text - Start Recording

`startRecordAudioToText (language: string): void;`

Parameter explanation

| Parameter | Description |
| --- | --- |
| language | Language code, only supports 'zh' and 'en_US' |

Code example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.startRecordAudioToTextCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log("Recording, please speak...")
})
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onVoiceToTextCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.startRecordAudioToText("zh");
```

#### Speech to Text - Stop Recording

`stopRecordAudioToText (): void;`

Code example

```TypeScript
huawei.game.mmsdk.mmsdkService.once(huawei.game.mmsdk.API_EVENT_LIST.onVoiceToTextCallback, (result: huawei.game.mmsdk.ApiCbResult) => {
    console.log(result);
})
huawei.game.mmsdk.mmsdkService.stopRecordAudioToText();
```

## Others

For a detailed function description, please refer to [Game Multimedia - Guide](https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/gamemme-introduction-0000001226565909).