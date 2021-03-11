---
title: 메타데이터 업그레이드
description: 메타데이터 업그레이드
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# 메타데이터 업그레이드 중{#upgrading-metadata}

Adobe Primetime DRM 클라이언트가 Flash Media Library Server 1.x로 패키지된 내용을 발견하면 컨텐츠에서 암호화 메타데이터를 추출하여 서버로 전송합니다. 그러면 서버가 FMRMS 1.x 메타데이터를 Primetime DRM 포맷으로 변환하여 클라이언트에 전송합니다. 그러면 클라이언트는 업데이트된 메타데이터를 표준 Primetime DRM 라이선스 요청으로 보냅니다.

* 요청 처리기 클래스는 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`입니다.
* 요청 URL은 &quot;*1.x 콘텐츠*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;의 기본 URL입니다.

서버가 클라이언트로부터 이전 메타데이터를 받을 때 메타데이터 변환을 즉시 수행할 수 있습니다. 또는 서버가 이전 컨텐츠를 미리 처리하고 변환된 메타데이터를 저장할 수 있습니다.이 경우 클라이언트가 새 메타데이터를 요청하면 서버는 이전 메타데이터의 라이센스 식별자와 일치하는 새 메타데이터를 가져와야 합니다.

메타데이터를 변환하려면 서버가 다음 단계를 수행해야 합니다.

* `LiveCycleKeyMetaData`을(를) 가져옵니다. 메타데이터를 미리 변환하기 위해 `LiveCycleKeyMetaData`은 `MediaEncrypter.examineEncryptedContent()`을(를) 사용하여 패키지된 1.x 파일에서 가져올 수 있습니다. 메타데이터도 메타데이터 변환 요청에 포함됩니다( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* 이전 메타데이터에서 라이선스 식별자를 가져오고 암호화 키 및 DRM 정책(이 정보는 원래 Adobe LiveCycle ES 데이터베이스에 있습니다. LiveCycle ES DRM 정책은 Primetime DRM 2.0 DRM 정책으로 변환해야 합니다.) 참조 구현에는 DRM 정책을 변환하고 LiveCycle ES에서 라이센스 정보를 내보내기 위한 스크립트 및 샘플 코드가 포함되어 있습니다.
* `MediaEncrypter.getKeyParameters()`을(를) 호출하여 검색하는 `V2KeyParameters` 개체를 채웁니다.

* 암호화 메타데이터 서명에 사용되는 Adobe에서 발행한 패키저 자격 증명인 `SigningCredential`을(를) 로드합니다. `MediaEncrypter.getSignatureParameters()`을(를) 호출하고 서명 자격 증명을 입력하여 `SignatureParameters` 개체를 가져옵니다.

* `V2ContentMetaData`을(를) 얻으려면 `MetaDataConverter.convertMetadata()`을(를) 호출하십시오.

* 나중에 사용하기 위해 `V2ContentMetaData.getBytes()`을(를) 호출하거나 `FMRMSv1MetadataHandler.setUpdatedMetadata()`로 전화하십시오.

