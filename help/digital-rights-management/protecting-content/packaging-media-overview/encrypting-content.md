---
title: 컨텐츠 암호화
description: 컨텐츠 암호화
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# 컨텐트{#encrypting-content} 암호화

`MediaEncrypter` 개체로 비디오 내용을 암호화합니다. 오디오 트랙만 포함하는 미디어 파일을 암호화할 수 있습니다. 부분 암호만 적용할 수도 있습니다.예를 들어, 저가형 디바이스에 H.264 컨텐츠를 암호화할 때 성능을 향상시킬 수 있습니다.

Java API를 사용하여 미디어 파일을 암호화하려면:

1. 개발 환경을 설정하고 프로젝트 내에 *개발 환경 설정*&#x200B;에 언급된 모든 JAR 파일을 포함합니다.
1. 서명에 필요한 자격 증명을 로드할 `ServerCredential` 인스턴스를 만듭니다.
1. `MediaEncrypter` 인스턴스를 만듭니다. 어떤 유형의 파일이 있는지 모를 경우 `MediaEncryperFactory`을 사용합니다.

1. `DRMParameters` 개체를 사용하여 암호화 옵션을 지정합니다.
1. `SignatureParameters` 개체를 사용하여 서명 옵션을 설정하고 `ServerCredential` 인스턴스를 `setServerCredentials` 메서드에 전달합니다.

1. `V2KeyParameters` 개체를 사용하여 키 및 라이센스 정보를 설정합니다. `setPolicies` 메서드를 사용하여 DRM 정책을 설정합니다. 클라이언트가 `setLicenseServerUrl` 및 `setLicenseServerTransportCertificate` 메서드를 호출하여 라이센스 서버에 연락하는 데 필요한 정보를 설정합니다. `setKeyProtectionOptions` 메서드를 사용하여 CEK 암호화 옵션과 `setCustomProperties` 메서드를 사용하여 사용자 정의 속성을 설정합니다. 마지막으로 사용된 암호화 유형에 따라 `DRMKeyParameters` 개체를 적절한 유형( `VideoDRMParameters`, `AudioDRMParameters`)으로 캐스팅하고 암호화 옵션을 설정합니다.

1. 입력 및 출력 파일 및 암호화 옵션을 `MediaEncrypter.encryptContent` 메서드에 전달하여 내용을 암호화합니다.

내용을 암호화하는 방법을 보여주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL samples/] 디렉토리의 `com.adobe.flashaccess.samples.mediapackager.EncryptContent`을 참조하십시오.
