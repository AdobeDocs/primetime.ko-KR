---
description: 클라이언트 플레이어에서 자막을 사용할 수 있게 하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.
seo-description: 클라이언트 플레이어에서 자막을 사용할 수 있게 하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.
seo-title: 자막 노출
title: 자막 노출
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 자막 표시 {#expose-closed-captions}

클라이언트 플레이어에서 자막을 사용할 수 있게 하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.

자막을 노출하려면

1. `PTMediaPlayer` 개체에서 `closedCaptionDisplayEnabled` 속성을 설정합니다.

   사용자가 자막을 활성화한 경우 이 단계는 텍스트를 표시합니다.

   >[!NOTE]
   >
   >클라이언트 사용자는 iOS 액세스 가능성 설정을 사용하여 자막을 켜거나 끌 수 있고 이러한 설정은 양식 옵션도 제공합니다.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 속성은 사용되지 않습니다. `PTMediaPlayerItem`의 `subtitlesOptions` 속성을 사용하십시오. 자막을 사용하려면 [자막 노출](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md)을 참조하십시오.