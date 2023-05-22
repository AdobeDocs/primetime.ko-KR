---
title: 메타데이터 업그레이드 중
description: 메타데이터 업그레이드 중
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 메타데이터 업그레이드 중{#upgrading-metadata}

Adobe Primetime DRM 클라이언트는 Flash Media Rights Management 서버 1.x로 패키지된 콘텐츠를 접하면 콘텐츠에서 암호화 메타데이터를 추출하여 서버로 전송합니다. 그런 다음 서버는 FMRMS 1.x 메타데이터를 Primetime DRM 형식으로 변환하여 클라이언트로 전송합니다. 그런 다음 클라이언트는 표준 Primetime DRM 라이센스 요청에서 업데이트된 메타데이터를 전송합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 요청 URL은 입니다.*1.x 콘텐츠의 기본 URL*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

메타데이터 변환은 서버가 클라이언트로부터 이전 메타데이터를 수신할 때 즉시 수행할 수 있습니다. 또는 서버가 이전 콘텐츠를 사전 처리하고 변환된 메타데이터를 저장할 수 있습니다. 이 경우 클라이언트가 새 메타데이터를 요청하면 서버는 이전 메타데이터의 라이선스 식별자와 일치하는 새 메타데이터를 가져오기만 하면 됩니다.

메타데이터를 변환하려면 서버는 다음 단계를 수행해야 합니다.

* Get `LiveCycleKeyMetaData`. 메타데이터를 미리 변환하려면 `LiveCycleKeyMetaData` 를 사용하여 1.x 패키지된 파일에서 가져올 수 있습니다. `MediaEncrypter.examineEncryptedContent()`. 메타데이터는 메타데이터 변환 요청에도 포함됩니다( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* 이전 메타데이터에서 라이센스 식별자를 가져와 암호화 키 및 DRM 정책(이 정보는 원래 Adobe LiveCycle ES 데이터베이스에 있음)을 찾습니다. LiveCycle ES DRM 정책은 Primetime DRM 2.0 DRM 정책으로 변환해야 합니다.) 참조 구현에는 DRM 정책을 변환하고 LiveCycle ES에서 라이센스 정보를 내보내기 위한 스크립트와 샘플 코드가 포함됩니다.
* 다음을 입력합니다. `V2KeyParameters` 객체(호출하여 검색) `MediaEncrypter.getKeyParameters()`).

* 을(를) 로드합니다 `SigningCredential`: 암호화 메타데이터 서명에 사용되는 Adobe에서 발급한 패키지 자격 증명입니다. 가져오기 `SignatureParameters` 를 호출한 개체 `MediaEncrypter.getSignatureParameters()` 서명 자격 증명을 입력합니다.

* 호출 `MetaDataConverter.convertMetadata()` 을(를) 가져오려면 `V2ContentMetaData`.

* 호출 `V2ContentMetaData.getBytes()` 나중에 사용하거나 전화를 위해 저장 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

