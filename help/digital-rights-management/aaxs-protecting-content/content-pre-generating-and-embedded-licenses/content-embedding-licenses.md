---
title: 라이선스 포함
description: 라이선스 포함
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 라이선스 포함 {#embedding-licenses}

콘텐츠가 암호화되고 라이센스가 미리 생성되면, 라이센스는 암호화된 콘텐츠에 임베드될 수 있다.

라이센스를 포함하려면 의 인스턴스를 가져옵니다. `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 암호화된 콘텐츠의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 `F4VKeyMetaDataUpdater`; 그렇지 않으면 `MediaProcessorFactory.getMediaProcessor()` 검색된 파일 형식을 기반으로 인스턴스를 반환합니다. 구문 `KeyMetaDataCallback` 및 호출 `modifyKeyMetaData()`. DRM 메타데이터가 암호화된 콘텐츠에 있는 경우 콜백 구현이 호출됩니다. 검색된 메타데이터를 기반으로 임베드할 라이선스를 선택하고 다음을 사용하여 라이선스를 설정할 수 있습니다. `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

임베드된 라이센스를 보여 주는 샘플 코드는 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 참조 구현 명령줄 도구 &quot;샘플&quot; 디렉토리에서

>[!NOTE]
>
>Adobe 액세스 2.0 클라이언트는 콘텐츠에 포함된 모든 라이선스를 무시하고 메타데이터에 지정된 라이선스 서버에서 라이선스를 얻으려고 시도합니다. 그러나 메타데이터에 사용 가능한 라이선스 서버가 없다는 메시지가 표시되면 Adobe 액세스 2.0 클라이언트를 업그레이드해야 콘텐츠를 볼 수 있습니다.

다음을 참조하십시오 [대역 외 라이선스](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
