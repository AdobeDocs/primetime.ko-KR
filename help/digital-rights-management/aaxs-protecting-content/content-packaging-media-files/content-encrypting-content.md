---
title: 컨텐츠 암호화
description: 컨텐츠 암호화
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# 컨텐트{#encrypting-content} 암호화

FLV 및 F4V 내용 암호화는 `MediaEncrypter` 객체를 사용해야 합니다. 오디오 트랙만 포함된 FLV 및 F4V 파일을 패키지화할 수도 있습니다. 저가형 디바이스에 H.264 컨텐츠를 암호화할 때 성능을 개선하기 위해 부분 암호화만 적용하는 것이 유용할 수 있습니다. 이 경우 F4V 파일은 `F4VDRMParameters.setVideoEncryptionLevel` 메서드를 사용하여 부분적으로 암호화될 수 있습니다.

Java API를 사용하여 FLV 또는 F4V 파일을 암호화하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 설명된 모든 JAR 파일을 포함합니다.
1. 서명에 필요한 자격 증명을 로드할 `ServerCredential` 인스턴스를 만듭니다.
1. `MediaEncrypter` 인스턴스를 만듭니다. 어떤 유형의 파일이 있는지 모를 경우 `MediaEncryperFactory`을 사용합니다. 그렇지 않으면 `FLVEncrypter` 또는 `F4VEncrypter`을 직접 만들 수 있습니다.
1. `DRMParameters` 개체를 사용하여 암호화 옵션을 지정합니다.
1. `SignatureParameters` 개체를 사용하여 서명 옵션을 설정하고 `ServerCredential` 인스턴스를 `setServerCredentials` 메서드에 전달합니다.
1. `V2KeyParameters` 개체를 사용하여 키 및 라이센스 정보를 설정합니다. `setPolicies` 메서드를 사용하여 정책을 설정합니다. 클라이언트가 `setLicenseServerUrl` 및 `setLicenseServerTransportCertificate` 메서드를 호출하여 라이센스 서버에 연락하는 데 필요한 정보를 설정합니다. `setKeyProtectionOptions` 메서드를 사용하여 CEK 암호화 옵션과 `setCustomProperties` 메서드를 사용하여 사용자 정의 속성을 설정합니다. 마지막으로 사용된 암호화 유형에 따라 `DRMKeyParameters` 개체를 `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` 또는 `F4VDRMParameters` 중 하나로 캐스팅하고 암호화 옵션을 설정합니다.
1. 입력 및 출력 파일 및 암호화 옵션을 `MediaEncrypter.encryptContent` 메서드에 전달하여 내용을 암호화합니다.

내용을 암호화하는 방법을 보여 주는 샘플 코드는 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리의 `com.adobe.flashaccess.samples.mediapackager.EncryptContent`을 참조하십시오.
