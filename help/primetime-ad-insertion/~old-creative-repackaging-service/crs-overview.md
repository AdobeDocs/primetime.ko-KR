---
description: CRS(Creative Repackaging Service)를 사용하면 HLS가 아닌 광고 크리에이티브가 HLS 스트림에서 제대로 재생될 수 있습니다. 매니페스트 서버는 HLS가 아닌 광고가 발생하면 CRS를 호출합니다.
title: CRS 개요
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# CRS 개요 {#overview-of-crs}

CRS(Creative Repackaging Service)를 사용하면 HLS가 아닌 광고 크리에이티브가 HLS 스트림에서 제대로 재생될 수 있습니다. 매니페스트 서버는 HLS가 아닌 광고가 발생하면 CRS를 호출합니다.

>[!NOTE]
>
>기본적으로 CRS는 비활성화되어 있습니다. 계정에 대해 CRS를 활성화하려면 Adobe 기술 계정 관리자에게 문의하십시오.
>
>TVSDK 앱 내에서 CRS를 활성화하는 방법에 대한 자세한 내용은 *TVSDK 애플리케이션에서 CRS 활성화* 플랫폼용 Programmer&#39;s Guide의 주제입니다. 예를 들어 Android 3.4의 경우 다음을 참조하십시오. [TVSDK 애플리케이션에서 CRS 활성화](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS는 컨텐츠 스트림에 대한 HTTP 라이브 스트리밍(HLS) 광고 크리에이티브를 준비하고 클라이언트측 광고 추적을 위해 ID3 패킷을 주입합니다. 타사 광고 서버, 광고 네트워크 및 에이전시 서버에서 받은 MP4, FLV 및 WebM 파일을 HLS 형식으로 코드 변환합니다.

Adobe Primetime 광고 삽입에서 비 HLS 광고 크리에이티브가 발생하면 재패키징하기 위해 CRS로 전송하며, 이 작업은 일반적으로 3분 이내에 수행됩니다. CRS는 향후 사용을 위해 트랜스코딩된 광고 크리에이티브를 CDN 서버로 전송합니다. 이 이름은 입니다. **`just-in-time (JIT) repackaging`**. 광고 크리에이티브가 필요하기 전에  [API 다시 패키징](../../primetime-ad-insertion/~old-creative-repackaging-service/api-repackage.md) . 이 이름은 입니다. *`asynchronous repackaging`*.

다른 동작이 애플리케이션에 더 적합한 경우 Adobe 기술 계정 관리자가 일부 CRS 기본 동작을 변경할 수도 있습니다. 이는 다음과 같습니다.

* 광고 크리에이티브 형식의 우선 순위입니다.

   다음 `MediaFiles` vast/VMAP 응답의 섹션에는 서로 다른 크리에이티브가 포함될 수 있습니다 `MediaFile` 유형. 기본적으로 매니페스트 서버는 고정된 우선순위 세트에 따라 하나를 선택합니다( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4`, `video/x-flv,video/webm`). Adobe은 계정의 우선 순위를 변경할 수 있습니다.
* 광고 대상 기간.

   매니페스트 서버는 콘텐츠 재생 목록에서 타겟 광고 기간을 감지하고 CRS로 전송합니다. Adobe은 CRS가 항상 계정에 대해 지정하는 고정 기간을 사용하도록 이 동작을 변경할 수 있습니다.
