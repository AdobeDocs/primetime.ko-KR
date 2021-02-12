---
description: 기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Delivery Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 자산을 배포할 수 있습니다.
seo-description: 기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Delivery Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 자산을 배포할 수 있습니다.
seo-title: CRS 광고 전달을 위한 다양한 CDN 지원
title: CRS 광고 전달을 위한 다양한 CDN 지원
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# CRS 광고 전달에 대한 여러 CDN 지원 {#multiple-cdn-support-for-crs-ad-delivery}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Delivery Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 자산을 배포할 수 있습니다.

## 요구 사항

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 대규모 보기 이벤트에 대해 크기 조절하기 위한 요구 사항
* CRS 자산의 CDN 소스를 기본 컨텐츠의 CDN 소스와 일치시키는 요구 사항입니다.
* CRS 기본 CDN(Akamai)과 다른 CDN을 사용하는 요구 사항입니다.

매니페스트 서버가 코드 변환된 요청을 조회하면 쿼리 매개 변수가 많은 부트스트랩 URL을 사용합니다. 다중 CDN 환경을 설정한 경우 부트스트랩 URL에도 `ptcdn` 매개 변수가 포함되어야 합니다. 매니페스트 서버는 이 매개 변수를 사용하여 트랜스코딩된 광고 버전을 가져올 CDN 서버를 식별합니다.

자세한 내용은 CRS 설명서의 [다중 CDN 지원](../../~old-creative-repackaging-service/multi-cdn-supportt.md)을 참조하십시오.
