---
description: 일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.
title: CRS(Adobe 크리에이티브 리패키징 서비스)를 사용하여 호환되지 않는 광고 리패키지
exl-id: b6fb2846-64b6-4db7-a6a9-f85365780775
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# CRS(Adobe 크리에이티브 리패키징 서비스)를 사용하여 호환되지 않는 광고 리패키지 {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

일부 타사 광고(또는 광고 크리에이티브)는 비디오 형식이 HLS와 호환되지 않으므로 HTTP 라이브 스트리밍(HLS) 콘텐츠 스트림에 결합할 수 없습니다. Primetime 광고 삽입 및 TVSDK는 선택적으로 호환되지 않는 광고를 호환되는 M3U8 비디오로 다시 패키징하려고 시도할 수 있습니다.

에이전시 광고 서버, 인벤토리 파트너 또는 광고 네트워크와 같은 다양한 타사에서 제공하는 광고는 점진적 다운로드 MP4 포맷과 같이 호환되지 않는 포맷으로 제공되는 경우가 많습니다.

TVSDK에 호환되지 않는 광고가 처음 발생하면 플레이어는 광고를 무시하고 Primetime 광고 삽입 백 엔드의 일부인 CRS(Creative Repackaging Service)에 광고를 호환되는 형식으로 다시 패키징하라는 요청을 보냅니다. CRS는 광고의 여러 비트 전송률 M3U8 렌디션을 생성하고 이러한 렌디션을 Primetime CDN(Content Delivery Network)에 저장합니다. 다음에 TVSDK가 해당 광고를 가리키는 광고 응답을 받으면 플레이어는 CDN에서 HLS 호환 M3U8 버전을 사용합니다.

이 선택적 CRS 기능을 활성화하려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>CRS 버전 3.0(및 이전 버전) 고객의 경우 CRS 버전 3.1부터 다음과 같은 변경 사항이 보안과 성능을 모두 개선했습니다.
>
>* CRS 3.1은 `https:` 다시 패키지하는 콘텐츠가 `https:`. 이렇게 하면 일부 플레이어가 안전하지 않은 콘텐츠를 표시할 가능성이 줄어듭니다.
>
>* CRS 3.1은 네트워크 호출을 크게 최소화하여 비디오 시작 시간을 향상시킵니다.
>


CRS에 대한 자세한 내용은 [CRS(Creative Packaging Service)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## TVSDK 애플리케이션에서 CRS 활성화{#enable-crs-in-tvsdk-applications}

TVSDK 애플리케이션에서 CRS를 활성화하려면 감사 설정에서 다음 정보를 설정해야 합니다.

1. 에서 CRS 활성화 `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
