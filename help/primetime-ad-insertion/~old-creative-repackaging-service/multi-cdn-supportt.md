---
description: 다중 CDN을 사용하면 하나 이상의 CDN 위치 설정을 통해 코드 변환된 광고를 제공할 수 있습니다.
seo-description: 다중 CDN을 사용하면 하나 이상의 CDN 위치 설정을 통해 코드 변환된 광고를 제공할 수 있습니다.
seo-title: 다중 CDN 지원
title: 다중 CDN 지원
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 다중 CDN 지원 {#multi-cdn-support}

다중 CDN을 사용하면 하나 이상의 CDN 위치 설정을 통해 코드 변환된 광고를 제공할 수 있습니다.

기본적으로 모든 코드 변환된 에셋은 Adobe 소유 Akamai CDN에 호스팅됩니다. 그러나 CRS가 코드 변환된 에셋을 호스팅할 고유한 CDN 위치를 0개 이상 추가로 선택할 수 있습니다. 이 경우 코드 변환된 에셋과 콘텐츠를 동일한 CDN에서 제공할 수 있습니다.

매니페스트 서버가 코드 변환된 요청을 조회하면 쿼리 매개 변수가 많은 부트스트랩 URL을 사용합니다. 다중 CDN 환경을 설정한 경우 부트스트랩 URL에도 `ptcdn` 매개 변수가 포함되어야 합니다. 매니페스트 서버는 이 매개 변수를 사용하여 트랜스코딩된 광고 버전을 가져올 CDN 서버를 식별합니다.

다음 Primetime 솔루션에도 멀티 CDN 지원을 사용할 수 있습니다.

1. Android용 TVSDK
1. 데스크탑 HLS용 TVSDK
1. iOS용 TVSDK

## CDN 지원 활성화 {#section_1BA344F2300B49F291865A7461EDFEAE}

기본적으로 CRS는 모든 고객에 대해 비활성화됩니다.

트랜스코딩된 광고 자산을 호스팅하기 위해 다른 CDN을 사용하도록 CRS 계정을 구성하려면 Adobe 기술 계정 관리자에게 문의하십시오.CRS가 트랜스코딩된 광고 자산을 CDN에 업로드하는 데 필요한 다음 정보를 제공해야 합니다

1. CDN URL
1. 인증 세부 정보
1. 출력 URL 형식

또한 Adobe 기술 계정 관리자는 이 CDN에 대한 별칭을 제공합니다.Bootstrap URL에 있는 `ptcdn` 매개 변수의 값으로 이 별칭을 전달해야 합니다.

Adobe 지원을 통해 CRS 끝에 여러 개의 CDN을 구성할 수 있습니다. 하지만 매니페스트 서버를 통해 연결할 광고 자산을 선택하는 데 사용되는 CDN은 Bootstrap URL에서 `ptcdn` 매개 변수의 값으로 전달되는 CDN이어야 합니다.