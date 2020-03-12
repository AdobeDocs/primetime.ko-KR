---
description: 라이선스 및 정책 적용을 조정할 수 있는 한 가지 방법은 권한 부여 서버에 이러한 기능을 구축하는 것입니다. Adobe는 자체 서버를 만들기 위해 함께 작업할 수 있는 SEE 참조 권한 서버를 제공합니다.
seo-description: 라이선스 및 정책 적용을 조정할 수 있는 한 가지 방법은 권한 부여 서버에 이러한 기능을 구축하는 것입니다. Adobe는 자체 서버를 만들기 위해 함께 작업할 수 있는 SEE 참조 권한 서버를 제공합니다.
seo-title: 참조 서버 샘플 ExpressPlay 권한 부여 서버(SEE)
title: 참조 서버 샘플 ExpressPlay 권한 부여 서버(SEE)
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 참조 서버:샘플 ExpressPlay 권한 부여 서버(SEE) {#reference-server-sample-expressplay-entitlement-server-sees}

라이선스 및 정책 적용을 조정할 수 있는 한 가지 방법은 권한 부여 서버에 이러한 기능을 구축하는 것입니다. Adobe는 자체 서버를 만들기 위해 함께 작업할 수 있는 SEE 참조 권한 서버를 제공합니다.

참조 서버 SEES에서 ExpressPlay 권한 부여 서비스를 보여 주며, 다음 두 가지 서비스를 보여 줍니다.기본 시간 기반의 권한 부여 및 디바이스 바인딩 권한 부여

SEES는 두 개의 ExpressPlay Fairplay 서비스 위에 구축되어 있습니다.

1. Express 토큰 요청 서비스
1. Express 레코드 검색 서비스

ExpressPlay 토큰 요청에 대한 URL 형식은 제작 양식, 테스트 환경 양식,

**제작**:https://fp-gen<span></span>을 참조하십시오.{prod_domain}/hms/fp/token

**테스트**:<span></span>https://fp-gen.test.expressplay.com/hms/fp/token

ExpressPlay 레코드 검색을 위한 URL 포맷은 제작용, 테스트 환경에 적합한 두 개의 양식을 사용합니다.

**제작**:https://api<span></span>을 참조하십시오.{prod_domain}/cmiapi/getrecord/

**테스트**:<span></span>https://api.test.expressplay.com/cmiapi/getrecord/
