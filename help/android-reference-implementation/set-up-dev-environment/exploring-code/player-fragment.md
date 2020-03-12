---
description: PlayerFragment 클래스는 코드를 편집하여 전체 활성화 기능 관리자를 생성하는 곳입니다.
seo-description: PlayerFragment 클래스는 코드를 편집하여 전체 활성화 기능 관리자를 생성하는 곳입니다.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# PlayerFragment {#playerfragment}

PlayerFragment 클래스는 코드를 편집하여 전체 활성화 기능 관리자를 생성하는 곳입니다.

이 `PlayerFragment` 클래스에는 `playerFrame`, `ControlBar`및 `playerClickableAdFragment`같은 모든 UI 구성 요소가 포함되어 `adOverlay`있습니다.

이러한 모든 구성 요소의 초기화는 물론 플레이어 만들기, 보기 설정, 미디어 플레이어용 기능 관리자 만들기, 다시 시작, 재생 및 일시 중지 등과 같은 미디어 이벤트 처리, `QoSManager``DRMManager``CCManager`, `AAManager``AdsManager`및 이벤트 리스너 처리 `PlaybackManager`등을 `EntitlementManager`처리합니다.

의 구성 매개 변수를 포함하는 XML 파일은 `PlayerFragment` 입니다 `res/layout/fragment_player.xml`.

기능 관리자를 만들기 전에 다음 코드가 `PlayerFragment.java` 파일에 있는지 확인하여 미디어 플레이어를 만들어야 합니다.

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
