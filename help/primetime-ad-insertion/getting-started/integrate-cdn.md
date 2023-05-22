---
title: CDN 통합
description: CDN 통합
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# CDN 통합 {#integrating-cdn}

Primetime Ad Insertion은 비디오 청크 자체가 아니라 클라이언트 애플리케이션과 매니페스트 간의 프록시 역할을 합니다. 원하는 CDN에 콘텐츠를 배포하고 Bootstrap API를 사용하여 Primetime Ad Insertion에 URL을 전달합니다. 통합에 대한 자세한 내용은 [지원되는 CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## 지원되는 CDN 토큰화 스키마 {#cdn-tokenization-schemes}

CDN은 종종 조각 인증에 서로 다른 토큰화 체계를 갖습니다. Primetime Ad Insertion은 다음을 포함한 주요 CDN 네트워크를 기본적으로 지원합니다.

* Akamai
* 각광
* Centurylink / 레벨 3
* 지원되는 CDN의 전체 목록은 Primetime 지원 담당자에게 문의하십시오

에 대한 자세한 내용은 `pttoken` 매개 변수, 참조 [Bootstrap API 매개 변수 설명](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## 콘텐츠 CDN에서 게재할 광고 구성 {#configure-ad-deliver-from-cdn}

콘텐츠 친화성을 유지하고 광고 차단기를 우회하거나 클라이언트 애플리케이션에서 필요한 연결 수를 최적화하는 데 도움이 되도록 동일한 CDN에서 광고 및 콘텐츠를 게재할 수 있습니다. Primetime Ad Insertion은 조각을 컨텐츠 CDN에 매핑하는 조각 재작성 규칙을 지원합니다. 자세한 내용은 [매니페스트 재작성](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## CDN으로 시작 성능 향상 {#increase-startup-performance}

자세한 내용은 [시작 최적화](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## 다중 CDN 기능 {#enable-multi-cdn-fetures}

다중 CDN 기능을 활성화하려면 Primetime 지원 담당자에게 문의하십시오.
