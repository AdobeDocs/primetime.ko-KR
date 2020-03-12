---
description: Flash Media Rights Management Server 1.x 호환성과 관련된 두 가지 유형의 요청이 있습니다. 한 가지 유형의 요청은 1.x 고객에게 Adobe Primetime DRM 2.0 이상을 지원하는 런타임으로 업그레이드하도록 요청하는 데 사용됩니다. 또한 라이선스를 요청하기 전에 1.x 메타데이터를 Primetime DRM 포맷으로 업데이트하는 데 사용됩니다. 이러한 요청에 대한 지원은 FMRMS 1.0 또는 1.5를 사용하는 컨텐츠를 이전에 배포한 경우에만 필요합니다.
seo-description: Flash Media Rights Management Server 1.x 호환성과 관련된 두 가지 유형의 요청이 있습니다. 한 가지 유형의 요청은 1.x 고객에게 Adobe Primetime DRM 2.0 이상을 지원하는 런타임으로 업그레이드하도록 요청하는 데 사용됩니다. 또한 라이선스를 요청하기 전에 1.x 메타데이터를 Primetime DRM 포맷으로 업데이트하는 데 사용됩니다. 이러한 요청에 대한 지원은 FMRMS 1.0 또는 1.5를 사용하는 컨텐츠를 이전에 배포한 경우에만 필요합니다.
seo-title: FMRMS 호환성 처리
title: FMRMS 호환성 처리
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# FMRMS 호환성 처리 {#handling-fmrms-compatibility}

Flash Media Rights Management Server 1.x 호환성과 관련된 두 가지 유형의 요청이 있습니다. 한 가지 유형의 요청은 1.x 고객에게 Adobe Primetime DRM 2.0 이상을 지원하는 런타임으로 업그레이드하도록 요청하는 데 사용됩니다. 또한 라이선스를 요청하기 전에 1.x 메타데이터를 Primetime DRM 포맷으로 업데이트하는 데 사용됩니다. 이러한 요청에 대한 지원은 FMRMS 1.0 또는 1.5를 사용하는 컨텐츠를 이전에 배포한 경우에만 필요합니다.

## 클라이언트 업그레이드 {#upgrading-clients}

FMRMS 1.x 클라이언트가 Adobe Primetime DRM 서버에 접속하는 경우 서버는 클라이언트에 업그레이드를 요청해야 합니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`입니다.
* 요청 URL은 &quot;*1.x 컨텐츠의*&#x200B;기본 URL&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;입니다.

   다른 Adobe Primetime 요청 핸들러와 달리 이 핸들러는 요청 정보에 대한 액세스 권한을 제공하지 않거나 모든 응답 데이터를 설정할 필요가 없습니다. 인스턴스의 인스턴스를 `FMRMSv1RequestHandler`만든 다음 `close()`

## 메타데이터 업그레이드 {#upgrading-metadata}

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