---
seo-title: 자격 증명 저장
title: 자격 증명 저장
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# 자격 증명 저장{#storing-credentials}

Primetime DRM SDK는 HSM(Hardware Security Module) 또는 PKCS12 파일로 사용하는 등 자격 증명을 저장하는 다양한 방법을 지원합니다. SDK는 개인 키가 필요한 경우 자격 증명(공개 키 인증서 및 관련 개인 키)을 사용합니다. 예를 들어 Packager는 자격 증명을 사용하여 메타데이터를 서명합니다.라이센스 서버는 자격 증명을 사용하여 라이센스 서버 또는 전송 공개 키로 암호화된 데이터를 해독합니다.

컨텐트 및 라이센스 서버의 보안을 위해 개인 키를 면밀히 보호해야 합니다. PKCS12는 암호로 암호화된 자격 증명을 저장하기 위한 표준 보관 파일 형식입니다. PKCS12 파일 자체를 암호화하고 서명할 수도 있습니다. 파일 확장명 [!DNL .pfx]은 일반적으로 이 형식을 지원하는 파일에 사용됩니다.

>[!NOTE]
>
>Adobe에서는 최대 보안을 위해 HSM을 사용하는 것이 좋습니다.
>
>*Adobe Primetime DRM 보안 배포 지침* 가이드를 참조하십시오.

>[!NOTE]
>
>Java 1.7부터 Windows용 64비트 Sun Java는 Primetime DRM이 HSM 디바이스와 통신하는 데 필요한 PKCS11 인터페이스를 더 이상 지원하지 않습니다. HSM을 사용하려는 경우 32비트 버전의 Java를 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용해야 합니다.

HSM에 개인 키를 유지하고 Primetime DRM SDK를 사용하여 HSM에서 받은 자격 증명을 전달할 수 있습니다. HSM에 저장된 자격 증명을 사용하려면 HSM과 통신하여 개인 키에 대한 핸들을 얻기 위해 JCE 공급자를 사용해야 합니다. 그런 다음 공개 키가 포함된 개인 키 핸들, 공급자 이름 및 인증서를 `ServerCredentialFactory.getServerCredential()`에 전달해야 합니다.

SunPKCS11 공급자는 HSM에서 개인 키에 액세스하는 데 사용할 수 있는 JCE 공급자의 한 예를 나타냅니다. 일부 HSM은 JCE 공급자와 번들로 제공되는 Java SDK에도 포함되어 있습니다.

이 공급자 사용 방법에 대한 지침은 Sun Java 설명서를 참조하십시오.

PEM과 DER는 공개 키 인증서를 인코딩하는 방법입니다. PEM은 기본 64 인코딩이고 DER는 바이너리 인코딩입니다. 인증서 파일은 일반적으로 [!DNL .cer], [!DNL .pem] 또는 [!DNL .der] 확장자를 사용합니다. 인증서는 공개 키만 필요한 경우에 사용됩니다. 구성 요소에 공개 키만 작동해야 하는 경우 자격 증명 또는 PKCS12 파일 대신 해당 구성 요소에 인증서를 제공하는 것이 좋습니다.
