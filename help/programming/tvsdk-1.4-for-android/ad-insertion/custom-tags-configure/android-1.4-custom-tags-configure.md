---
description: 미디어 스트림은 재생 목록/매니페스트 파일의 태그 형태로 추가 메타데이터를 전달할 수 있으며, 이 파일은 광고 배치를 나타냅니다. 사용자 지정 태그 이름을 지정하고 매니페스트 파일에 특정 태그가 나타나면 알림을 받을 수 있습니다.
title: 사용자 정의 태그
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 개요 {#custom-tags-overview}

미디어 스트림은 재생 목록/매니페스트 파일의 태그 형태로 추가 메타데이터를 전달할 수 있으며, 이 파일은 광고 배치를 나타냅니다. 사용자 지정 태그 이름을 지정하고 매니페스트 파일에 특정 태그가 나타나면 알림을 받을 수 있습니다.

## HLS 콘텐츠 태그 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>TVSDK는 HLS 콘텐츠를 재생하기 위해 Flash 또는 MSE가 아닌 비디오 태그를 사용하기 때문에 Apple 컴퓨터의 Safari에는 이 기능을 사용할 수 없습니다.

TVSDK는 특정 #EXT 광고 태그에 대한 기본 지원을 제공합니다. 애플리케이션은 사용자 정의 태그를 사용하여 광고 워크플로우를 개선하거나 일시 중단 시나리오를 지원할 수 있습니다. 고급 워크플로를 지원하기 위해 TVSDK를 사용하여 매니페스트에서 추가 태그를 지정하고 구독할 수 있습니다. 이러한 태그가 매니페스트 파일에 나타나면 알림을 받을 수 있습니다.

>[!TIP]
>
>VOD 및 라이브/선형 스트림에 대한 사용자 지정 태그를 구독할 수 있습니다.

>[!NOTE]
>
>**제한 사항**
>
>를 사용하여 HLS를 재생할 때 `Video` 태그는 Safari에서 제공되고, Flash 폴백을 사용하지 않는 경우에는 Safari에서 이 기능을 사용할 수 없습니다.

## 사용자 지정 HLS 태그 사용 {#section_AD032318AEF5418393D2B1DF36B0BABB}

다음은 사용자 지정된 VOD 에셋의 예입니다.

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

* 다음의 경우에 대한 알림 `#EXT-X-ASSET` 태그 또는 구독한 기타 사용자 지정 태그 이름 세트가 파일에 있습니다.
* 다음 경우에 광고 삽입 `#EXT-X-AD` 태그나 다른 모든 사용자 지정 태그 이름은 스트림에서 찾을 수 있습니다.

다음 태그를 사용자 지정 태그로 구독할 수 있습니다. `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. 다음 알림을 받았습니다. `TimedMetadata` 매니페스트 파일을 구문 분석하는 동안 이벤트가 발생했습니다.

다음과 같은 몇 가지 광고 태그가 있습니다. `EXT-X-CUE`을 추가하여 이미 구독 중입니다. 이러한 광고 태그는 기본 영업 기회 생성기에서도 사용됩니다. 기본 영업 기회 생성기가 사용하는 광고 태그를 지정할 수 있습니다. `adTags` 속성.
