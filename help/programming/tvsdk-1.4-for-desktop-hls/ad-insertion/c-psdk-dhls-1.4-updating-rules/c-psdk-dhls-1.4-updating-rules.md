---
description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브를 위한 소스 URL 변형 규칙을 정의할 수도 있습니다.
title: 광고 크리에이티브 선택 규칙 업데이트
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# 개요 {#updating-ad-creative-selection-rules}

TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브를 위한 소스 URL 변형 규칙을 정의할 수도 있습니다.

비디오 플레이어가 광고 서버에 요청을 하면 VAST/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` 요소)가 포함되며, 각각은 다른 컨테이너-코덱에 대한 URL을 제공합니다. 경우에 따라 VAST/VMAP 응답의 광고 크리에이티브는 각각 광고에 대해 다른 비트 전송률을 제공합니다. 이러한 광고 크리에이티브를 위한 고유한 우선순위 및 변형 규칙을 지정하려면 [!DNL AdobeTVSDKConfig.json] 구성 파일에서 지정할 수 있습니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 [!DNL AdobeTVSDKConfig.json]이어야 합니다.
>* 이 파일은 CDN(Content Delivery Network)에서 호스팅되어야 합니다.

>



[!DNL AdobeTVSDKConfig.json]에서 두 가지 유형의 규칙을 지정할 수 있습니다.*우선순위* 규칙 및 *표준화* 규칙
