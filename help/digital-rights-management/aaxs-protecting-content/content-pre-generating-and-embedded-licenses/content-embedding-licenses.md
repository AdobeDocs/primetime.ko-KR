---
seo-title: 라이선스 포함
title: 라이선스 포함
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 라이선스 포함 {#embedding-licenses}

컨텐츠가 암호화되고 라이센스가 사전 생성되면 라이센스가 암호화된 컨텐츠에 포함될 수 있습니다.

라이센스를 포함하려면 인스턴스 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`를 가져옵니다. 암호화된 컨텐츠의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 `F4VKeyMetaDataUpdater`;그렇지 않은 경우, 검색된 파일 유형을 기준으로 인스턴스 `MediaProcessorFactory.getMediaProcessor()` 를 반환하는 데 사용합니다. Construction a `KeyMetaDataCallback` and invoke `modifyKeyMetaData()`. DRM 메타데이터가 암호화된 내용에 있으면 콜백 구현이 호출됩니다. 검색된 메타데이터를 기반으로 임베드할 라이센스를 선택하고 라이센스를 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`

임베디드 라이센스를 시연하는 샘플 코드는 참조 구현 명령줄 도구 &quot;샘플&quot; 디렉토리 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 에서 참조하십시오.

>[!NOTE]
>
>Adobe 액세스 2.0 클라이언트는 컨텐츠에 임베드된 모든 라이센스를 무시하고 메타데이터에 지정된 라이센스 서버에서 라이센스를 얻으려고 시도합니다. 그러나 메타데이터에 사용 가능한 라이센스 서버가 없다는 메시지가 표시되면 Adobe Access 2.0 클라이언트를 업그레이드하여 컨텐츠를 확인해야 합니다.

대역 [외 라이선스를 참조하십시오](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
