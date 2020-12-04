---
description: 일부 타사 광고(또는 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HLS(HTTP Live Streaming) 콘텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.
seo-description: 일부 타사 광고(또는 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HLS(HTTP Live Streaming) 콘텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.
seo-title: Adobe CRS(Creative Repackaging Service)를 사용하여 호환되지 않는 광고 재패키지
title: Adobe CRS(Creative Repackaging Service)를 사용하여 호환되지 않는 광고 재패키지
uuid: c3961628-39aa-444c-9c93-9f1e267d9cd4
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Adobe CRS(Creative Repackaging Service) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}을(를) 사용하여 호환되지 않는 광고를 재패키징합니다.

일부 타사 광고(또는 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HLS(HTTP Live Streaming) 콘텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오로 재패키징할 수도 있습니다.

광고 대행사 광고 서버, 재고 파트너 또는 광고 네트워크 등 다양한 서드 파티에서 제공하는 광고는 종종 점진적 다운로드 MP4 포맷과 같이 호환되지 않는 형식으로 제공됩니다.

TVSDK에서 호환되지 않는 광고가 처음 발견되면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 재패키징하여 호환 가능한 포맷으로 재패키징하도록 요청합니다. CRS는 광고의 다양한 비트 전송률 M3U8 변환을 생성하고 이러한 변환을 Primetime CDN(Content Delivery Network)에 저장합니다. 다음 번에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면, 플레이어는 CDN의 HLS 호환 M3U8 버전을 사용합니다.

이 선택적 CRS 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>CRS 버전 3.0 이전 버전 고객의 경우 CRS 버전 3.1부터 다음과 같은 변경 사항이 보안과 성능을 모두 개선했습니다.
>
>* 다시 패키지되는 컨텐츠가 `https:`을(를) 사용하는 경우 CRS 3.1은 `https:`으로 계속됩니다. 따라서 일부 플레이어에서 안전하지 않은 컨텐츠를 제공할 가능성이 줄어듭니다.
   >
   >
* CRS 3.1은 네트워크 호출을 크게 최소화하여 비디오 시작 시간을 향상시킵니다.

>



CRS에 대한 자세한 내용은 [CRS(Creative Packaging Service)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf)을 참조하십시오.

## TVSDK 응용 프로그램에서 CRS 활성화{#enable-crs-in-tvsdk-applications}

TVSDK 애플리케이션에서 CRS를 활성화하려면 Auditude 설정에서 다음 정보를 설정해야 합니다.

1. `AuditudeSettings`에서 CRS를 활성화합니다.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
