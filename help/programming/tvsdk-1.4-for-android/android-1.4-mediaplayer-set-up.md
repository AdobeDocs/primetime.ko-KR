---
description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
title: MediaPlayer 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# MediaPlayer 설정 {#set-up-the-mediaplayer}

Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스, `DefaultMediaPlayer` 클래스. 비디오 재생 기능이 필요한 경우 를 인스턴스화합니다. `DefaultMediaPlayer`.

>[!TIP]
>
>와 상호 작용 `DefaultMediaPlayer` 에 의해 노출된 메서드만 사용하는 인스턴스 `MediaPlayer` 인터페이스.

1. 공용 을 사용하여 MediaPlayer 인스턴스화 `DefaultMediaPlayer.create` factory 메서드, Java Android 애플리케이션 컨텍스트 개체를 전달합니다.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 호출 `MediaPlayer.getView` 에 대한 참조를 가져오려면 `MediaPlayerView` 인스턴스.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 배치 `MediaPlayerView` 인스턴스 위치: `FrameLayout` 디바이스의 화면에 비디오를 배치하는 인스턴스.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

다음 `MediaPlayer` 이제 인스턴스를 사용할 수 있으며 장치 화면에 비디오 콘텐츠를 표시하도록 올바르게 구성되었습니다.
