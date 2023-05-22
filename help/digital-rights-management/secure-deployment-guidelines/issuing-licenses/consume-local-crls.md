---
description: 로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인하십시오.
title: 로컬에서 생성된 CRL 사용
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 로컬에서 생성된 CRL 사용 {#consuming-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인하십시오.

다음 API는 목록이 변경되지 않았으며 올바른 라이선스 서버에서 서명했는지 확인합니다.

* 호출 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 서명을제공하기 전에 확인하려면 [해지 목록](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 모든 API에

   자세한 내용은 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* 호출 [PolicyUpdateList.verifySign](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 을(를) 제공하기 전에 서명을 확인하려면 `PolicyUpdateList` 모든 API에

   자세한 내용은 [정책 업데이트 목록](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

