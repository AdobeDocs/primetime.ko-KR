---
seo-title: 라이선스 포함
title: 라이선스 포함
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 포함 {#embedding-licenses}

컨텐츠가 암호화되어 라이센스가 사전 생성되면 라이센스가 암호화된 컨텐츠에 포함될 수 있습니다.

라이센스를 임베드하려면 의 인스턴스를 얻어야 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`합니다. 암호화된 컨텐츠의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 를 위한 생성자를 `F4VKeyMetaDataUpdater`사용하십시오.그렇지 않으면 검색된 파일 유형을 기반으로 인스턴스를 반환하는 `MediaProcessorFactory.getMediaProcessor()` 데 사용합니다. 그런 다음 `KeyMetaDataCallback` 를 구조화하고 호출해야 `modifyKeyMetaData()`합니다. 그런 다음 DRM 메타데이터가 암호화된 내용에 있을 때 콜백 구현이 호출됩니다. 검색된 메타데이터를 기반으로 임베드할 라이선스를 선택하고 를 사용하여 라이센스를 설정할 수 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`있습니다.

포함된 라이선스를 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 보여 주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL Samples] 디렉토리에서 을 참조하십시오.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Adobe Primetime DRM 2.0 클라이언트는 컨텐츠에 포함된 모든 라이센스를 무시하고 메타데이터에 지정된 라이센스 서버로부터 라이센스를 얻으려고 시도합니다. 그러나 메타데이터가 사용 가능한 라이센스 서버가 없음을 나타내는 경우 Primetime DRM 2.0 클라이언트를 업그레이드해야 컨텐츠를 볼 수 있습니다.

