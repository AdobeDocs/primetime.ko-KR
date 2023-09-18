---
description: 폐쇄 캡션을 클라이언트 플레이어에서 사용할 수 있도록 하려면 폐쇄 캡션을 활성화해야 합니다. 사용자는 폐쇄 캡션을 켜거나 끄고 서식을 선택할 수 있습니다.
title: 폐쇄 캡션 표시
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 폐쇄 캡션 표시 {#expose-closed-captions}

폐쇄 캡션을 클라이언트 플레이어에서 사용할 수 있도록 하려면 폐쇄 캡션을 활성화해야 합니다. 사용자는 폐쇄 캡션을 켜거나 끄고 서식을 선택할 수 있습니다.

폐쇄 캡션을 노출하려면 다음 작업을 수행하십시오.

1. 위치 `PTMediaPlayer` 개체, 설정 `closedCaptionDisplayEnabled` 속성.

   사용자가 폐쇄 캡션을 활성화한 경우 이 단계에서는 텍스트를 표시합니다.

   >[!NOTE]
   >
   >클라이언트 사용자는 iOS 접근성 설정을 사용하여 폐쇄 캡션을 켜거나 끄고, 이러한 설정은 형식 지정 옵션도 제공합니다.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 속성은 더 이상 사용되지 않습니다. 사용 `subtitlesOptions` 다음의 속성 `PTMediaPlayerItem`. 다음을 참조하십시오 [자막 표시](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) 닫힘 캡션을 사용합니다.
