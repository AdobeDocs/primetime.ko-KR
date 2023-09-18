---
title: Adobe에 의해 게시된 CRL 사용
description: Adobe에 의해 게시된 CRL 사용
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Adobe에 의해 게시된 CRL 사용{#consume-crls-published-by-adobe}

SDK는 Adobe에서 게시한 CRL을 주기적으로 다운로드합니다. 이러한 파일에 대한 액세스를 차단하거나 이러한 CRL을 적용하지 마십시오.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있습니다. 이 옵션은 개발 환경에서만 사용할 수 있습니다. 프로덕션 환경에서는 라이선스 서버가 Adobe에서 CRL을 검색할 수 있어야 합니다. 유효한 CRL을 획득하지 못하면 오류가 발생합니다.
