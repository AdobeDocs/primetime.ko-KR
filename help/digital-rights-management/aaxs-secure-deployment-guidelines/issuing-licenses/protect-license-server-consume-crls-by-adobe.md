---
seo-title: Adobe에 의해 게시된 CRL 사용
title: Adobe에 의해 게시된 CRL 사용
uuid: 43f65edb-0c96-46ab-b787-1b5f0b4b093e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Adobe{#consume-crls-published-by-adobe}에 의해 게시된 CRL 사용

SDK는 Adobe에서 게시한 CRL을 정기적으로 다운로드합니다. 이러한 파일에 대한 액세스를 차단하거나 이러한 CRL의 적용을 차단하지 마십시오.

SDK에는 Adobe CRL을 검색할 때 오류를 무시하는 구성 옵션이 있습니다. 이 옵션은 개발 환경에서만 사용할 수 있습니다. 프로덕션 환경에서 라이센스 서버는 Adobe에서 CRL을 검색할 수 있어야 합니다. 유효한 CRL을 가져오지 못한 경우 오류가 발생합니다.
