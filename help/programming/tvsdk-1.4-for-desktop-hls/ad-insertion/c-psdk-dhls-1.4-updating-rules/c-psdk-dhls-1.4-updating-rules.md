---
description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.
title: 광고 크리에이티브 선택 규칙 업데이트
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 개요 {#updating-ad-creative-selection-rules}

TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.

비디오 플레이어가 광고 서버에 요청할 때 VAST/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` elements): 각각 다른 컨테이너-코덱 버전에 URL을 제공합니다. 경우에 따라 VAST/VMAP 응답의 광고 크리에이티브가 각각 광고에 대한 다른 비트율을 제공합니다. 이러한 광고 크리에이티브에 대한 자체 우선 순위 및 변형 규칙을 지정하려면 다음에서 수행할 수 있습니다. [!DNL AdobeTVSDKConfig.json] 구성 파일입니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 유지해야 합니다. [!DNL AdobeTVSDKConfig.json].
>* 이 파일은 CDN(콘텐츠 전송 네트워크)에서 호스팅해야 합니다.
>


에서 두 가지 유형의 규칙을 지정할 수 있습니다. [!DNL AdobeTVSDKConfig.json]: *우선 순위* 규칙 및 *정규화* 규칙.
