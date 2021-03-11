---
description: 로컬로 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.
title: 로컬에서 생성된 CRL 사용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 로컬로 생성된 CRL {#consuming-locally-generated-crls} 사용

로컬로 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.

다음 API는 목록이 무단 변경되었는지, 목록이 올바른 라이센스 서버에서 서명되었는지 확인합니다.

* API에 [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html)을(를) 제공하기 전에 [RevocationList.verify](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate))을(를) 호출하여 서명을 확인합니다.

   자세한 내용은 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)를 참조하십시오.

* `PolicyUpdateList`를 모든 API에 제공하기 전에 [PolicyUpdateList.verify](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate))을(를) 호출하여 서명을 확인합니다.

   자세한 내용은 [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)를 참조하십시오.

