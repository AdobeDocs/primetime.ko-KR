---
description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 또한 이 구성 파일을 사용하여 광고 크리에이티브 전문가를 위한 소스 URL 변형 규칙을 정의할 수 있습니다.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 또한 이 구성 파일을 사용하여 광고 크리에이티브 전문가를 위한 소스 URL 변형 규칙을 정의할 수 있습니다.
seo-title: 광고 크리에이티브 선택 규칙 업데이트
title: 광고 크리에이티브 선택 규칙 업데이트
uuid: b7d316ef-323e-4769-83d9-036422ae1707
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 개요 {#update-ad-creative-selection-rules-overview}

TVSDK 구성 파일(AdobeTVSDKConfig.json)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 또한 이 구성 파일을 사용하여 광고 크리에이티브 전문가를 위한 소스 URL 변형 규칙을 정의할 수 있습니다.

비디오 플레이어가 광고 서버에 요청을 하면 VAST/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` 요소)가 포함되며, 각각은 다른 컨테이너-코덱의 버전에 URL을 제공합니다. 경우에 따라 VAST/VMAP 응답의 광고 크리에이티브는 각각 광고에 대해 다른 비트 전송률을 제공합니다. 이러한 광고 크리에이티브 전문가를 위한 자체 우선 순위 및 변형 규칙을 지정하려면 [!DNL AdobeTVSDKConfig.json] 구성 파일에서 지정할 수 있습니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 [!DNL AdobeTVSDKConfig.json]이어야 합니다.
>* 번들에 액세스할 수 있는 위치에 이 파일을 배치할 수 있습니다.

>



[!DNL AdobeTVSDKConfig.json]에서 두 가지 유형의 규칙을 지정할 수 있습니다.*우선 순위* 규칙 및 *정규화* 규칙

**[!UICONTROL Disabling Pre-Roll]**

프리롤 기능을 비활성화하려면 프리롤 호출을 하지 않도록 기본 기회 생성기를 변경해야 합니다. 기본적으로 TVSDK는 다음 기회 생성기를 사용합니다.

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

라이브 스트림에서 프리롤 기능을 비활성화하려면 SpliceOutOpportunityGenerator만 포함하도록 변경해야 합니다.

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
