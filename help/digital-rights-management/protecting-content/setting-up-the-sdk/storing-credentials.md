---
title: 자격 증명 저장
description: 자격 증명 저장
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# 자격 증명 저장{#storing-credentials}

Primetime DRM SDK는 HSM(하드웨어 보안 모듈)을 사용하거나 PKCS12 파일로 사용하는 등 다양한 자격 증명 저장 방법을 지원합니다. 개인 키가 필요한 경우 SDK는 자격 증명(공개 키 인증서 및 관련 개인 키)을 사용합니다. 예를 들어, 패키저는 자격 증명을 사용하여 메타데이터에 서명하고, 라이선스 서버는 자격 증명을 사용하여 라이선스 서버 또는 전송 공개 키로 암호화된 데이터의 암호를 해독합니다.

콘텐츠와 라이선스 서버의 보안을 유지하려면 개인 키를 면밀히 보호해야 합니다. PKCS12는 암호로 암호화된 자격 증명을 저장하는 표준 아카이브 파일 형식입니다. (PKCS12 파일 자체를 암호화하고 서명할 수도 있습니다.) 파일 확장명 [!DNL .pfx] 는 일반적으로 이 형식을 지원하는 파일에 사용됩니다.

>[!NOTE]
>
>Adobe은 보안을 최대화하기 위해 HSM을 사용할 것을 권장합니다.
>
>다음을 참조하십시오. *Adobe Primetime DRM 보안 배포 지침* 가이드.

>[!NOTE]
>
>Java 1.7부터 64비트 Windows용 Sun Java는 Primetime DRM에서 HSM 장치와 통신하는 데 필요한 PKCS11 인터페이스를 더 이상 지원하지 않습니다. HSM을 사용하려면 32비트 버전의 Java를 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용해야 합니다.

HSM에 개인 키를 보관하고 Primetime DRM SDK를 사용하여 HSM에서 가져온 자격 증명을 전달할 수 있습니다. HSM에 저장된 자격 증명을 사용하려면 HSM과 통신할 수 있는 JCE 공급자를 사용하여 개인 키에 대한 핸들을 얻어야 합니다. 그런 다음 개인 키 핸들, 공급자 이름 및 공개 키가 포함된 인증서를 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11 공급자는 HSM의 개인 키에 액세스하는 데 사용할 수 있는 JCE 공급자의 한 가지 예를 나타냅니다. 일부 HSM은 JCE 공급자와 번들로 제공되는 Java SDK에도 포함되어 있습니다.

이 공급자를 사용하는 방법에 대한 지침은 Sun Java 설명서 를 참조하십시오.

PEM 및 DER은 공개 키 인증서를 인코딩하는 방법입니다. PEM은 base-64 인코딩이며 DER은 이진 인코딩입니다. 인증서 파일은 일반적으로 확장을 사용합니다 [!DNL .cer], [!DNL .pem], 또는 [!DNL .der]. 인증서는 공개 키만 필요한 경우에 사용됩니다. 구성 요소가 작동하기 위해 공개 키만 필요로 하는 경우 해당 구성 요소에 자격 증명 또는 PKCS12 파일 대신 인증서를 제공하는 것이 좋습니다.
