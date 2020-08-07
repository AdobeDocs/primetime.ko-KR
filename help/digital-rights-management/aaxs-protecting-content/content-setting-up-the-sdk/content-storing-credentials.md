---
seo-title: 자격 증명 저장
title: 자격 증명 저장
uuid: dbce523c-32d9-423f-bc95-39786f85fc29
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# 자격 증명 저장{#storing-credentials}

SDK는 HSM 또는 PKCS12 파일 등 여러 가지 방법으로 자격 증명(공개 키 인증서 및 관련 개인 키)을 저장할 수 있습니다. 자격 증명은 개인 키가 필요한 경우(예: 패키지 사용자가 메타데이터를 서명하거나 라이센스 서버 또는 전송 공개 키로 암호화된 데이터를 해독하기 위해 라이센스 서버가) 사용됩니다. 개인 키는 컨텐츠와 라이센스 서버의 보안을 위해 철저하게 보호해야 합니다. PKCS12는 암호를 사용하여 암호화된 자격 증명을 포함하는 파일의 표준 형식입니다. 파일 확장자 .pfx는 일반적으로 이 형식의 파일에 사용됩니다.

>[!NOTE]
>
>Adobe은 최대 보안을 위해 HSM을 사용하는 것이 좋습니다. 자세한 내용은 Adobe 액세스 보안 배포 지침을 참조하십시오.

>[!NOTE]
>
>Java1.7부터 64비트 Sun Java for Windows는 HSM 디바이스와 통신하기 위해 Adobe 액세스 DRM이 필요한 PKCS11 인터페이스를 지원하지 않습니다. HSM을 사용하려는 경우 32비트 Java 버전을 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용하십시오.

HSM(Hardware Security Module)에 개인 키를 유지하고 SDK를 사용하여 HSM에서 얻은 자격 증명을 전달할 수 있습니다. HSM에 저장된 자격 증명을 사용하려면 HSM과 통신할 수 있는 JCE 공급자를 사용하여 개인 키에 대한 핸들을 가져옵니다. 그런 다음 공개 키가 들어 있는 개인 키 핸들, 공급자 이름 및 인증서를 전달하십시오 `ServerCredentialFactory.getServerCredential()`.

SunPKCS11 제공자는 HSM의 개인 키에 액세스하는 데 사용할 수 있는 JCE 공급자의 한 예입니다(이 공급자 사용에 대한 지침은 Sun Java 설명서 참조). 일부 HSM에는 JCE 제공자가 포함된 Java SDK도 포함되어 있습니다.

PEM과 DER는 공개 키 인증서를 인코딩하는 두 가지 방법입니다. PEM은 기본 64 인코딩이고 DER는 바이너리 인코딩입니다. 인증서 파일은 일반적으로 .cer, .pem 확장자를 사용합니다. 또는 .der. 인증서는 공개 키만 필요한 위치에서 사용됩니다. 구성 요소에 공개 키만 작동해야 하는 경우 자격 증명 또는 PKCS12 파일 대신 해당 구성 요소에 인증서를 제공하는 것이 좋습니다.
