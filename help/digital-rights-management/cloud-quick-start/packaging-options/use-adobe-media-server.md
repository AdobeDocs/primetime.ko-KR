---
title: Adobe Medium 서버 사용
description: Adobe Medium 서버 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Adobe Medium 서버 {#use-adobe-media-server} 사용

일부 고객은 이미 Adobe Medium Server를 사용하고 있으며 해당 컨텐츠 전달 모델을 유지 관리하려고 할 수 있습니다. 이 경우 필요한 Primetime Cloud DRM 관련 데이터를 이 키트에 포함된 구성 파일 중 하나에서 수집하여 AMS에 대한 JIT(Just In Time) XML 구성을 채울 수 있습니다.

예:

```xml
<?xml version="1.0"?>
<Application>
  <HDS>
    <HLS>
      <Encryption enabled="true" protection-scheme="AdobeAccessV4">
        <AdobeAccessV4>
          <ContentID>SampleVideo</ContentID>
          <CommonKeyPath>common-key.bin</CommonKeyPath>
          <LicenseServerURL>
            https://access.adobeprimetime.com/flashaccessserver/axs_prod
          </LicenseServerURL>
          <KeyServerURL>
            https://access.adobeprimetime.com:443/faxsks/axs_prod/key
          </KeyServerURL>
          <TransportCertPath>cert/Cloud DRM-transport.cer</TransportCertPath>
          <LicenseServerCertPath>cert/Cloud DRM-license.cer</LicenseServerCertPath>
          <PackagerCredentialPath>cert-from-adobe.pfx</PackagerCredentialPath>
          <PackagerCredentialPwd>pass-for-cert-from-adobe</PackagerCredentialPwd>
          <PolicyPath>policy_ios_localkeyserver.pol</PolicyPath>
        </AdobeAccessV4>
      </Encryption>
    </HLS>
  </HDS>
</Application>
```

