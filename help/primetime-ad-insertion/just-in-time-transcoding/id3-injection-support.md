---
description: Just-in-time-transcoding은 ID3 시간 메타데이터를 광고 크리에이티브에 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.
title: Just-in-time-transcoding을 사용하여 ID3 시간 메타데이터 태그 주입
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Just-in-Time 코드 변환 기능을 사용하여 ID3 시간 메타데이터 태그 주입 {#using-crs-to-inject-id-timed-metadata-tags}

CRS는 클라이언트측 광고 추적을 용이하게 하기 위해 ID3 시간 메타데이터를 광고 크리에이티브에 삽입할 수 있습니다.

클라이언트 플레이어는 ID3 메타데이터를 읽어 프레임 정확한 광고 추적을 가능하게 합니다.

>[!NOTE]
>
>ID3 시간 메타데이터 삽입 함수는 Safari/iOS에 대해서만 수행됩니다.

## ID3 삽입에 대한 CRS 워크플로 {#workflow-for-crs-for-id3-injection}

Primetime Ad Insertion이 `ptplayer=ios-mobileweb` 매개 변수를 사용하면 적절한 광고 저장소 CDN에 업로드하기 전에 ID3 패킷을 트랜스코딩된 광고 크리에이티브에 주입하게 됩니다.
