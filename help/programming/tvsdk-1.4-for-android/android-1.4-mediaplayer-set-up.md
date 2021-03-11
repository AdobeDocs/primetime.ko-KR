---
description: Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 비헤이비어를 캡슐화합니다.
title: MediaPlayer 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# MediaPlayer {#set-up-the-mediaplayer} 설정

Android용 MediaPlayer 인터페이스는 미디어 플레이어의 기능과 비헤이비어를 캡슐화합니다.

TVSDK는 `MediaPlayer` 인터페이스, `DefaultMediaPlayer` 클래스의 단일 구현을 제공합니다. 비디오 재생 기능이 필요하면 `DefaultMediaPlayer`을(를) 인스턴스화합니다.

>[!TIP]
>
>`DefaultMediaPlayer` 인스턴스와 `MediaPlayer` 인터페이스에서 노출되는 메서드만 상호 작용합니다.

1. Java Android 응용 프로그램 컨텍스트 객체를 전달하여 public `DefaultMediaPlayer.create` factory 메서드를 사용하여 MediaPlayer를 인스턴스화합니다.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. `MediaPlayer.getView`을(를) 호출하여 `MediaPlayerView` 인스턴스에 대한 참조를 가져옵니다.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. `MediaPlayerView` 인스턴스를 장치의 화면에 비디오를 배치하는 `FrameLayout` 인스턴스에 배치합니다.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

이제 `MediaPlayer` 인스턴스를 사용할 수 있으며 장치 화면에 비디오 내용을 표시하도록 올바르게 구성됩니다.
