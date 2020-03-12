---
seo-title: 컨텐츠 암호화
title: 컨텐츠 암호화
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 컨텐츠 암호화{#encrypting-content}

이 `MediaEncrypter` 객체를 사용하여 비디오 컨텐츠를 암호화합니다. 오디오 트랙만 포함하는 미디어 파일을 암호화할 수 있습니다. 부분 암호화만 적용할 수도 있습니다.예를 들어, 저가 디바이스에 대한 H.264 컨텐츠를 암호화할 때 성능을 향상시킬 수 있습니다.

Java API 파섹

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 *설정에 언급된 모든 JAR 파일을* 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드하는 `ServerCredential` 인스턴스를 만듭니다.
1. 인스턴스를 `MediaEncrypter` 만듭니다. 어떤 유형의 파일이 있는지 모를 `MediaEncryperFactory` 경우 를 사용합니다.

1. 객체를 사용하여 암호화 옵션을 `DRMParameters` 지정합니다.
1. 객체를 사용하여 서명 옵션을 설정하고 해당 `SignatureParameters` 인스턴스를 `ServerCredential` `setServerCredentials` 메서드에 전달합니다.

1. 객체를 사용하여 키 및 라이센스 정보를 `V2KeyParameters` 설정합니다. 이 방법을 사용하여 DRM 정책을 `setPolicies` 설정합니다. 클라이언트가 라이센스 서버에 연결하는 데 필요한 정보를 `setLicenseServerUrl` 및 `setLicenseServerTransportCertificate` 메서드를 호출하여 설정합니다. 메서드를 사용하여 CEK 암호화 옵션을 `setKeyProtectionOptions` 설정하고 메서드를 사용하여 사용자 정의 속성을 `setCustomProperties` 설정합니다. 마지막으로 사용된 암호화 유형에 따라 적절한 유형(, `DRMKeyParameters` `VideoDRMParameters``AudioDRMParameters`)으로 개체를 캐스팅하고 암호화 옵션을 설정합니다.

1. 입력 및 출력 파일과 암호화 옵션을 `MediaEncrypter.encryptContent` 메서드에 전달하여 컨텐츠를 암호화합니다.

내용을 암호화하는 방법을 보여 주는 샘플 코드는 참조 구현 `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 명령줄 도구 [!DNL samples/] 디렉토리에서 참조하십시오.
