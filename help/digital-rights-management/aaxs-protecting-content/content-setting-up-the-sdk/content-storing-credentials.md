---
title: 자격 증명 저장
description: 자격 증명 저장
copied-description: true
exl-id: 42bccf3a-307f-4763-8b02-f983bcc2e131
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# 자격 증명 저장{#storing-credentials}

SDK는 HSM에서 또는 PKCS12 파일로 자격 증명(공개 키 인증서 및 연결된 개인 키)을 저장하는 여러 가지 방법을 지원합니다. 자격 증명은 개인 키가 필요할 때 사용됩니다(예: 패키저가 메타데이터에 서명하거나 라이선스 서버가 라이선스 서버 또는 전송 공개 키로 암호화된 데이터의 암호를 해독하는 데 사용). 컨텐츠 및 라이선스 서버의 보안을 유지하려면 개인 키를 철저하게 보호해야 합니다. PKCS12는 암호를 사용하여 암호화된 자격 증명이 포함된 파일에 대한 표준 형식입니다. 파일 확장명 .pfx는 일반적으로 이 형식의 파일에 사용됩니다.

>[!NOTE]
>
>Adobe은 보안을 최대화하기 위해 HSM을 사용할 것을 권장합니다. 자세한 내용은 Adobe 액세스 보안 배포 지침을 참조하십시오.

>[!NOTE]
>
>Java1.7부터 64비트 Sun Java for Windows는 DRM Adobe에서 HSM 장치와 통신하는 데 필요한 PKCS11 인터페이스를 지원하지 않습니다. HSM을 사용할 계획이라면 32비트 버전의 Java를 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용하십시오.

HSM(하드웨어 보안 모듈)에 개인 키를 보관하고 SDK를 사용하여 HSM에서 가져온 자격 증명을 전달할 수 있습니다. HSM에 저장된 자격 증명을 사용하려면 HSM과 통신할 수 있는 JCE 공급자를 사용하여 개인 키에 대한 핸들을 가져옵니다. 그런 다음 개인 키 핸들, 공급자 이름 및 공개 키가 포함된 인증서를 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11 공급자는 HSM의 개인 키에 액세스하는 데 사용할 수 있는 JCE 공급자의 한 예입니다(이 공급자의 사용에 대한 지침은 Sun Java 설명서 참조). 일부 HSM에는 JCE 공급자가 포함된 Java SDK도 포함되어 있습니다.

PEM과 DER은 공개 키 인증서를 인코딩하는 두 가지 방법입니다. PEM은 base-64 인코딩이며 DER은 이진 인코딩입니다. 인증서 파일은 일반적으로 .cer, .pem 확장명을 사용합니다. 또는 .der. 인증서는 공개 키만 필요한 곳에서 사용됩니다. 구성 요소에서 공개 키만 작동시켜야 하는 경우에는 해당 구성 요소에 자격 증명이나 PKCS12 파일 대신 인증서를 제공하는 것이 좋습니다.
