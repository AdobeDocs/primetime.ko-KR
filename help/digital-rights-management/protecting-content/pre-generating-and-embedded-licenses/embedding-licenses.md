---
title: 라이선스 포함
description: 라이선스 포함
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 라이선스 포함 {#embedding-licenses}

컨텐츠가 암호화되어 있고 라이선스가 사전 생성된 경우 라이선스는 암호화된 컨텐츠에 포함될 수 있습니다.

라이센스를 포함하려면 `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater` 인스턴스를 구해야 합니다. 암호화된 내용의 유형을 알고 있는 경우 `FLVKeyMetaDataUpdater` 또는 `F4VKeyMetaDataUpdater`;의 생성자를 사용하십시오.그렇지 않으면 검색된 파일 유형에 따라 인스턴스를 반환하려면 `MediaProcessorFactory.getMediaProcessor()`를 사용합니다. 그런 다음 `KeyMetaDataCallback`을(를) 구성하고 `modifyKeyMetaData()`을(를) 호출해야 합니다. 그러면 DRM 메타데이터가 암호화된 내용에 있을 때 콜백 구현이 호출됩니다. 찾은 메타데이터를 기반으로 임베드할 라이선스를 선택하고 `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`을 사용하여 라이센스를 설정할 수 있습니다.

포함된 라이선스를 보여 주는 샘플 코드는 참조 구현 명령줄 도구 [!DNL Samples] 디렉토리의 `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense`을 참조하십시오.

>[!NOTE]
>
>Adobe Primetime DRM 2.0 클라이언트는 컨텐츠에 포함된 모든 라이센스를 무시하고 메타데이터에 지정된 라이센스 서버에서 라이센스를 얻으려고 합니다. 그러나 메타데이터에 사용 가능한 라이센스 서버가 없다는 메시지가 표시되면 콘텐츠를 보기 전에 Primetime DRM 2.0 클라이언트를 업그레이드해야 합니다.

