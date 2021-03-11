---
title: 개별 CA CRL 생성
description: 개별 CA CRL 생성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 개인화 CA CRL 생성{#create-individualization-ca-crl}

이 CRL(Certificate Revocation List) 배포 지점은 개인 지정 서버에서 발행한 각 컴퓨터 인증서에 포함됩니다. 라이센스 서버의 컴퓨터 인증서 유효성 검사 동안 이 CRL은 인증서에 나열된 배포 지점(또는 이미 다운로드한 경우 캐시에서 읽기)에서 다운로드되며 인증서가 해지되지 않았는지 확인합니다.

>[!NOTE]
>
>CRL 배포 지점에 대한 URL을 설정하려면 [!DNL AdobeInitial.properties] `cert.machine.crldp` 필드를 설정해야 합니다. 이 배포 지점은 Primetime DRM에서 유효성 확인을 하지 않은 *입니다.* 이 URL이 유효한지 확인해야 합니다. 잘못된 URL로 인한 오류는 라이센스 서버에서 유효성 검사 오류가 나타날 때까지 발생하지 않습니다.

아래 요약은 라이센스 서버에서 사용할 수 있는 CRL을 만들기 위해 OpenSSL을 사용하는 샘플 지침을 간략히 설명합니다. 프로덕션 개인화 CA 자격 증명을 받은 후에는 이러한 단계를 안전한 방식으로 수행하는 것이 좋습니다.

1. 작업 디렉터리를 이 배포에 포함된 [!DNL create_crl] 디렉토리로 변경합니다.
1. Personalization CA [!DNL pfx]을(를) 동일한 [!DNL create_crl] 디렉토리로 복사합니다.

   다음 단계에서는 개인 지정 CA pfx의 이름이 [!DNL i15n.pfx]인 것으로 가정합니다. 설정에 맞게 조정합니다.
1. 개인 지정 CA [!DNL pfx] 파일의 개인 키를 추출합니다.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 개인 키를 [!DNL pksc8] 형식으로 변환합니다.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. CRL을 생성합니다.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   이 예제에서는 기본 1개월 유효 기간을 갖는 CRL을 만듭니다. 기본값을 무시하려면 `-crldays` 및 `-crlhours` 옵션을 사용합니다.

   CRL을 생성하면 [!DNL openssl.conf]에서 가리키는 [!DNL index] 및 [!DNL crlnumber] 파일이 사용됩니다. 기본적으로 작업 디렉토리의 [!DNL demoCA] 위치가 사용됩니다. 샘플 [!DNL index] 및 [!DNL crlnumber] 파일이 제공된 [!DNL demoCA] 디렉토리에 포함됩니다.

1. 이전 단계에서 생성된 CRL 파일을 라이센스 서버에서 접속할 수 있는 적절한 위치에 배포합니다(예:개인화 서버 [!DNL ROOT]).
1. CRL이 지정된 후 라이센스 서버를 다시 시작합니다.
