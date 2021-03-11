---
title: Adobe에서 발행한 인증서가 만료될 때 인증서 업데이트 처리
description: Adobe에서 발행한 인증서가 만료될 때 인증서 업데이트 처리
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Adobe에서 발행한 인증서가 만료될 때 인증서 업데이트 처리 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Adobe에서 새 인증서를 가져와야 하는 경우가 있을 수 있습니다. 예를 들어 프로덕션 인증서가 만료되거나 평가 인증서를 프로덕션 인증서로 전환하는 경우 평가 인증서가 만료됩니다. 인증서가 만료되고 이전 인증서를 사용한 내용을 다시 패키지하지 않으려는 경우. 라이센스 서버에 이전 인증서와 새 인증서를 모두 인식하도록 할 수 있습니다.

다음 절차를 사용하여 새 인증서로 서버를 업데이트합니다.

1. (선택 사항) 기존 정책 업데이트 목록 또는 해지 목록에 새 항목을 추가할 때는 새 자격 증명으로 서명하고 기존 인증서를 사용하여 기존 파일의 서명을 확인합니다.

   예를 들어 다음 명령줄을 사용하여 다른 자격 증명을 사용하여 서명된 기존 정책 업데이트 목록에 항목을 추가합니다.

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Java API를 사용하여 라이센스 서버를 새 정책 업데이트 목록 또는 해지 목록으로 업데이트합니다.

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   또는:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   참조 구현에서 사용하는 속성은 `HandlerConfiguration.RevocationList` 및 `HandlerConfiguration.PolicyUpdateList`입니다. 서명 확인에 사용되는 인증서를 업데이트합니다.`RevocationList.verifySignature.X509Certificate`.

1. 이전 인증서를 사용하여 패키지된 콘텐트를 사용하려면 라이센스 서버에 이전 및 새 라이센스 서버 자격 증명과 전송 자격 증명이 필요합니다. 라이센스 서버를 새 인증서와 이전 인증서로 업데이트합니다.

   라이센스 서버 자격 증명의 경우:

   * 현재 자격 증명이 `LicenseHandler` 생성자에 전달되었는지 확인합니다.

      * 참조 구현에서 `LicenseHandler.ServerCredential` 속성을 통해 설정합니다.
      * 보호 스트리밍을 위한 Adobe Access Server에서 현재 자격 증명은 flashaccess-tenant.xml 파일의 `LicenseServerCredential` 요소에 지정된 첫 번째 자격 증명이어야 합니다.
   * 현재 자격 증명과 이전 자격 증명이 `AsymmetricKeyRetrieval`에 제공되는지 확인합니다.

      * 참조 구현에서 `LicenseHandler.ServerCredential` 및 `AsymmetricKeyRetrieval.ServerCredential. n` 속성을 통해 설정합니다.
      * 보호된 스트리밍을 위한 Adobe Access Server에서 이전 자격 증명은 flashaccess-tenant.xml 파일의 `LicenseServerCredential` 요소에 있는 첫 번째 자격 증명 뒤에 지정됩니다.

   전송 자격 증명의 경우:

   * 현재 자격 증명이 `HandlerConfiguration.setServerTransportCredential()` 메서드에 전달되었는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.ServerTransportCredential` 속성을 통해 설정합니다.
      * 안전한 스트리밍을 위해 Adobe Access Server에서 현재 자격 증명은 flashaccess-tenant.xml 파일의 `TransportCredential` 요소에 지정된 첫 번째 자격 증명이어야 합니다.
   * 이전 자격 증명이 `HandlerConfiguration.setAdditionalServerTransportCredentials`()에 제공되는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.AdditionalServerTransportCredential. n` 속성을 통해 설정합니다.
      * 안전한 스트리밍을 위한 Adobe Access Server에서 flashaccess-tenant.xml 파일의 `TransportCredential` 요소에 있는 첫 번째 자격 증명 후에 이 이름이 지정됩니다.




1. 패키징 도구를 업데이트하여 현재 자격 증명으로 컨텐츠를 패키징하고 있는지 확인합니다. 최신 라이선스 서버 인증서, 전송 인증서 및 패키지 자격 증명이 패키징에 사용되는지 확인하십시오.
1. 키 서버의 라이센스 서버 인증서를 업데이트하려면:

   * Adobe 액세스 키 서버 테넌트 구성 파일의 자격 증명을 업데이트합니다. flashaccess-keyserver-tenant.xml에 이전 및 새 키 서버 자격 증명을 모두 포함합니다.
   * 현재 인증서가 `HandlerConfiguration.setKeyServerCertificate()` 메서드에 전달되었는지 확인합니다.

      * 참조 구현에서 `HandlerConfiguration.KeyServerCertificate` 속성을 통해 설정합니다.
      * 보호된 스트리밍을 위한 Adobe Access Server에서 Configuration/Tenant/Certificates/KeyServer 요소를 통해 의 키 서버 인증서를 지정합니다.

