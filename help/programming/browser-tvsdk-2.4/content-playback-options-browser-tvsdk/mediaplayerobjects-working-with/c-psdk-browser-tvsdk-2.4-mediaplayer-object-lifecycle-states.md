---
description: MediaPlayer 인스턴스가 만들어지는 순간부터 종료되는 순간까지 이 인스턴스는 한 상태에서 다음 상태로 전환됩니다.
title: MediaPlayer 개체의 수명 주기 및 상태
exl-id: 26cad982-ef85-42fb-aaa7-e5d494088766
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# MediaPlayer 개체의 수명 주기 및 상태{#life-cycle-and-states-of-the-mediaplayer-object}

MediaPlayer 인스턴스가 만들어지는 순간부터 종료되는 순간까지 이 인스턴스는 한 상태에서 다음 상태로 전환됩니다.

가능한 상태는 다음과 같습니다.

* **유휴 상태**: `MediaPlayerStatus.IDLE`

* **초기화 중**: `MediaPlayerStatus.INITIALIZING`

* **초기화됨**: `MediaPlayerStatus.INITIALIZED`

* **준비 중**: `MediaPlayerStatus.PREPARING`

* **준비됨**: `MediaPlayerStatus.PREPARED`

* **재생 중**: `MediaPlayerStatus.PLAYING`

* **일시 중지됨**: `MediaPlayerStatus.PAUSED`

* **찾기**: `MediaPlayerStatus.SEEKING`

* **완료**: `MediaPlayerStatus.COMPLETE`

* **오류**: `MediaPlayerStatus.ERROR`

* **릴리스됨**: `MediaPlayerStatus.RELEASED`

전체 상태 목록은 다음에 정의되어 있습니다. `MediaPlayerStatus`.

플레이어의 상태를 아는 것은 플레이어가 특정 상태에 있는 동안에만 일부 동작이 허용되기 때문에 유용하다. 예를 들어, `play` IDLE 상태에서는 를 호출할 수 없습니다. PREPARED 상태에 도달한 후 호출해야 합니다. ERROR 상태는 다음에 발생할 수 있는 사항도 변경합니다.

미디어 리소스가 로드되고 재생되면 플레이어는 다음과 같은 방식으로 전환됩니다.

1. 초기 상태는 IDLE입니다.
1. 애플리케이션이 호출함 `MediaPlayer.replaceCurrentResource`: 플레이어를 INITIALIZING 상태로 이동합니다.
1. 브라우저 TVSDK가 리소스를 성공적으로 로드하면 상태가 INITIALIZED로 변경됩니다.
1. 애플리케이션이 호출함 `MediaPlayer.prepareToPlay`, 그리고 상태가 준비로 변경됩니다.
1. 브라우저 TVSDK는 미디어 스트림을 준비하고 광고 해결 및 광고 삽입(활성화된 경우)을 시작합니다.

   이 단계가 완료되면 타임라인에 광고가 삽입되거나 광고 절차가 실패하고 플레이어 상태가 준비됨으로 변경됩니다.
1. 애플리케이션이 미디어를 재생하고 일시 중지하면 상태가 재생 및 일시 중지됨 간에 이동합니다.

   >[!TIP]
   >
   >재생 또는 일시 중지된 상태에서 재생 화면으로 이동하거나 디바이스를 종료하거나 애플리케이션을 전환하면 상태가 일시 중지됨으로 바뀌고 리소스가 해제됩니다. 계속하려면 미디어 플레이어를 복원하십시오.

1. 플레이어가 스트림 끝에 도달하면 상태는 COMPLETE가 됩니다.
1. 애플리케이션이 미디어 플레이어를 놓으면 상태가 릴리즈됨(RELEASED)으로 변경됩니다.
1. 프로세스 중에 오류가 발생하면 상태가 ERROR로 변경됩니다.

다음은 MediaPlayer 인스턴스의 수명 주기에 대한 그림입니다.

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

상태를 사용하여 프로세스에 대한 사용자 피드백을 제공하거나(예: 다음 상태 변경을 기다리는 동안 회전체) 다음 메서드를 호출하기 전에 적절한 상태를 기다리는 등, 미디어 재생의 다음 단계를 수행할 수 있습니다.

예:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 
```
