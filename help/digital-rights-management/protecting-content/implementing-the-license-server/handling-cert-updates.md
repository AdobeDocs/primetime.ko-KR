---
seo-title: Adobe에서 발행한 인증서가 만료되는 경우 인증서 업데이트 처리
title: Adobe에서 발행한 인증서가 만료되는 경우 인증서 업데이트 처리
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Adobe에서 발행한 인증서가 만료될 때 인증서 업데이트 처리{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Adobe에서 새 인증서를 받아야 할 수도 있습니다. 예를 들어 평가 인증서가 만료되거나 평가 인증서를 프로덕션 인증서로 전환하는 경우 프로덕션 인증서가 만료됩니다. 인증서가 만료되고 이전 인증서를 사용하는 내용을 다시 패키지하지 않을 때마다 라이센스 서버에 이전 인증서와 새 인증서가 모두 인식되도록 할 수 있습니다.

새 인증서를 사용하여 서버를 업데이트하려면:

1. (선택 사항) 기존 DRM 정책 업데이트 목록 또는 해지 목록에 새 항목을 추가할 때 새 자격 증명으로 서명하고 기존 인증서를 사용하여 기존 파일의 서명을 확인해야 합니다.

   예를 들어 다음 명령줄을 사용하여 다른 자격 증명을 사용하여 서명된 기존 DRM 정책 업데이트 목록에 항목을 추가할 수 있습니다.

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (선택 사항) Java API를 사용하여 새로운 DRM 정책 업데이트 목록 또는 해지 목록으로 라이센스 서버를 업데이트합니다.

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   또는:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   참조 구현에서 사용하는 속성은 `HandlerConfiguration.RevocationList` 및 `HandlerConfiguration.PolicyUpdateList`입니다. 서명을 확인하는 데 사용되는 인증서를 업데이트해야 합니다.`RevocationList.verifySignature.X509Certificate`.

1. 라이센스 서버를 새 인증서와 이전 인증서로 업데이트합니다.

   이전 인증서를 사용하여 패키지된 콘텐트를 사용하려면 라이선스 서버가 이전 라이센스 서버 자격 증명과 새 라이센스 서버 자격 증명에 대한 액세스 권한을 가지고 있어야 합니다.

   라이센스 서버 자격 증명의 경우:

   * 현재 자격 증명이 `LicenseHandler` 생성자에 전달되었는지 확인합니다.

      * 참조 구현에서 `LicenseHandler.ServerCredential` 속성으로 설정합니다.
      * 보호된 스트리밍을 위한 Adobe Primetime DRM 서버에서 현재 자격 증명은 flashaccess-tenant.xml 파일의 `LicenseServerCredential` 요소에 지정된 첫 번째 자격 증명이어야 합니다.
   * 현재 자격 증명과 이전 자격 증명이 `AsymmetricKeyRetrieval`에 제공되었는지 확인합니다.

      * 참조 구현에서 `LicenseHandler.ServerCredential` 및 `AsymmetricKeyRetrieval.ServerCredential. n` 속성으로 설정합니다.

      * 보호된 스트리밍을 위한 Primetime DRM 서버에서 flashaccess-tenant.xml 파일의 `LicenseServerCredential` 요소의 첫 번째 자격 증명 뒤에 이전 자격 증명이 지정됩니다.

   전송 자격 증명의 경우:

   * 현재 자격 증명이 `HandlerConfiguration.setServerTransportCredential()` 메서드에 전달되었는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.ServerTransportCredential` 속성으로 설정합니다.
      * 보호된 스트리밍을 위한 Primetime DRM 서버에서 현재 자격 증명은 [!DNL flashaccess-tenant.xml] 파일의 `TransportCredential` 요소에 지정된 첫 번째 자격 증명이어야 합니다.
   * 이전 자격 증명이 `HandlerConfiguration.setAdditionalServerTransportCredentials`()에 제공되었는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.AdditionalServerTransportCredential. n` 속성으로 설정합니다.
      * 보호된 스트리밍을 위한 Primetime DRM 서버에서 flashaccess-tenant.xml 파일의 `TransportCredential` 요소의 첫 번째 자격 증명 후에 지정됩니다.




1. 패키징 도구를 업데이트하여 현재 자격 증명으로 컨텐츠를 패키지화하고 있는지 확인합니다. 최신 라이선스 서버 인증서, 전송 인증서 및 Packager 자격 증명이 패키징에 사용되는지 확인하십시오.
1. 키 서버의 라이센스 서버 인증서를 다음과 같이 업데이트합니다.

   * flashaccess-keyserver-tenant.xml에 이전 키 서버 자격 증명과 새 키 서버 자격 증명을 모두 포함하여 Adobe Primetime DRM 키 서버 테넌트 구성 파일의 자격 증명을 업데이트합니다.
   * 현재 인증서가 `HandlerConfiguration.setKeyServerCertificate()` 메서드에 전달되었는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.KeyServerCertificate` 속성으로 설정합니다.
      * 보호된 스트리밍을 위한 Primetime DRM 서버에서 구성/테넌트/인증서/키 서버 요소를 통해 키 서버의 인증서를 지정합니다.

