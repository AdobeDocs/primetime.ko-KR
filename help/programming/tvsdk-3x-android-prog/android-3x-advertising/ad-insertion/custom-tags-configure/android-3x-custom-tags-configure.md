---
description: 미디어 스트림에는 재생 목록/매니페스트 파일에서 태그 형식의 추가 메타데이터가 포함될 수 있으며 이 파일은 광고 배치를 나타냅니다. 사용자 지정 태그 이름을 지정하고 특정 태그가 매니페스트 파일에 나타날 때 알림을 받을 수 있습니다.
title: 사용자 지정 태그
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 개요 {#custom-tags-overview}

미디어 스트림에는 재생 목록/매니페스트 파일에서 태그 형식의 추가 메타데이터가 포함될 수 있으며 이 파일은 광고 배치를 나타냅니다. 사용자 지정 태그 이름을 지정하고 특정 태그가 매니페스트 파일에 나타날 때 알림을 받을 수 있습니다.

## HLS 컨텐트 태그 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>TVSDK는 Flash 또는 MSE가 아닌 비디오 태그를 사용하여 HLS 컨텐츠를 재생하기 때문에 Apple 컴퓨터의 Safari에서는 이 기능을 사용할 수 없습니다.

TVSDK는 특정 `#EXT` 광고 태그에 대한 기본 지원을 제공합니다. 애플리케이션에서 사용자 정의 태그를 사용하여 광고 워크플로우를 향상시키거나 일시 중단 시나리오를 지원할 수 있습니다. 고급 워크플로우를 지원하기 위해 TVSDK를 사용하여 매니페스트에서 추가 태그를 지정하고 가입할 수 있습니다. 이러한 태그가 매니페스트 파일에 나타날 때 알림을 받을 수 있습니다.

>[!TIP]
>
>VOD 및 라이브/리니어 스트림에 대해 사용자 정의 태그를 구독할 수 있습니다.

>[!NOTE]
>
>**제한 사항**
>
>Flash 폴백을 사용하지 않고 Safari에서 비디오 태그를 사용하여 HLS를 재생하면 Safari에서 이 기능을 사용할 수 없습니다.

## 사용자 지정 HLS 태그 사용 {#section_AD032318AEF5418393D2B1DF36B0BABB}

사용자 지정된 VOD 자산의 예는 다음과 같습니다.

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

애플리케이션은 다음 시나리오를 설정할 수 있습니다.

* `#EXT-X-ASSET` 태그 또는 가입한 다른 사용자 지정 태그 이름 세트가 파일에 있을 때의 알림.
* 스트림에서 `#EXT-X-AD` 태그 또는 다른 사용자 지정 태그 이름이 발견되면 광고를 삽입합니다.

다음 태그를 사용자 지정 태그로 가입할 수 있습니다.

* `EXT-PROGRAM-DATE-TIME`
* `EXT-X-START`
* `EXT-X-AD`
* `EXT-X-CUE`
* `EXT-X-ENDLIST`

매니페스트 파일을 구문 분석하는 동안 `TimedMetadata` 이벤트를 통해 알림을 받게 됩니다.

이미 구독한 광고 태그(예: `EXT-X-CUE`)가 있습니다. 이러한 광고 태그는 기본 기회 생성기도 사용합니다. `adTags` 속성을 설정하여 기본 기회 생성기에서 사용할 광고 태그를 지정할 수 있습니다.