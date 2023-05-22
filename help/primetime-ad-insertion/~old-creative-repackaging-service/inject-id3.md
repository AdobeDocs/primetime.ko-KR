---
description: CRS는 클라이언트측 광고 추적을 용이하게 하기 위해 ID3 시간 메타데이터를 HLS 포맷 광고 크리에이티브에 삽입할 수 있습니다.
title: CRS를 사용하여 ID3 시간 메타데이터 태그 주입
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# CRS를 사용하여 ID3 시간 메타데이터 태그 주입 {#using-crs-to-inject-id-timed-metadata-tags}

CRS는 클라이언트측 광고 추적을 용이하게 하기 위해 ID3 시간 메타데이터를 HLS 포맷 광고 크리에이티브에 삽입할 수 있습니다.

클라이언트 플레이어는 ID3 메타데이터를 읽어 프레임 정확한 광고 추적을 가능하게 합니다.

>[!NOTE]
>
>ID3 시간 메타데이터 삽입은 iOS의 Safari에서만 작동합니다.

## ID3 삽입에 대한 CRS 워크플로 {#workflow-for-crs-for-id3-injection}

ID3 삽입에 대한 워크플로우는 과 동일합니다 [JIT 다시 패키징을 위한 자세한 워크플로우입니다.](../~old-creative-repackaging-service/jit-repackage.md) 매니페스트 서버가 `ptplayer=ios-mobileweb` 매개 변수를 사용하면 CDN 서버에 업로드하기 전에 CRS에 ID3 패킷을 트랜스코딩된 광고 크리에이티브에 삽입하도록 합니다.

>[!NOTE]
>
>다중 CDN 설정에서 매니페스트 서버는 `ptcdn` 광고 크리에이티브를 업로드할 CDN 서버를 식별하기 위한 부트스트랩 URL의 매개 변수입니다.