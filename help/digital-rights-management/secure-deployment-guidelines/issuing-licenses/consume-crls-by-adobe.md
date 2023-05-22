---
description: SDK는 Adobe에서 게시한 CRL을 주기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL을 적용할 수 없도록 해야 합니다.
title: Adobe에 의해 게시된 CRL 사용
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Adobe에 의해 게시된 CRL 사용{#consuming-crls-published-by-adobe}

SDK는 Adobe에서 게시한 CRL을 주기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL을 적용할 수 없도록 해야 합니다.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있으며 이 옵션은 개발 환경에서만 적용할 수 있습니다. 프로덕션 환경에서는 라이선스 서버가 Adobe에서 CRL을 검색해야 합니다. 라이선스 서버가 유효한 CRL을 가져올 수 없는 경우 오류가 발생했습니다.
