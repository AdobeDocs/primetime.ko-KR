---
seo-title: 라이선스 포함
title: 라이선스 포함
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 라이선스 포함 {#embedding-licenses}

컨텐츠가 암호화되고 라이센스가 사전 생성되면 라이센스가 암호화된 컨텐츠에 포함될 수 있습니다.

라이선스를 포함하려면 해당 인스턴스를 얻어야 합니다 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 암호화된 컨텐츠의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 `F4VKeyMetaDataUpdater`;그렇지 않은 경우, 검색된 파일 유형을 기준으로 인스턴스 `MediaProcessorFactory.getMediaProcessor()` 를 반환하는 데 사용합니다. 그런 다음 A를 구조화하고 호출해야 `KeyMetaDataCallback` 합니다 `modifyKeyMetaData()`. 그러면 DRM 메타데이터가 암호화된 내용에 있을 때 콜백 구현이 호출됩니다. 검색된 메타데이터를 기반으로 임베드할 라이센스를 선택하고 라이센스를 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`

임베드된 라이선스 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 를 보여주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL Samples] 디렉토리에서 을 참조하십시오.

>[!NOTE]
>
>Adobe Primetime DRM 2.0 클라이언트는 컨텐츠에 포함된 모든 라이센스를 무시하고 메타데이터에 지정된 라이센스 서버에서 라이센스를 얻으려고 시도합니다. 그러나 메타데이터가 사용 가능한 라이센스 서버가 없음을 나타내는 경우 Primetime DRM 2.0 클라이언트를 업그레이드해야 컨텐츠를 볼 수 있습니다.

