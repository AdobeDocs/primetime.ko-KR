---
title: 로컬에서 생성된 CRL 사용
description: 로컬에서 생성된 CRL 사용
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 로컬에서 생성된 CRL 사용{#consume-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe 액세스 API를 사용하여 서명을 확인하십시오. API는 목록이 변경되지 않았으며 올바른 라이선스 서버에서 서명했는지 확인합니다.

* 호출 `RevocationList.verifySignature` API에 RevocationList를 제공하기 전에 서명을 확인합니다.

  자세한 내용은 `RevocationListFactory` 다음에서 *Adobe 액세스 API 참조*.

* 호출 `PolicyUpdateList.verifySignature`을(를) 제공하기 전에 서명을 확인하려면 `PolicyUpdateList` 모든 API에

  자세한 내용은 `PolicyUpdateList` 다음에서 *Adobe 액세스 API 참조*.
