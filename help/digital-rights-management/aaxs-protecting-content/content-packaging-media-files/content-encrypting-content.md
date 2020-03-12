---
seo-title: 컨텐츠 암호화
title: 컨텐츠 암호화
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 컨텐츠 암호화{#encrypting-content}

FLV 및 F4V 컨텐츠 암호화는 `MediaEncrypter` 객체 사용을 포함합니다. 오디오 트랙만 포함된 FLV 및 F4V 파일을 패키지화할 수도 있습니다. 하단 디바이스에 대한 H.264 컨텐츠를 암호화하는 경우 부분 암호화만 적용하여 성능을 향상시킬 수 있습니다. 이 경우 F4V 파일은 `F4VDRMParameters.setVideoEncryptionLevel`메서드를 사용하여 부분적으로 암호화될 수 있습니다.

Java API를 사용하여 FLV 또는 F4V 파일을 암호화하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 언급된 모든 JAR 파일을 포함합니다.
1. 서명을 위해 필요한 자격 증명을 로드하는 `ServerCredential` 인스턴스를 만듭니다.
1. 인스턴스를 `MediaEncrypter` 만듭니다. 어떤 유형의 파일이 있는지 모를 `MediaEncryperFactory` 경우 를 사용합니다. 그렇지 않으면 `FLVEncrypter` 또는 `F4VEncrypter` 직접 만들 수 있습니다.
1. 객체를 사용하여 암호화 옵션을 `DRMParameters` 지정합니다.
1. 객체를 사용하여 서명 옵션을 설정하고 해당 `SignatureParameters` 인스턴스를 `ServerCredential` `setServerCredentials` 메서드에 전달합니다.
1. 객체를 사용하여 키 및 라이센스 정보를 `V2KeyParameters` 설정합니다. 방법을 사용하여 정책을 `setPolicies` 설정합니다. 클라이언트가 라이센스 서버에 연결하는 데 필요한 정보를 `setLicenseServerUrl` 및 `setLicenseServerTransportCertificate` 메서드를 호출하여 설정합니다. 메서드를 사용하여 CEK 암호화 옵션을 `setKeyProtectionOptions` 설정하고 메서드를 사용하여 사용자 정의 속성을 `setCustomProperties` 설정합니다. 마지막으로, 사용된 암호화 유형에 따라 `DRMKeyParameters` 개체를 `VideoDRMParameters``AudioDRMParameters`하나, `FLVDRMParameters``F4VDRMParameters`또는 중 하나로 변환하고 암호화 옵션을 설정합니다.
1. 입력 및 출력 파일과 암호화 옵션을 `MediaEncrypter.encryptContent` 메서드에 전달하여 컨텐츠를 암호화합니다.

내용을 암호화하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 디렉토리에서 을 참조하십시오.
