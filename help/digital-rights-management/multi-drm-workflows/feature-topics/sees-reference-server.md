---
description: 라이선스 및 정책 적용을 조정하는 한 가지 방법은 권한 부여 서버에 이러한 기능을 빌드하는 것입니다. Adobe은 자체 서버를 만드는 데 사용할 수 있는 SEE 참조 권한 부여 서버를 제공합니다.
title: 참조 서버 샘플 ExpressPlay 권한 부여 서버(SEE)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 참조 서버:샘플 ExpressPlay 자격 부여 서버(SEE) {#reference-server-sample-expressplay-entitlement-server-sees}

라이선스 및 정책 적용을 조정하는 한 가지 방법은 권한 부여 서버에 이러한 기능을 빌드하는 것입니다. Adobe은 자체 서버를 만드는 데 사용할 수 있는 SEE 참조 권한 부여 서버를 제공합니다.

참조 서버 SEES에서 ExpressPlay 권한 부여 서비스를 보여 주며 다음과 같은 2가지 서비스를 보여 줍니다.기본 시간 기반의 권한 부여 및 디바이스 바인딩 자격 부여

SEES는 두 개의 ExpressPlay Fairplay 서비스 위에 구축되어 있습니다.

1. Express 토큰 요청 서비스
1. 표현식 레코드 검색 서비스

ExpressPlay 토큰 요청에 대한 URL 형식은 제작 양식, 테스트 환경에 대해 각각 두 개의 양식을 사용합니다.

**프로덕션**:https://fp-gen<span></span>을 참조하십시오.{prod_domain}/hms/fp/token

**테스트**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay 레코드 검색을 위한 URL 형식은 제작 양식, 테스트 환경 양식,

**프로덕션**:https://api<span></span>을 참조하십시오.{prod_domain}/cmiapi/getrecord/

**테스트**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
