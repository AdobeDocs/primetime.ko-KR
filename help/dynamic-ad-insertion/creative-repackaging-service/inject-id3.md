---
description: CRS는 ID3 시간 메타데이터를 HLS 포맷 및 크리에이티브를 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.
seo-description: CRS는 ID3 시간 메타데이터를 HLS 포맷 및 크리에이티브를 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.
seo-title: CRS를 사용하여 ID3 시간 지정 메타데이터 태그 삽입
title: CRS를 사용하여 ID3 시간 지정 메타데이터 태그 삽입
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# CRS를 사용하여 ID3 시간 지정 메타데이터 태그 {#using-crs-to-inject-id-timed-metadata-tags}

CRS는 ID3 시간 메타데이터를 HLS 포맷 및 크리에이티브를 삽입하여 클라이언트측 광고 추적을 용이하게 할 수 있습니다.

클라이언트 플레이어는 ID3 메타데이터를 읽고 프레임 정확한 광고 추적을 활성화합니다.

>[!NOTE]
>
>iOS의 Safari에서만 ID3 시간 메타데이터 삽입이 작동합니다.

## ID3 주입 CRS 작업 과정 {#workflow-for-crs-for-id3-injection}

ID3 삽입에 대한 워크플로우는 JIT 재패키징을 위한 자세한 워크플로우와 동일합니다.[](../creative-repackaging-service/jit-repackage.md) 매니페스트 서버가  `ptplayer=ios-mobileweb` 매개 변수를 받으면 CDN 서버에 업로드하기 전에 ID3 패킷을 트랜스코딩 광고 크리에이티브로 주입하도록 CRS에게 알립니다.

>[!NOTE]
>
>다중 CDN 설정에서 매니페스트 서버는 부트스트랩 URL의 `ptcdn` 매개 변수를 사용하여 광고 크리에이티브를 업로드할 CDN 서버를 식별합니다.