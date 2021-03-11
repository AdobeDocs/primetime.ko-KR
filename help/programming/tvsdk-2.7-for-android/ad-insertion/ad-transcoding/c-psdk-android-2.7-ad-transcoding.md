---
description: 비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.
title: Adobe CRS(Creative Repackaging Service)를 사용하여 호환되지 않는 광고를 재패키징합니다.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Adobe CRS(Creative Repackaging Service) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}을(를) 사용하여 호환되지 않는 광고를 재패키징합니다.

비디오 형식이 HLS와 호환되지 않으므로 일부 타사 광고(또는 크리에이티브)를 HLS(HTTP Live Streaming) 컨텐츠 스트림에 연결할 수 없습니다. Primetime 광고 삽입 및 TV SDK는 호환되지 않는 광고를 호환되는 M3U8 비디오에 선택적으로 재패키징할 수 있습니다.

광고 대행사 광고 서버, 인벤토리 파트너 또는 광고 네트워크 등 다양한 제3자로부터 제공되는 광고는 종종 점진적 다운로드 MP4 형식과 같은 호환되지 않는 형식으로 제공됩니다.

TVSDK에서 처음에 호환되지 않는 광고가 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 재패키징하여 호환되는 포맷으로 재패키징할 것을 요청합니다. CRS는 광고의 다양한 비트 전송률 M3U8 변환을 생성하고 이러한 변환을 Primetime CDN(Content Delivery Network)에 저장하려고 합니다. 다음 번에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면, 플레이어는 CDN의 HLS 호환 M3U8 버전을 사용합니다.

이 선택적 CRS 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>CRS 버전 3.0 이전 버전 고객의 경우, CRS 버전 3.1부터 다음과 같은 변경 사항이 보안과 성능을 모두 개선했습니다.
>
>* 다시 패키지되는 콘텐트에서 `https:`을(를) 사용하는 경우 CRS 3.1은 `https:`으로 계속됩니다. 따라서 일부 플레이어에서 안전하지 않은 컨텐츠를 제공할 가능성이 줄어듭니다.
   >
   >
* CRS 3.1은 네트워크 호출을 크게 최소화하여 비디오 시작 시간을 향상시킵니다.

>



CRS에 대한 자세한 내용은 [CRS(Creative Packaging Service)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf)을 참조하십시오.

## TVSDK 응용 프로그램에서 CRS 사용{#enable-crs-in-tvsdk-applications}

TVSDK 애플리케이션에서 CRS를 활성화하려면 Auditude 설정에서 다음 정보를 설정해야 합니다.

1. `AuditudeSettings`에서 CRS를 활성화합니다.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
