---
description: 클라이언트 플레이어에서 자막을 사용할 수 있게 하려면 자막을 활성화해야 합니다. 사용자는 닫힌 캡션을 켜거나 끄고 서식을 선택할 수 있습니다.
title: 자막 노출
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 닫힌 캡션 표시 {#expose-closed-captions}

클라이언트 플레이어에서 자막을 사용할 수 있게 하려면 자막을 활성화해야 합니다. 사용자는 닫힌 캡션을 켜거나 끄고 서식을 선택할 수 있습니다.

닫힌 캡션을 표시하려면:

1. `PTMediaPlayer` 개체에서 `closedCaptionDisplayEnabled` 속성을 설정합니다.

   사용자가 닫힌 캡션을 활성화한 경우 이 단계에서는 텍스트가 표시됩니다.

   >[!NOTE]
   >
   >클라이언트 사용자는 iOS 액세서빌러티 설정을 사용하여 자막을 켜거나 끌 수 있고 이러한 설정은 양식 옵션도 제공합니다.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 속성은 사용되지 않습니다. `PTMediaPlayerItem`의 `subtitlesOptions` 속성을 사용합니다. 닫힌 캡션을 사용하려면 [자막 노출](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md)을 참조하십시오.