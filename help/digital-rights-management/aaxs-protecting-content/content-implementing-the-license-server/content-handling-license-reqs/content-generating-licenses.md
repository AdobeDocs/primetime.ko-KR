---
seo-title: 라이선스 생성
title: 라이선스 생성
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 생성 {#generating-licenses}

사용자에게 리프 라이선스를 발행하려면 SDK가 컨텐츠 메타데이터에 포함된 CEK의 암호를 해독하여 라이선스를 요청하는 시스템에 맞게 다시 암호화해야 합니다. CEK를 해독하려면 서버가 키를 해독하는 데 필요한 정보를 제공해야 합니다. 호출하고 `ContentInfo.setKeyRetrievalInfo()` 개체를 `AsymmetricKeyRetrieval` 제공합니다. 메타데이터에 여러 정책이 포함되어 있는 경우 서버에서 사용하고 호출할 정책을 결정해야 합니다 `LicenseRequestMessage.setSelectedPolicy()`. 그런 `LicenseRequestMessage.generateLicense()` 다음 전화를 걸어 라이센스를 생성합니다. 반환되는 `License` 객체를 사용하면 라이센스의 만료 또는 권한을 수정할 수 있습니다.

개체에 ExternalKeyRetrieval 객체가 지정된 경우 라이선스 서버는 관련 CEK ID를 사용하여 라이센스에 삽입될 적절한 CEK를 가져오게 됩니다. `ContentInfo` 외부 CEK 작업 과정 사용 방법에 대한 자세한 내용은 Adobe Access DRM [외부 CEK 개요를 참조하십시오.](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
