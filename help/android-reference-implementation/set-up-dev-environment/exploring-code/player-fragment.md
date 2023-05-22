---
description: PlayerFragment 클래스에서 코드를 편집하여 완전히 활성화된 기능 관리자를 생성합니다.
title: PlayerFragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# PlayerFragment {#playerfragment}

PlayerFragment 클래스에서 코드를 편집하여 완전히 활성화된 기능 관리자를 생성합니다.

다음 `PlayerFragment` 클래스에는 와 같은 모든 UI 구성 요소가 포함됩니다. `playerFrame`, `ControlBar`, `playerClickableAdFragment`, 및 `adOverlay`.

이러한 모든 구성 요소의 초기화를 처리하며 플레이어 만들기, 보기 설정, 미디어 플레이어의 기능 관리자 만들기, 다시 시작, 재생 및 일시 중지와 같은 미디어 이벤트 처리 및 이벤트 리스너 처리 작업을 수행합니다 `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`, 및 `EntitlementManager`.

에 대한 구성 매개 변수를 포함하는 XML 파일 `PlayerFragment` 은(는) `res/layout/fragment_player.xml`.

기능 관리자를 만들기 전에 다음 코드가 에 있는지 확인하여 미디어 플레이어를 만들어야 합니다. `PlayerFragment.java` 파일:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
