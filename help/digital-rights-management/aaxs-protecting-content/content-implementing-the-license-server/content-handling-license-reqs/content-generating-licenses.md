---
title: 라이선스 생성 중
description: 라이선스 생성 중
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 라이선스 생성 중 {#generating-licenses}

사용자에게 리프 라이선스를 발급하려면 SDK는 콘텐츠 메타데이터에 포함된 CEK를 해독하고 라이선스를 요청하는 컴퓨터에 대해 다시 암호화해야 합니다. CEK를 해독하려면 서버에서 키를 해독하는 데 필요한 정보를 제공해야 합니다. 호출 `ContentInfo.setKeyRetrievalInfo()` 다음을 제공합니다. `AsymmetricKeyRetrieval` 개체. 메타데이터에 여러 정책이 포함된 경우 서버는 사용할 정책을 결정하고 호출해야 합니다 `LicenseRequestMessage.setSelectedPolicy()`. 그런 다음 를 호출합니다. `LicenseRequestMessage.generateLicense()` 라이센스를 생성합니다. 사용 `License` 반환되는 개체는 라이센스에서 만료 또는 권한을 수정할 수 있습니다.

ExternalKeyRetrieval 개체가 `ContentInfo` 그러면 라이센스 서버는 연관된 CEK ID를 사용하여 라이센스에 삽입될 적절한 CEK를 가져오게 됩니다. 외부 CEK 워크플로우 사용 방법에 대한 자세한 내용은 [Adobe 액세스 DRM 외부 CEK 개요](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
