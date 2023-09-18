---
description: 라이센싱 및 정책 시행을 조정하는 한 가지 방법은에서 권한 부여 서버에 이러한 기능을 구축하는 것입니다. Adobe은 고유한 서버를 빌드하기 위해 함께 사용할 수 있는 SEES 참조 권한 부여 서버를 제공합니다.
title: 참조 서버 샘플 ExpressPlay 권한 서버(SEES)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 참조 서버: 샘플 ExpressPlay 권한 서버(SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

라이센싱 및 정책 시행을 조정하는 한 가지 방법은에서 권한 부여 서버에 이러한 기능을 구축하는 것입니다. Adobe은 고유한 서버를 빌드하기 위해 함께 사용할 수 있는 SEES 참조 권한 부여 서버를 제공합니다.

참조 서버 SEES에서는 ExpressPlay 권한 부여 서비스를 보여 주며 기본 시간 기반 권한 부여와 장치 바인딩 권한 부여, 이렇게 두 가지 서비스가 표시됩니다.

SEES는 ExpressPlay 페어플레이 서비스 2개를 기반으로 구축되었습니다.

1. Expressplay 토큰 요청 서비스
1. Expressplay 레코드 검색 서비스

ExpressPlay 토큰 요청의 URL 형식은 프로덕션용 양식과 테스트 환경용 양식 두 개를 사용합니다.

**프로덕션**: ht<span></span>tps://fp-gen입니다.{prod_domain}/hms/fp/token

**테스트**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay 레코드 검색을 위한 URL 형식은 프로덕션용 양식과 테스트 환경용 양식 두 가지를 사용합니다.

**프로덕션**: ht<span></span>tps://api입니다.{prod_domain}/cmiapi/getrecord/

**테스트**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
