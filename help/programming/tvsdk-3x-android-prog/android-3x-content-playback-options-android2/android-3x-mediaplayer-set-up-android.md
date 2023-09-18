---
description: TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다. 또한 비디오 재생 품질을 극대화하도록 설계된 다양한 기능을 제공합니다.
title: 미디어 플레이어 설정
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# 미디어 플레이어 설정 {#set-up-the-media-player}

TVSDK는 다른 Primetime 구성 요소와 통합할 수 있는 고급 비디오 플레이어 애플리케이션(Primetime 플레이어)을 만드는 도구를 제공합니다. 또한 비디오 재생 품질을 극대화하도록 설계된 다양한 기능을 제공합니다.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

인스턴스화 `MediaPlayer` 프레임 레이아웃에 뷰를 배치합니다.

1. 인스턴스화 `MediaPlayer`, 전달 `android.content.Context` 개체를 생성자에 추가합니다.

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 프레임 레이아웃 제공( `android.widget.FrameLayout`)을 클릭하여 `ViewGroup` / `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >다음은 생성할 코드 조각입니다. `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 보기 배치 `mediaPlayer` 프레임 레이아웃 내에서:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >다음 `MediaPlayer` 인스턴스( `mediaPlayer`이제 를 사용할 수 있으며, 장치 화면에 비디오 컨텐츠를 표시하도록 적절히 구성되었습니다.
