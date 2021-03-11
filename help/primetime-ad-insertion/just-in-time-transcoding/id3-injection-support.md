---
description: 적시 트랜스코딩은 ID3 시간 메타데이터를 광고 크리에이티브에 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.
title: ID3 시간 지정 메타데이터 태그를 삽입하는 데 적시 트랜스코딩 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 적시 트랜스코딩을 사용하여 ID3 시간 지정 메타데이터 태그 {#using-crs-to-inject-id-timed-metadata-tags} 삽입

CRS는 ID3 시간 메타데이터를 광고 크리에이티브에 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.

클라이언트 플레이어는 ID3 메타데이터를 읽고 프레임 정확성 광고 추적을 활성화합니다.

>[!NOTE]
>
>ID3 시간 메타데이터 삽입 기능은 Safari/iOS에만 사용됩니다.

## ID3 주입 CRS 작업 과정 {#workflow-for-crs-for-id3-injection}

Primetime Ad Insertion이 `ptplayer=ios-mobileweb` 매개 변수를 받는 경우 해당 광고 저장소 CDN에 업로드하기 전에 변환된 광고 크리에이티브에 ID3 패킷을 주입합니다.
