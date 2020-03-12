---
seo-title: 자격 증명 저장
title: 자격 증명 저장
uuid: dbce523c-32d9-423f-bc95-39786f85fc29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 자격 증명 저장{#storing-credentials}

SDK는 HSM 또는 PKCS12 파일을 포함하여 여러 가지 방식으로 자격 증명(공개 키 인증서 및 관련 개인 키)을 저장할 수 있도록 지원합니다. 자격 증명은 개인 키가 필요할 때 사용됩니다(예: 패키지 사용자가 메타데이터를 서명하거나 라이센스 서버 또는 전송 공개 키로 암호화된 데이터의 암호를 해독하기 위해 라이센스 서버). 개인 키는 컨텐츠와 라이센스 서버의 보안을 유지하기 위해 철저히 보호되어야 합니다. PKCS12는 암호를 사용하여 암호화된 자격 증명을 포함하는 파일의 표준 형식입니다. 파일 확장명 .pfx는 일반적으로 이 형식의 파일에 사용됩니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>HSM을 사용하여 보안을 극대화할 것을 권장합니다. 자세한 내용은 Adobe Access 보안 배포 지침을 참조하십시오.

>[!NOTE] {importance=&quot;high&quot;}
>
>Java1.7부터 Windows용 64비트 Sun Java는 HSM 디바이스와 통신하기 위해 Adobe Access DRM에서 필요로 하는 PKCS11 인터페이스를 지원하지 않습니다. HSM을 사용하려는 경우 32비트 버전의 Java를 사용하거나 전체 PKCS11 인터페이스를 지원하는 JDK를 사용하십시오.

HSM(Hardware Security Module)에 개인 키를 보관하고 SDK를 사용하여 HSM에서 가져온 자격 증명을 전달할 수 있습니다. HSM에 저장된 자격 증명을 사용하려면 HSM과 통신할 수 있는 JCE 공급자를 사용하여 개인 키에 대한 핸들을 가져옵니다. 그런 다음 공개 키가 들어 있는 개인 키 핸들, 공급자 이름 및 인증서를 `ServerCredentialFactory.getServerCredential()`에 전달합니다.

SunPKCS11 공급자는 HSM의 개인 키에 액세스하는 데 사용할 수 있는 JCE 공급자의 한 예입니다(이 공급자 사용에 대한 지침은 Sun Java 설명서 참조). 일부 HSM에는 JCE 공급자가 포함된 Java SDK도 포함되어 있습니다.

PEM과 DER는 공개 키 인증서를 인코딩하는 두 가지 방법입니다. PEM 파섹 인증서 파일은 일반적으로 .cer, .pem 확장자를 사용합니다. 또는 .der. 인증서는 공개 키만 필요한 위치에서 사용됩니다. 구성 요소에 공개 키만 작동해야 하는 경우 자격 증명 또는 PKCS12 파일 대신 해당 구성 요소에 인증서를 제공하는 것이 좋습니다.
