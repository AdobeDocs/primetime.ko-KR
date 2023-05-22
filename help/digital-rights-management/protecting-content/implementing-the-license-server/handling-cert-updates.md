---
title: Adobe이 발급한 인증서가 만료되면 인증서 업데이트 처리
description: Adobe이 발급한 인증서가 만료되면 인증서 업데이트 처리
copied-description: true
exl-id: 9051a647-87ed-4df6-8bbc-bb5c112383ee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Adobe이 발급한 인증서가 만료되면 인증서 업데이트 처리{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Adobe에서 새 인증서를 받아야 할 수 있습니다. 예를 들어 평가 인증서가 만료되거나 평가에서 프로덕션 인증서로 전환할 때 프로덕션 인증서가 만료됩니다. 인증서가 만료되고 이전 인증서를 사용하는 콘텐츠를 다시 패키징하지 않으려는 경우 라이선스 서버가 이전 인증서와 새 인증서를 모두 인식하도록 할 수 있습니다.

새 인증서로 서버를 업데이트하려면 다음을 수행하십시오.

1. (선택 사항) 기존 DRM 정책 업데이트 목록 또는 해지 목록에 새 항목을 추가할 때 새 자격 증명으로 서명하고 이전 인증서를 사용하여 기존 파일의 서명을 확인해야 합니다.

   예를 들어 다음 명령줄을 사용하여 다른 자격 증명을 사용하여 서명된 기존 DRM 정책 업데이트 목록에 항목을 추가할 수 있습니다.

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (선택 사항) Java API를 사용하여 새 DRM 정책 업데이트 목록 또는 해지 목록으로 라이선스 서버를 업데이트합니다.

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   또는:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   참조 구현에서 사용하는 속성은 다음과 같습니다 `HandlerConfiguration.RevocationList` 및 `HandlerConfiguration.PolicyUpdateList`. 서명을 확인하는 데 사용되는 인증서도 업데이트해야 합니다. `RevocationList.verifySignature.X509Certificate`.

1. 새 인증서와 이전 인증서로 라이선스 서버를 업데이트합니다.

   이전 인증서를 사용하여 패키지된 콘텐츠를 사용하려면 라이선스 서버에서 이전 및 새 라이선스 서버 자격 증명과 전송 자격 증명에 액세스할 수 있는지 확인하십시오.

   라이센스 서버 자격 증명의 경우:

   * 현재 자격 증명이 (으)로 전달되었는지 확인합니다. `LicenseHandler` 생성자:

      * 참조 구현에서 `LicenseHandler.ServerCredential` 속성.
      * 보호된 스트리밍용 Adobe Primetime DRM 서버에서 현재 자격 증명은 `LicenseServerCredential` flashaccess-tenant.xml 파일의 요소입니다.
   * 현재 및 이전 자격 증명이 다음 대상에게 제공되는지 확인합니다. `AsymmetricKeyRetrieval`

      * 참조 구현에서 `LicenseHandler.ServerCredential` 및 `AsymmetricKeyRetrieval.ServerCredential. n` 속성.

      * Primetime DRM Server for Protected Streaming에서 이전 자격 증명은 의 첫 번째 자격 증명 뒤에 지정됩니다. `LicenseServerCredential` flashaccess-tenant.xml 파일의 요소입니다.
   전송 자격 증명:

   * 현재 자격 증명이 (으)로 전달되었는지 확인합니다. `HandlerConfiguration.setServerTransportCredential()` 방법:

      * 참조 구현에서 `HandlerConfiguration.ServerTransportCredential` 속성.
      * 보호된 스트리밍을 위한 Primetime DRM 서버에서 현재 자격 증명은 `TransportCredential` 의 요소 [!DNL flashaccess-tenant.xml] 파일.
   * 에 이전 자격 증명이 제공되는지 확인합니다. `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * 참조 구현에서 `HandlerConfiguration.AdditionalServerTransportCredential. n` 속성.
      * 보호된 스트리밍을 위한 Primetime DRM 서버에서는 의 첫 번째 자격 증명 뒤에 지정됩니다. `TransportCredential` flashaccess-tenant.xml 파일의 요소입니다.




1. 패키징 도구를 업데이트하여 현재 자격 증명으로 콘텐츠를 패키징하고 있는지 확인합니다. 최신 라이선스 서버 인증서, 전송 인증서 및 패키지 자격 증명을 패키징에 사용해야 합니다.
1. 다음과 같이 키 서버의 라이선스 서버 인증서를 업데이트합니다.

   * flashaccess-keyserver-tenant.xml에 이전 및 새 키 서버 자격 증명을 모두 포함하여 Adobe Primetime DRM 키 서버 테넌트 구성 파일의 자격 증명을 업데이트합니다.
   * 현재 인증서가 (으)로 전달되었는지 확인합니다. `HandlerConfiguration.setKeyServerCertificate()` 메서드를 사용합니다.

      * 참조 구현에서 `HandlerConfiguration.KeyServerCertificate` 속성.
      * Primetime DRM Server for Protected Streaming에서 Configuration/Tenant/Certificates/KeyServer 요소를 통해에 키 서버의 인증서를 지정합니다.
