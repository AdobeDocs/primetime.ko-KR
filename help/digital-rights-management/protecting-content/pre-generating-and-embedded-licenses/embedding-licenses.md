---
title: 라이선스 포함
description: 라이선스 포함
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 라이선스 포함 {#embedding-licenses}

콘텐츠가 암호화되고 라이센스가 미리 생성되면, 라이센스는 암호화된 콘텐츠에 임베드될 수 있다.

라이센스를 포함하려면 의 인스턴스를 가져와야 합니다. `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. 암호화된 콘텐츠의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 `F4VKeyMetaDataUpdater`; 그렇지 않으면 `MediaProcessorFactory.getMediaProcessor()` 검색된 파일 형식을 기반으로 인스턴스를 반환합니다. 그런 다음 를 구성해야 합니다. `KeyMetaDataCallback` 및 호출 `modifyKeyMetaData()`. 그런 다음 DRM 메타데이터가 암호화된 콘텐츠에 있는 경우 콜백 구현이 호출됩니다. 검색된 메타데이터를 기반으로 임베드할 라이선스를 선택하고 다음을 사용하여 라이선스를 설정할 수 있습니다. `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

다음을 참조하십시오 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` 참조 구현 명령줄 도구 [!DNL Samples] 포함된 라이선스를 보여 주는 샘플 코드에 대한 디렉터리입니다.

>[!NOTE]
>
>Adobe Primetime DRM 2.0 클라이언트는 콘텐츠에 포함된 모든 라이선스를 무시한 다음 메타데이터에 지정된 라이선스 서버에서 라이선스를 획득하려고 합니다. 그러나 메타데이터에 사용 가능한 라이선스 서버가 없다는 메시지가 표시되면 콘텐츠를 보기 전에 Primetime DRM 2.0 클라이언트를 업그레이드해야 합니다.
