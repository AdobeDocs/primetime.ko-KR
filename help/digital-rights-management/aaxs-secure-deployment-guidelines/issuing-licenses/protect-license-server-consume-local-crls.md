---
title: 로컬에서 생성된 CRL 사용
description: 로컬에서 생성된 CRL 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 로컬로 생성된 CRL 사용{#consume-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe 액세스 API를 사용하여 서명을 확인합니다. API는 목록이 무단 변경되지 않았으며 올바른 라이센스 서버에서 서명되었는지 확인합니다.

* API에 RevocationList를 제공하기 전에 `RevocationList.verifySignature`을(를) 호출하여 서명을 확인합니다.

   자세한 내용은 *Adobe 액세스 API 참조*&#x200B;의 `RevocationListFactory`을(를) 참조하십시오.

* `PolicyUpdateList.verifySignature`을(를) 호출하여 모든 API에 `PolicyUpdateList`을(를) 제공하기 전에 서명을 확인합니다.

   자세한 내용은 *Adobe 액세스 API 참조*&#x200B;의 `PolicyUpdateList`을(를) 참조하십시오.

