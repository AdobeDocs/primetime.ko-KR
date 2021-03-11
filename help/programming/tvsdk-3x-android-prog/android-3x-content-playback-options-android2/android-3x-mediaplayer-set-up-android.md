---
description: TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하기 위한 툴을 제공합니다. 또한 비디오 재생 품질을 극대화하기 위해 고안된 다양한 기능을 제공합니다.
title: 미디어 플레이어 설정
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 미디어 플레이어 {#set-up-the-media-player} 설정

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 제작하기 위한 툴을 제공합니다. 또한 비디오 재생 품질을 극대화하기 위해 고안된 다양한 기능을 제공합니다.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

`MediaPlayer`을 인스턴스화하고 프레임 레이아웃에 해당 뷰를 배치합니다.

1. `MediaPlayer`을 인스턴스화하고 `android.content.Context` 객체를 생성자에게 전달합니다.

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. `mediaPlayer`의 `ViewGroup`을(를) 저장할 프레임 레이아웃( `android.widget.FrameLayout`)을 제공합니다.

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >다음은 `_viewGroup`을(를) 만드는 코드 조각입니다.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 프레임 레이아웃 내에 `mediaPlayer` 보기를 배치합니다.

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >이제 `MediaPlayer` 인스턴스( `mediaPlayer`)를 사용할 수 있으며 장치 화면에 비디오 내용을 표시하도록 올바르게 구성됩니다.