---
description: MediaPlayer 인스턴스가 만들어진 순간부터 종료되는 순간까지 이 인스턴스는 한 상태에서 다음 상태로 전환됩니다.
title: MediaPlayer 객체의 라이프 사이클 및 상태
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# MediaPlayer 객체의 라이프 사이클 및 상태{#life-cycle-and-states-of-the-mediaplayer-object}

MediaPlayer 인스턴스가 만들어진 순간부터 종료되는 순간까지 이 인스턴스는 한 상태에서 다음 상태로 전환됩니다.

가능한 상태는 다음과 같습니다.

* **유휴**:  `MediaPlayerStatus.IDLE`

* **초기화** 중:  `MediaPlayerStatus.INITIALIZING`

* **초기화됨**:  `MediaPlayerStatus.INITIALIZED`

* **준비**:  `MediaPlayerStatus.PREPARING`

* **준비**:  `MediaPlayerStatus.PREPARED`

* **재생**:  `MediaPlayerStatus.PLAYING`

* **일시 중지됨**:  `MediaPlayerStatus.PAUSED`

* **검색**:  `MediaPlayerStatus.SEEKING`

* **완료**:  `MediaPlayerStatus.COMPLETE`

* **오류**:  `MediaPlayerStatus.ERROR`

* **릴리스**:  `MediaPlayerStatus.RELEASED`

전체 상태 목록은 `MediaPlayerStatus`에 정의되어 있습니다.

플레이어가 특정 상태에 있는 동안에만 일부 작업이 허용되므로 플레이어의 상태를 파악하는 것이 유용합니다. 예를 들어 유휴 상태인 동안에는 `play`을(를) 호출할 수 없습니다. 준비 상태에 도달한 후에 호출해야 합니다. ERROR 상태는 다음에 발생할 수 있는 사항도 변경합니다.

미디어 리소스가 로드되고 재생되면 플레이어는 다음과 같은 방식으로 전환됩니다.

1. 초기 상태는 IDLE입니다.
1. 응용 프로그램에서 `MediaPlayer.replaceCurrentResource`을(를) 호출하여 플레이어를 INITIALIZING 상태로 이동합니다.
1. 브라우저 TVSDK가 리소스를 성공적으로 로드하면 상태가 INITIALIZED로 변경됩니다.
1. 응용 프로그램에서 `MediaPlayer.prepareToPlay`을 호출하고 상태가 PREPARING으로 변경됩니다.
1. 브라우저 TVSDK가 미디어 스트림을 준비하고 광고 확인 및 광고 삽입(활성화된 경우)을 시작합니다.

   이 단계가 완료되면 광고가 타임라인에 삽입되거나 광고 절차가 실패하여 플레이어 상태가 PREMITED로 변경됩니다.
1. 응용 프로그램이 미디어를 재생 및 일시 정지하면 상태는 PLAYING과 PAUSED 간에 이동합니다.

   >[!TIP]
   >
   >재생 또는 일시 정지하는 동안 재생 외부로 이동하거나 장치를 종료하거나 애플리케이션을 전환할 때 상태가 일시 중단됨으로 변경되고 리소스가 해제됩니다. 계속하려면 미디어 플레이어를 복원합니다.

1. 플레이어가 스트림의 끝에 도달하면 상태가 COMPLETE가 됩니다.
1. 응용 프로그램에서 미디어 플레이어를 릴리스하면 상태가 RELEASED로 변경됩니다.
1. 프로세스 중에 오류가 발생하면 상태가 ERROR로 변경됩니다.

다음은 MediaPlayer 인스턴스의 라이프사이클에 대한 그림입니다.

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

상태를 사용하여 프로세스(예: 다음 상태 변경을 기다리는 동안 스피너)에 대한 피드백을 제공하거나 다음 메서드를 호출하기 전에 적절한 상태를 기다리는 등의 미디어 재생 시 다음 단계를 수행할 수 있습니다.

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

