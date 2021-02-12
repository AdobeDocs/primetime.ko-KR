---
title: CDN 통합
description: CDN 통합
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# CDN {#integrating-cdn} 통합

Primetime Ad Insertion은 비디오 내용이 아닌 클라이언트 애플리케이션과 매니페스트 간의 프록시 역할을 합니다. 원하는 CDN에 컨텐츠를 배포하고 Bootstrap API를 사용하여 URL을 Primetime Ad Insertion에 전달합니다. 통합 세부 사항은 [지원되는 CDN](/help/primetime-ad-insertion/technical-reference/supported-cdns.md)을 참조하십시오.

## 지원되는 CDN 토큰화 구성표 {#cdn-tokenization-schemes}

CDN은 종종 조각 인증에 대해 다른 토큰화 체계를 가집니다. Primetime Ad Insertion은 다음을 비롯한 주요 CDN 네트워크를 기본적으로 지원합니다.

* Akamai
* Limelight
* Centrurylink / Level3
* 지원되는 CDN의 전체 목록은 Primetime 지원 담당자에게 문의하십시오.

`pttoken` 매개 변수에 대한 자세한 내용은 [Bootstrap API 매개 변수 설명](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description)을 참조하십시오.

## 컨텐츠 CDN {#configure-ad-deliver-from-cdn}에서 전달할 광고를 구성합니다.

동일한 CDN의 광고 및 컨텐트를 전달하여 컨텐트 친화성을 유지하고, 광고 차단을 건너뛰고, 클라이언트 응용 프로그램으로부터 필요한 연결 수를 최적화할 수 있습니다. Primetime Ad Insertion은 컨텐츠 CDN에 조각을 매핑하기 위해 조각 다시 쓰기 규칙을 지원합니다. 자세한 내용은 [매니페스트 다시 쓰기](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md)를 참조하십시오.

## CDN {#increase-startup-performance}을 사용하여 시작 성능 향상

자세한 내용은 [시작 최적화](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md)를 참조하십시오.

## 다중 CDN 기능 {#enable-multi-cdn-fetures}

다중 CDN 기능을 활성화하려면 Primetime 지원 담당자에게 문의하십시오.
