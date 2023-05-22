---
title: 개별화 CA CRL 만들기
description: 개별화 CA CRL 만들기
copied-description: true
exl-id: 72147209-1337-4aed-9e4e-210c905c55a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 개별화 CA CRL 만들기{#create-individualization-ca-crl}

이 CRL(인증서 해지 목록) 배포 지점은 개별화 서버에서 발급한 각 컴퓨터 인증서 내에 포함됩니다. 라이선스 서버에서 컴퓨터 인증서를 확인하는 동안 이 CRL은 인증서에 나열된 배포 지점에서 다운로드되고(또는 이미 다운로드한 경우 캐시에서 읽음) 인증서가 해지되지 않았는지 확인합니다.

>[!NOTE]
>
>CRL 배포 지점의 URL을 설정하려면 [!DNL AdobeInitial.properties] `cert.machine.crldp` 필드. 이 배포 지점은 *아님* Primetime DRM에서 유효성을 확인했습니다. 이 URL이 유효한지 확인해야 합니다. 잘못된 URL로 인한 오류는 라이센스 서버에서 유효성 검사 오류가 나타날 때까지 명확하지 않습니다.

다음은 라이센스 서버에서 사용할 수 있는 CRL을 만들기 위해 OpenSSL을 사용하는 방법에 대한 간소화된 샘플 지침입니다. Adobe은 프로덕션 개별화 CA 자격 증명을 얻은 후 보안 방식 및 환경에서 이러한 단계를 수행할 것을 권장합니다.

1. 작업 디렉터리를 로 변경합니다. [!DNL create_crl] 이 배포에 포함된 디렉토리.
1. 개별화 CA 복사 [!DNL pfx] 동일에 [!DNL create_crl] 디렉토리.

   다음 단계에서는 개별화 CA pfx의 이름이 로 지정되어 있다고 가정합니다 [!DNL i15n.pfx]. 설정에 맞게 조정하십시오.
1. 개별화 CA 추출 [!DNL pfx] 파일의 개인 키.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 개인 키를 다음으로 변환 [!DNL pksc8] 포맷.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. CRL을 생성합니다.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   이 예에서는 기본 1개월 유효 기간으로 CRL을 생성합니다. 사용 `-crldays` 및 `-crlhours` 기본값을 재정의하는 옵션.

   CRL 생성은 [!DNL index] 및 [!DNL crlnumber] 에서 지정한 파일 [!DNL openssl.conf]. 기본적으로 [!DNL demoCA] 작업 디렉토리의 위치가 사용됩니다. 샘플 [!DNL index] 및 [!DNL crlnumber] 제공된 에는 파일이 포함됩니다 [!DNL demoCA] 디렉토리.

1. 이전 단계에서 생성된 CRL 파일을 라이센스 서버에 연결할 수 있는 적절한 위치에 배포합니다(예: 개별화 서버). [!DNL ROOT]).
1. CRL이 설치되면 라이센스 서버를 다시 시작합니다.
