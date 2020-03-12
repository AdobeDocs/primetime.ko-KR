---
description: TVSDK 구성 파일(AdobeTVSDK 구성 파일)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브를 위한 소스 URL 변형 규칙을 정의할 수도 있습니다.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: TVSDK 구성 파일(AdobeTVSDK 구성 파일)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브를 위한 소스 URL 변형 규칙을 정의할 수도 있습니다.
seo-title: 광고 크리에이티브 선택 규칙 업데이트
title: 광고 크리에이티브 선택 규칙 업데이트
uuid: 77d8e186-01b5-4d62-8686-28f431d18876
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# 개요 {#update-ad-creative-selection-rules-overview}

TVSDK 구성 파일(AdobeTVSDK 구성 파일)을 사용하여 VAST/VMAP 응답에서 광고 크리에이티브 선택에 대한 우선 순위를 업데이트할 수 있습니다. 이 구성 파일을 사용하여 광고 크리에이티브를 위한 소스 URL 변형 규칙을 정의할 수도 있습니다.

비디오 플레이어가 광고 서버에 요청을 하면 VAST 파섹/VMAP 응답에는 일반적으로 여러 광고 크리에이티브( `MediaFile` 요소)가 포함되며, 각 응답에는 다른 컨테이너-코덱의 버전에 대한 URL이 제공됩니다. 경우에 따라 VAST 파섹/VMAP 응답의 광고 크리에이티브는 각각 광고에 대해 다른 비트 전송률을 제공합니다. 이러한 광고 크리에이티브의 자체 우선 순위 및 변형 규칙을 지정하려면 [!DNL AdobeTVSDKConfig.json] 구성 파일에서 지정할 수 있습니다.

>[!IMPORTANT]
>
>* TVSDK 구성 파일의 이름을 변경하지 마십시오. 이름은 [!DNL AdobeTVSDKConfig.json]남아 있어야 합니다.
>* 이 파일은 프로젝트의 [!DNL assets/] 폴더에 저장해야 합니다.
>* 광고 재생 시 오디오 트랙을 변경해도 오디오 트랙은 변경되지 않습니다. 플레이어는 사용자가 광고를 재생할 때 오디오 트랙을 변경할 수 없도록 허용해서는 안 됩니다.
>



다음 두 가지 유형의 규칙을 지정할 수 [!DNL AdobeTVSDKConfig.json]있습니다.우선 *순위* 규칙 및 *표준화* 규칙.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

광고 규칙은 JSON 파일을 사용하여 지정됩니다. JSON 파일의 형식은 두 버전의 TVSDK에서 동일하게 유지됩니다. 그러나 TVSDK v3.0에서는 HTTP URL을 통해 액세스할 수 있는 위치에 광고 규칙 JSON 파일을 호스팅해야 합니다. 응용 프로그램은 AuditudeSettings의 인스턴스를 사용할 수 있습니다.

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
