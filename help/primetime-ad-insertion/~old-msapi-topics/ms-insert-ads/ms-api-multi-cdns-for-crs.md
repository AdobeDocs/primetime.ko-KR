---
description: 기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Delivery Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 에셋을 배포할 수 있습니다.
title: CRS 광고 게재에 대한 여러 CDN 지원
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# CRS 광고 게재에 대한 여러 CDN 지원 {#multiple-cdn-support-for-crs-ad-delivery}

기본 CRS(Creative Repackaging Service) 시나리오는 하나의 CDN(Content Delivery Network)을 사용하는 것이지만, 두 개 이상의 CDN에 CRS 에셋을 배포할 수 있습니다.

## 요구 사항

다음과 같은 이유로 여러 CDN을 사용할 수 있습니다.

* 대규모 보기 이벤트에 대한 확장 요구 사항
* CRS 에셋의 CDN 소스와 기본 컨텐츠의 CDN 소스를 일치시키기 위한 요구 사항입니다.
* CRS 기본 CDN(Akamai)과 다른 CDN을 사용하기 위한 요구 사항입니다.

매니페스트 서버에서 트랜스코딩된 요청을 조회하면 많은 쿼리 매개 변수가 포함된 부트스트랩 URL을 사용합니다. 다중 CDN 환경을 설정한 경우 부트스트랩 URL에도 `ptcdn` 매개 변수. 매니페스트 서버는 이 매개 변수를 사용하여 트랜스코딩된 광고 버전을 가져올 CDN 서버를 식별합니다.

자세한 내용은 [다중 CDN 지원](../../~old-creative-repackaging-service/multi-cdn-supportt.md) CRS 설명서.
