---
description: 다중 CDN을 사용하면 하나 이상의 CDN 위치를 설정하여 트랜스코딩된 광고를 제공할 수 있습니다.
title: 다중 CDN 지원
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 다중 CDN 지원 {#multi-cdn-support}

다중 CDN을 사용하면 하나 이상의 CDN 위치를 설정하여 트랜스코딩된 광고를 제공할 수 있습니다.

기본적으로 모든 트랜스코딩된 자산은 Adobe 소유 Akamai CDN에서 호스팅됩니다. 그러나 CRS가 트랜스코딩된 에셋을 호스팅할 0개 이상의 추가 CDN 위치를 선택할 수 있습니다. 따라서 이 경우 트랜스코딩된 에셋 및 콘텐츠는 동일한 CDN에서 제공될 수 있습니다.

매니페스트 서버에서 트랜스코딩된 요청을 조회하면 많은 쿼리 매개 변수가 포함된 부트스트랩 URL을 사용합니다. 다중 CDN 환경을 설정한 경우 부트스트랩 URL에도 `ptcdn` parameter.manifest 서버는 이 매개 변수를 사용하여 코드 변환된 광고 버전을 가져올 CDN 서버를 식별합니다.

다중 CDN 지원은 다음 Primetime 솔루션에도 사용할 수 있습니다.

1. Android용 TVSDK
1. 데스크탑 HLS용 TVSDK
1. iOS용 TVSDK

## CDN 지원 활성화 {#section_1BA344F2300B49F291865A7461EDFEAE}

기본적으로 CRS는 모든 고객에 대해 비활성화되어 있습니다

Adobe 기술 계정 관리자에게 문의하여 다른 CDN을 사용하여 트랜스코딩된 광고 자산을 호스팅하도록 CRS 계정을 구성하십시오. CDN에 트랜스코딩된 광고 자산을 업로드하는 데 필요한 다음 정보를 제공해야 합니다

1. CDN URL
1. 인증 세부 정보
1. 출력 URL 형식

또한 Adobe 기술 계정 관리자가 이 CDN의 별명을 제공합니다. 이 별명을 의 값으로 전달해야 합니다. `ptcdn` Bootstrap URL의 매개 변수.

Adobe 지원을 통해 CRS 끝에 여러 CDN을 구성할 수 있습니다. 그러나 매니페스트 서버를 통해 연결할 광고 자산을 선택하는 데 사용되는 CDN은 의 값으로 전달되는 CDN이어야 합니다 `ptcdn` Bootstrap URL의 매개 변수.
