---
title: CDN 통합
description: CDN 통합
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# CDN {#integrating-cdn} 통합

Primetime Ad Insertion은 비디오가 직접 아닌 클라이언트 애플리케이션과 매니페스트 간의 프록시 역할을 합니다. 원하는 CDN에 콘텐츠를 배포하고 Bootstrap API를 사용하여 URL을 Primetime Ad Insertion에 전달합니다.<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## 지원되는 CDN 토큰화 구성표 {#cdn-tokenization-schemes}

CDN은 종종 조각 인증에 대해 다른 토큰화 체계를 가집니다. Primetime Ad Insertion은 다음을 비롯한 주요 CDN 네트워크를 기본적으로 지원합니다.

* Akamai
* Limelight
* Centrurylink / Level3
* 지원되는 CDN의 전체 목록은 Primetime 지원 담당자에게 문의하십시오.

`pttoken` 매개 변수에 대한 자세한 내용은 [Bootstrap API 매개 변수 설명](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)을 참조하십시오.

## 컨텐츠 CDN {#configure-ad-deliver-from-cdn}에서 전달할 광고 구성

동일한 CDN에서 광고 및 컨텐트를 전달하여 컨텐츠 관련성을 유지하고, 광고 차단 기능을 우회하거나, 클라이언트 애플리케이션에서 필요한 연결 수를 최적화할 수 있습니다. Primetime Ad Insertion은 콘텐츠 CDN에 조각을 매핑하기 위한 조각 다시 쓰기 규칙을 지원합니다.

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## 다중 CDN 기능 {#enable-multi-cdn-fetures}

다중 CDN 기능을 활성화하려면 Primetime 지원 담당자에게 문의하십시오.
