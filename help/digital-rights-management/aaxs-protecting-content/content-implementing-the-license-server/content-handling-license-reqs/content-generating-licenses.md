---
seo-title: 라이선스 생성
title: 라이선스 생성
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# 라이선스 생성 중 {#generating-licenses}

사용자에게 리프 라이센스를 발급하려면 SDK가 컨텐츠 메타데이터에 포함된 CEK의 암호를 해독하여 라이센스를 요청하는 시스템에 맞게 다시 암호화해야 합니다. CEK를 해독하려면 서버는 키의 암호를 해독하는 데 필요한 정보를 제공해야 합니다. `ContentInfo.setKeyRetrievalInfo()`을(를) 호출하고 `AsymmetricKeyRetrieval` 개체를 제공합니다. 메타데이터에 여러 정책이 포함되어 있으면 서버에서 사용할 정책을 결정하고 `LicenseRequestMessage.setSelectedPolicy()`을(를) 호출해야 합니다. 그런 다음 `LicenseRequestMessage.generateLicense()`을(를) 호출하여 라이센스를 생성합니다. 반환되는 `License` 개체를 사용하면 라이센스의 만료 또는 권한을 수정할 수 있습니다.

`ContentInfo` 개체에 ExternalKeyRetrieval 개체가 지정된 경우 라이선스 서버는 관련 CEK ID를 사용하여 라이선스에 삽입될 해당 CEK를 가져올 것으로 예상됩니다. 외부 CEK 작업 과정 사용 방법에 대한 자세한 내용은 [Adobe 액세스 DRM 외부 CEK 개요](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)를 참조하십시오.
