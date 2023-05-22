---
description: FMRMS 호환성 처리 중
title: 클라이언트 업그레이드
exl-id: 7774b408-c2cb-400b-be41-74cc9739e0e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# FMRMS 호환성 처리 중 {#handling-fmrms-compatibility}

Flash 미디어 Rights Management 서버 1.x 호환성과 관련된 요청에는 두 가지 유형이 있습니다. 한 유형의 요청은 1.x 클라이언트에 Adobe Primetime DRM 2.0 이상을 지원하는 런타임으로 업그레이드하라는 메시지를 표시하는 데 사용됩니다. 다른 하나는 라이선스를 요청하기 전에 1.x 메타데이터를 Primetime DRM 형식으로 업데이트하는 데 사용됩니다. 이러한 요청에 대한 지원은 FMRMS 1.0 또는 1.5를 사용하는 콘텐츠를 이전에 배포한 경우에만 필요합니다.

## 클라이언트 업그레이드 {#upgrading-clients}

FMRMS 1.x 클라이언트가 Adobe Primetime DRM 서버에 연결된 경우 서버는 클라이언트에 업그레이드를 요청해야 합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 요청 URL은 입니다.*1.x 콘텐츠의 기본 URL*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   다른 Adobe Primetime 요청 핸들러와 달리 이 핸들러는 요청 정보에 대한 액세스를 제공하지 않거나 응답 데이터를 설정해야 합니다. 의 인스턴스 만들기 `FMRMSv1RequestHandler`, 그런 다음 를 호출합니다. `close()`

## 메타데이터 업그레이드 중 {#upgrading-metadata}

Adobe 액세스 클라이언트가 Flash Media Rights Management 서버 1.x로 패키지된 콘텐츠를 발견하면 콘텐츠에서 암호화 메타데이터를 추출하여 서버로 전송합니다. 서버에서 FMRMS 1.x 메타데이터를 Adobe 액세스 형식으로 변환하고 이를 클라이언트로 다시 보냅니다. 그런 다음 클라이언트는 표준 Adobe 액세스 라이선스 요청에서 업데이트된 메타데이터를 전송합니다.

* 요청 처리기 클래스는 다음과 같습니다 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* 요청 URL은 입니다.*1.x 콘텐츠의 기본 URL*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

메타데이터 변환은 서버가 클라이언트로부터 이전 메타데이터를 수신할 때 즉시 수행할 수 있습니다. 또는 서버가 이전 콘텐츠를 사전 처리하고 변환된 메타데이터를 저장할 수 있습니다. 이 경우 클라이언트가 새 메타데이터를 요청하면 서버는 이전 메타데이터의 라이선스 식별자와 일치하는 새 메타데이터를 가져오기만 하면 됩니다.

메타데이터를 변환하려면 서버는 다음 단계를 수행해야 합니다.

* Get `LiveCycleKeyMetaData`. 메타데이터를 미리 변환하려면 `LiveCycleKeyMetaData` 를 사용하여 1.x 패키지된 파일에서 가져올 수 있습니다. `MediaEncrypter.examineEncryptedContent()`. 메타데이터는 메타데이터 변환 요청에도 포함됩니다( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* 이전 메타데이터에서 라이센스 식별자를 가져와 암호화 키 및 정책(이 정보는 원래 Adobe LiveCycle ES 데이터베이스에 있음)을 찾습니다. LiveCycle ES 정책을 Adobe 액세스 2.0 정책으로 변환해야 합니다.) 참조 구현에는 정책을 변환하고 LiveCycle ES에서 라이선스 정보를 내보내기 위한 스크립트 및 샘플 코드가 포함되어 있습니다.
* 다음을 입력합니다. `V2KeyParameters` 객체(호출하여 검색) `MediaEncrypter.getKeyParameters()`).
* 을(를) 로드합니다 `SigningCredential`: 암호화 메타데이터 서명에 사용되는 Adobe에서 발급한 패키지 자격 증명입니다. 가져오기 `SignatureParameters` 를 호출한 개체 `MediaEncrypter.getSignatureParameters()` 서명 자격 증명을 입력합니다.
* 호출 `MetaDataConverter.convertMetadata()` 을(를) 가져오려면 `V2ContentMetaData`.
* 호출 `V2ContentMetaData.getBytes()` 나중에 사용하거나 전화를 위해 저장 `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
