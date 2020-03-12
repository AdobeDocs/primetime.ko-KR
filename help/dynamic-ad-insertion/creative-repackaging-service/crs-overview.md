---
description: CRS(Creative Repackaging Service)를 통해 비HLS 광고 크리에이티브가 HLS 스트림에서 제대로 재생할 수 있습니다. 매니페스트 서버는 HLS가 아닌 광고가 발생하면 CRS를 호출합니다.
seo-description: CRS(Creative Repackaging Service)를 통해 비HLS 광고 크리에이티브가 HLS 스트림에서 제대로 재생할 수 있습니다. 매니페스트 서버는 HLS가 아닌 광고가 발생하면 CRS를 호출합니다.
seo-title: CRS 개요
title: CRS 개요
uuid: 3ae75fa7-397f-47ba-8e3d-50543ca25458
translation-type: tm+mt
source-git-commit: 4788a8de8ba47d7f448967066e1bd0fb73fdb7a8

---


# CRS 개요 {#overview-of-crs}

CRS(Creative Repackaging Service)를 통해 비HLS 광고 크리에이티브가 HLS 스트림에서 제대로 재생할 수 있습니다. 매니페스트 서버는 HLS가 아닌 광고가 발생하면 CRS를 호출합니다.

>[!NOTE]
>
>기본적으로 CRS는 비활성화됩니다. 계정에 대해 CRS를 활성화하려면 Adobe 기술 계정 관리자에게 문의하십시오.
>
>TVSDK 앱에서 CRS 활성화에 대한 자세한 내용은 *플랫폼용 Programmer&#39;s Guide의 Enable CRS in TVSDK applications* 항목을 참조하십시오. 예를 들어 Android 3.4의 경우 TVSDK [애플리케이션에서 CRS 활성화를 참조하십시오](../../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-transcoding/android-3x-ad-transcoding.md)

CRS는 컨텐츠 스트림의 HLS(HTTP Live Streaming) 광고 크리에이티브를 준비하고 클라이언트측 광고 추적을 위해 ID3 패킷을 삽입합니다. 타사 광고 서버, 광고 네트워크 및 에이전시 서버에서 받은 MP4, FLV 및 WebM 파일을 HLS 포맷으로 트랜스코딩합니다.

Adobe Primetime 광고 삽입에 HLS가 아닌 광고 크리에이티브가 발생하면 재패키징을 위해 CRS로 전송되며, 이는 일반적으로 3분 이내에 발생합니다. CRS 파섹 이것을 **`just-in-time (JIT) repackaging`**&#x200B;부릅니다. 또한 광고 크리에이티브를 다시 패키징 API를 사용하기 전에 트랜스코딩할 [수 있습니다](../../dynamic-ad-insertion/creative-repackaging-service/api-repackage.md) . 이것을 *`asynchronous repackaging`*&#x200B;부릅니다.

또한 Adobe 기술 계정 관리자는 다른 비헤이비어가 애플리케이션에 더 적합한 경우 일부 CRS 기본 동작을 변경할 수 있습니다. 다음과 같습니다.

* 광고 크리에이티브 포맷의 우선 순위

   VAST/VMAP 응답의 `MediaFiles` 섹션에는 다양한 `MediaFile` 유형의 크리에이티브가 포함될 수 있습니다. 기본적으로 매니페스트 서버는 고정된 우선 순위 집합( `application/x-mpegURL`, `application/vnd.apple.mpegURL`, `video/mp4``video/x-flv,video/webm`,)에 따라 하나를 선택합니다. Adobe는 계정 우선 순위를 변경할 수 있습니다.
* 광고 타겟 지속 시간.

   매니페스트 서버는 콘텐트 재생 목록에서 대상 광고 기간을 감지하여 이를 CRS로 전송합니다. Adobe는 CRS가 항상 계정에 대해 지정한 고정 기간을 사용하도록 이 동작을 변경할 수 있습니다.
