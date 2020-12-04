---
description: SDK는 Adobe에 의해 게시되는 CRL을 정기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL의 적용이 차단되지 않도록 해야 합니다.
seo-description: SDK는 Adobe에 의해 게시되는 CRL을 정기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL의 적용이 차단되지 않도록 해야 합니다.
seo-title: Adobe에 의해 게시된 CRL 사용
title: Adobe에 의해 게시된 CRL 사용
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Adobe{#consuming-crls-published-by-adobe}에 의해 게시된 CRL 소비

SDK는 Adobe에 의해 게시되는 CRL을 정기적으로 다운로드합니다. 이러한 파일에 대한 액세스가 차단되거나 이러한 CRL의 적용이 차단되지 않도록 해야 합니다.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있으며, 개발 환경에서만 이 옵션을 적용할 수 있습니다. 프로덕션 환경에서 라이센스 서버는 Adobe에서 CRL을 검색해야 합니다. 라이센스 서버에서 유효한 CRL을 가져올 수 없는 경우 오류가 발생했습니다.
