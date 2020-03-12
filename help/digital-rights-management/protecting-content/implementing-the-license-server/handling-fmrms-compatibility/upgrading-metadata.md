---
seo-title: 메타데이터 업그레이드
title: 메타데이터 업그레이드
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 메타데이터 업그레이드{#upgrading-metadata}

Adobe Primetime DRM 클라이언트가 Flash Media Rights Management Server 1.x와 함께 패키지된 컨텐츠를 발견하면 컨텐츠에서 암호화 메타데이터를 추출하여 서버로 전송합니다. 그러면 서버가 FMRMS 1.x 메타데이터를 Primetime DRM 포맷으로 변환하여 클라이언트에 전송합니다. 그러면 클라이언트는 업데이트된 메타데이터를 표준 Primetime DRM 라이선스 요청으로 전송합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`입니다.
* 요청 URL은 &quot;*1.x 컨텐츠의*&#x200B;기본 URL&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;입니다.

서버가 클라이언트로부터 이전 메타데이터를 받을 때 메타데이터 변환이 신속하게 수행될 수 있습니다. 또는 서버가 이전 컨텐츠를 미리 처리하고 변환된 메타데이터를 저장할 수 있습니다.이 경우 클라이언트가 새 메타데이터를 요청하면 서버는 이전 메타데이터의 라이센스 식별자와 일치하는 새 메타데이터를 가져와야 합니다.

메타데이터를 변환하려면 서버가 다음 단계를 수행해야 합니다.

* Get. `LiveCycleKeyMetaData`. 메타데이터를 미리 변환하려면 를 사용하여 1.x 패키지 파일에서 가져올 `LiveCycleKeyMetaData` 수 `MediaEncrypter.examineEncryptedContent()`있습니다. 메타데이터는 메타데이터 변환 요청( `FMRMSv1MetadataHandler.getOriginalMetadata()`)에도 포함됩니다.

* 이전 메타데이터에서 라이선스 식별자를 얻고 암호화 키와 DRM 정책을 찾습니다(이 정보는 원래 Adobe LiveCycle ES 데이터베이스에 있습니다. LiveCycle ES DRM 정책은 Primetime DRM 2.0 DRM 정책으로 전환해야 합니다.) 참조 구현에는 DRM 정책을 변환하고 LiveCycle ES에서 라이센스 정보를 내보내기 위한 스크립트 및 샘플 코드가 포함되어 있습니다.
* 호출할 때 검색하는 `V2KeyParameters` 개체를 `MediaEncrypter.getKeyParameters()`채웁니다.

* 암호화 메타데이터 서명에 사용되는 Adobe에서 발행한 패키지 자격 증명인 `SigningCredential`패키지를 로드합니다. 서명 `SignatureParameters` 자격 증명을 호출하고 `MediaEncrypter.getSignatureParameters()` 입력하여 개체를 가져옵니다.

* 전화를 `MetaDataConverter.convertMetadata()` 걸어 물건을 `V2ContentMetaData`구한다.

* 나중에 사용하기 위해 전화 `V2ContentMetaData.getBytes()` 및 스토어 또는 전화 `FMRMSv1MetadataHandler.setUpdatedMetadata()`문의

