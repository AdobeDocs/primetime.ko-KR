---
title: 향상된 라이선스 체인
description: 향상된 라이선스 체인
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 향상된 라이선스 체인 {#enhanced-license-chaining}

DRM 정책을 사용하여 라이센스 체인을 지원하는 라이센스를 생성하는 경우 서버는 Leaf 라이센스 또는 Root 라이센스 중 하나를 발행할지 또는 둘 다를 발행할지 여부를 결정해야 합니다. DRM 정책이 지원하는 라이선스 유형을 결정하려면 다음을 사용해야 합니다 `Policy.getLicenseChainType()`또는 호출 `Policy.getRootLicenseId()` DRM 정책에 루트 라이센스가 있는지 확인합니다. Adobe Primetime DRM 2.0 라이센스 체인을 사용하면 일반적으로 서버는 사용자가 특정 컴퓨터에 대한 라이센스를 처음 요청할 때 리프 라이센스를 발행하고 그 후에 루트 라이센스를 발행합니다. 컴퓨터에 지정된 정책에 대한 리프 라이선스가 이미 있는지 확인하려면 을(를) 호출해야 합니다. `LicenseRequestMessage.clientHasLeafForPolicy()`.

Adobe Primetime DRM 3.0의 향상된 라이센스 체인을 사용하면 사용자가 특정 컴퓨터에 대한 라이센스를 처음 요청할 때 Leaf와 Root를 모두 실행하는 것이 좋습니다. 사용자가 이미 루트 라이선스를 가지고 있는 경우 서버는 Leaf(호출)만 발급할 수 있습니다. `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 를 사용하여 클라이언트에 이미 3.0 Enhanced Root가 있는지 확인합니다. 그런 다음 후속 라이센스 요청의 경우 클라이언트는 이미 Leaf 및 Root가 있으므로 서버에서 새 Root 라이센스를 발행해야 함을 나타냅니다. 향상된 라이선스 체인이 사용되는 경우, `setRootKeyRetrievalInfo()` drm 정책에서 루트 암호화 키를 해독하는 데 필요한 자격 증명을 제공하기 위해 를 호출해야 합니다.

>[!NOTE]
>
>정책이 3.0 향상된 라이센스 체인을 지원하지만 클라이언트가 Primetime DRM 2.0인 경우 서버는 2.0 원본 체인 라이센스를 발행합니다. 클라이언트 버전을 확인하려면 다음을 사용하십시오. `LicenseRequestMessage.getClientVersion()`.
