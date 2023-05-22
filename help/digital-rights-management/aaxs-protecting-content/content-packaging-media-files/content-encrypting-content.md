---
title: 콘텐츠 암호화
description: 콘텐츠 암호화
copied-description: true
exl-id: 84a490ae-af0c-43c5-a849-ed832e83a28d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 콘텐츠 암호화{#encrypting-content}

FLV 및 F4V 콘텐츠 암호화에는 `MediaEncrypter` 개체. 오디오 트랙만 포함된 FLV 및 F4V 파일을 패키징할 수도 있습니다. 하위 엔드 디바이스용 H.264 콘텐츠를 암호화할 때 부분 암호화만 적용하여 성능을 향상시키는 것이 실용적일 수 있습니다. 이러한 경우, F4V 파일은 다음을 사용하여 부분적으로 암호화될 수 있다. `F4VDRMParameters.setVideoEncryptionLevel`메서드를 사용합니다.

Java API를 사용하여 FLV 또는 F4V 파일을 암호화하려면 다음 단계를 수행하십시오.

1. 개발 환경을 설정하고 프로젝트 내의 개발 환경 설정에 언급된 모든 JAR 파일을 포함합니다.
1. 만들기 `ServerCredential` 서명에 필요한 자격 증명을 로드할 인스턴스입니다.
1. 만들기 `MediaEncrypter` 인스턴스. 사용 `MediaEncryperFactory` 어떤 유형의 파일이 있는지 모를 경우 그렇지 않으면 `FLVEncrypter` 또는 `F4VEncrypter` 직접.
1. 다음을 사용하여 암호화 옵션 지정 `DRMParameters` 개체.
1. 다음을 사용하여 서명 옵션 설정 `SignatureParameters` 개체 및 전달 `ServerCredential` 인스턴스를 해당 인스턴스로 `setServerCredentials` 메서드를 사용합니다.
1. 를 사용하여 키 및 라이선스 정보 설정 `V2KeyParameters` 개체. 다음을 사용하여 정책 설정 `setPolicies` 메서드를 사용합니다. 를 호출하여 클라이언트가 라이선스 서버에 연결하는 데 필요한 정보를 설정합니다. `setLicenseServerUrl` 및 `setLicenseServerTransportCertificate` 메서드를 사용합니다. 다음을 사용하여 CEK 암호화 옵션 설정 `setKeyProtectionOptions` 메서드 및 를 사용하는 해당 사용자 지정 속성 `setCustomProperties` 메서드를 사용합니다. 마지막으로 사용된 암호화 유형에 따라 `DRMKeyParameters` 다음 중 하나에 오브젝트 추가 `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`, 또는 `F4VDRMParameters`을 클릭하고 암호화 옵션을 설정합니다.
1. 입출력 파일과 암호화 옵션을 로 전달하여 콘텐츠를 암호화합니다. `MediaEncrypter.encryptContent` 메서드를 사용합니다.

콘텐츠 암호화 방법을 보여 주는 샘플 코드는 을 참조하십시오. `com.adobe.flashaccess.samples.mediapackager.EncryptContent` 참조 구현 명령줄 도구 &quot;samples&quot; 디렉토리에서
