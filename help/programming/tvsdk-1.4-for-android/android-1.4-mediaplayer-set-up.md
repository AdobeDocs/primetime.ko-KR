---
description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-title: MediaPlayer 설정
title: MediaPlayer 설정
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# MediaPlayer {#set-up-the-mediaplayer} 설정

Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스인 `DefaultMediaPlayer` 클래스의 한 가지 구현을 제공합니다. 비디오 재생 기능이 필요한 경우 `DefaultMediaPlayer`을(를) 인스턴스화합니다.

>[!TIP]
>
>`DefaultMediaPlayer` 인스턴스와 상호 작용하려면 `MediaPlayer` 인터페이스에서 노출되는 메서드만 사용합니다.

1. 공용 `DefaultMediaPlayer.create` 팩토리 메서드를 사용하여 MediaPlayer를 인스턴스화하여 Java Android 응용 프로그램 컨텍스트 개체를 전달합니다.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. `MediaPlayer.getView`을(를) 호출하여 `MediaPlayerView` 인스턴스에 대한 참조를 가져옵니다.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. `MediaPlayerView` 인스턴스를 `FrameLayout` 인스턴스에 배치합니다. 이 인스턴스는 장치의 화면에 비디오를 배치합니다.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 내용을 표시하도록 올바르게 구성됩니다.
