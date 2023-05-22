---
description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.
keywords: 크리에이티브 선택 규칙;AdobeTVSDKConfig;광고 크리에이티브 우선 순위;변환 규칙
title: 광고 크리에이티브 선택 규칙 업데이트
exl-id: da0420a0-6be9-47c8-bdd8-45f0f1860f28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 개요 {#update-ad-creative-selection-rules-overview}

TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에 대한 광고 크리에이티브 선택의 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브에 대한 소스 URL 변환 규칙을 정의할 수도 있습니다.

비디오 플레이어가 광고 서버에 요청할 때 VAST/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` elements): 각각 다른 컨테이너-코덱 버전에 URL을 제공합니다. 경우에 따라 VAST/VMAP 응답의 광고 크리에이티브가 각각 광고에 대한 다른 비트율을 제공합니다. 이러한 광고 크리에이티브에 대한 자체 우선 순위 및 변형 규칙을 지정하려면 다음에서 수행할 수 있습니다. [!DNL AdobeTVSDKConfig.json] 구성 파일입니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 유지해야 합니다. [!DNL AdobeTVSDKConfig.json].
>* 이 파일은 다음 위치에 배치해야 합니다. [!DNL assets/] 프로젝트의 폴더입니다.
>* 광고가 재생될 때 오디오 트랙을 변경해도 오디오 트랙은 변경되지 않습니다. 플레이어는 광고가 재생될 때 사용자가 오디오 트랙을 변경하도록 허용하지 않아야 합니다.
>


에서 두 가지 유형의 규칙을 지정할 수 있습니다. [!DNL AdobeTVSDKConfig.json]: *우선 순위* 규칙 및 *정규화* 규칙.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

광고 규칙은 JSON 파일을 사용하여 지정됩니다. JSON 파일의 형식은 두 TVSDK 버전에서 동일하게 유지됩니다. 그러나 TVSDK v3.0에서 광고 규칙 JSON 파일은 HTTP URL을 통해 액세스할 수 있는 위치에서 호스팅되어야 합니다. 응용 프로그램에서 AuditudeSettings의 인스턴스를 사용할 수 있습니다.

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
