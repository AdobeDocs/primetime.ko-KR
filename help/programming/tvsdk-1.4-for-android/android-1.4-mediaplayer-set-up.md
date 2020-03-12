---
description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.
seo-title: MediaPlayer 설정
title: MediaPlayer 설정
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer 설정 {#set-up-the-mediaplayer}

Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 동작을 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스, 즉 `DefaultMediaPlayer` 클래스를 하나의 구현으로 제공합니다. 비디오 재생 기능이 필요할 때 인스턴스화합니다 `DefaultMediaPlayer`.

>[!TIP]
>
>인터페이스에서 노출되는 메서드와만 `DefaultMediaPlayer` 인스턴스와 상호 작용합니다 `MediaPlayer` .

1. 공용 팩토리 방법을 사용하여 MediaPlayer를 `DefaultMediaPlayer.create` 인스턴스화하여 Java Android 응용 프로그램 컨텍스트 객체를 전달합니다.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 인스턴스에 `MediaPlayer.getView` 대한 참조를 얻으려면 `MediaPlayerView` 호출합니다.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 장치의 화면에 비디오를 배치하는 인스턴스에 `MediaPlayerView` `FrameLayout` 인스턴스를 배치합니다.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 컨텐츠를 표시하도록 올바르게 구성됩니다.
