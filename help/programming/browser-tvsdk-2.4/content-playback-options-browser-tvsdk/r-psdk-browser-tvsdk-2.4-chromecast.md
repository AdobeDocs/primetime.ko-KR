---
description: TVSDK 기반의 발신자 앱에서 스트림을 캐스팅할 수 있으며, 스트림이 Chromecast에서 Browser TVSDK를 사용하여 재생되도록 할 수 있습니다.
seo-description: TVSDK 기반의 발신자 앱에서 스트림을 캐스팅할 수 있으며, 스트림이 Chromecast에서 Browser TVSDK를 사용하여 재생되도록 할 수 있습니다.
seo-title: 브라우저 TVSDK용 Google Cast 앱
title: 브라우저 TVSDK용 Google Cast 앱
uuid: 018143e2-143a-4f88-97c6-4b10a2083f9e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# 브라우저 TVSDK용 Google Cast 앱{#google-cast-app-for-browser-tvsdk}

TVSDK 기반의 발신자 앱에서 스트림을 캐스팅할 수 있으며, 스트림이 Chromecast에서 Browser TVSDK를 사용하여 재생되도록 할 수 있습니다.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

캐스트 지원 앱에는 두 가지 구성 요소가 있습니다.

* 원격 제어 역할을 하는 발신자 앱.

   발신자 앱에는 스마트폰, PC 등이 포함됩니다. iOS, Android 및 Chrome용 기본 SDK를 사용하여 앱을 개발할 수 있습니다.
* Chromecast에서 실행되고 컨텐츠를 재생하는 수신기 앱입니다.

   >[!IMPORTANT]
   >
   >이 앱은 HTML5 앱만 될 수 있습니다.

보낸 사람과 받는 사람은 Cast SDK를 사용하여 메시지를 전달하여 통신합니다.

## 기본 워크플로 {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

다음은 프로세스에 대한 개요입니다.

1. 보낸 사람 앱이 받는 사람 앱과의 연결을 설정합니다.
1. 보낸 사람 앱은 받는 사람 앱에서 미디어를 로드하라는 메시지를 보냅니다.
1. 수신기 앱이 재생을 시작합니다.
1. 발신자 앱은 재생, 일시 중지, 검색, 빨리 감기, 빨리 되감기, 되감기, 볼륨 변경 등과 같은 재생 제어 메시지를 수신자 앱으로 전송합니다.
1. 수신기 앱은 이러한 메시지에 반응합니다.

## 메시지 형식 {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

보낸 사람과 받는 사람이 이해할 수 있도록 메시지를 정의해야 합니다. 다음은 검색 메시지의 예입니다.

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Cast SDK를 통해 검색 메시지와 같은 사용자 지정 메시지를 전송할 때는 사용자 지정 메시지 네임스페이스가 필요합니다. 다음은 JavaScript의 예입니다.

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 연결 {#section_B4D40CABDD3E46FDBE7B5651DFF91653} 설정

>[!IMPORTANT]
>
>브라우저 TVSDK API는 연결을 설정할 때 관련 없습니다.

연결을 설정하려면 보낸 사람과 받는 사람이 다음 작업을 완료해야 합니다.

* 보낸 사람은 [보낸 사람 앱 개발](https://developers.google.com/cast/docs/sender_apps)에서 플랫폼의 설명서를 검토해야 합니다.
* 수신자는 Cast 수신기 API를 사용하여 발신자 앱과의 연결을 설정합니다. 예:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## 메시지 처리 {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

수신자에게 메시지를 보내려면 보낸 사람의 플랫폼에 대한 설명서를 참조하십시오.

>[!IMPORTANT]
>
>모든 메시지에 사용자 지정 메시지 네임스페이스인 `MSG_NAMESPACE`을(를) 포함해야 합니다.

수신기 앱의 경우 캐스트 수신기 API에 대한 설명서를 따르십시오.

**크롬 기반 보낸 사람 메시지 예**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Chrome 기반 보낸 사람 이벤트 처리**

해당 이벤트가 트리거될 때 메시지를 전송할 UI 요소에 이벤트 핸들러를 바인딩합니다. 예를 들어 Chrome 기반 보낸 사람 앱의 경우 검색 이벤트가 다음과 같이 전송될 수 있습니다.

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**받는 사람 메시지 처리**

다음은 리시버 앱에서 검색 메시지를 처리하는 방법의 예입니다.

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

