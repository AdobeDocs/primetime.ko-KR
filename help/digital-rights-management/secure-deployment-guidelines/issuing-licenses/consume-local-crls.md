---
description: 로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.
seo-description: 로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.
seo-title: 로컬에서 생성된 CRL 사용
title: 로컬에서 생성된 CRL 사용
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 로컬에서 생성된 CRL 사용 {#consuming-locally-generated-crls}

로컬에서 생성된 인증서 해지 목록(CRL) 및 정책 업데이트 목록을 사용하려면 Adobe Primetime DRM API를 사용하여 서명을 확인합니다.

다음 API는 목록이 무단 변경되었는지, 그리고 목록이 올바른 라이센스 서버에서 서명되었는지 확인합니다.

* RevocationList [.verifySignature를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 호출하여 [API에 RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 를 제공하기 전에 서명을확인합니다.

   자세한 내용은 RevocationListFactory를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* PolicyUpdateList [.verifySignature를](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 호출하여 `PolicyUpdateList` API에 대한 서명을제공합니다.

   자세한 내용은 PolicyUpdateList를 [참조하십시오](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

