---
description: 클라이언트 플레이어에서 자막을 사용하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.
seo-description: 클라이언트 플레이어에서 자막을 사용하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.
seo-title: 자막 노출
title: 자막 노출
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# 자막 노출 {#expose-closed-captions}

클라이언트 플레이어에서 자막을 사용하려면 자막을 활성화해야 합니다. 사용자는 자막을 켜거나 끄고 서식을 선택할 수 있습니다.

자막을 표시하려면:

1. 개체에서 속성을 `PTMediaPlayer` 설정합니다 `closedCaptionDisplayEnabled` .

   사용자가 자막을 활성화한 경우 이 단계에서는 텍스트가 표시됩니다.

   >[!NOTE]
   >
   >클라이언트 사용자는 iOS 액세서빌러티 설정을 사용하여 폐쇄자막을 켜거나 끌 수 있으며 이러한 설정은 양식 옵션도 제공합니다.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 속성은 더 이상 사용되지 않습니다. 의 `subtitlesOptions` 속성을 `PTMediaPlayerItem`사용합니다. 자막을 [사용하여 자막](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) 표시를 참조하십시오.