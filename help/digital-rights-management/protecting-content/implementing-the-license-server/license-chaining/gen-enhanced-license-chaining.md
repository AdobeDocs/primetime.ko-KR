---
seo-title: 향상된 라이센스 체인
title: 향상된 라이센스 체인
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 향상된 라이센스 체인 {#enhanced-license-chaining}

DRM 정책을 사용하여 라이센스 체인을 지원하는 라이센스를 생성하는 경우 서버는 리프 라이센스, 루트 라이센스 또는 둘 다를 발행할지 여부를 결정해야 합니다. DRM 정책에서 지원하는 라이선스 유형을 결정하려면 DRM 정책에 루트 라이선스가 있는지 여부를 `Policy.getLicenseChainType()`사용하거나 `Policy.getRootLicenseId()` 호출해야 합니다. Adobe Primetime DRM 2.0 라이선스 체인을 사용하면 일반적으로 서버는 사용자가 처음 특정 시스템에 대한 라이선스와 이후 루트 라이선스를 요청할 때 리프 라이선스를 발행합니다. 컴퓨터에 지정된 정책에 대한 리프 라이선스가 이미 있는지 확인하려면 전화해야 `LicenseRequestMessage.clientHasLeafForPolicy()`합니다.

Adobe Primetime DRM 3.0의 향상된 라이선스 체인을 사용하면 사용자가 처음으로 특정 컴퓨터에 대한 라이선스를 요청할 때 Leaf와 Root를 모두 발행하는 것이 좋습니다. 사용자가 이미 루트 라이선스를 보유하고 있는 경우 서버는 Leaf만 발행할 수 있습니다(클라이언트에 이미 3.0 향상된 루트가 있는지 확인하기 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 위해 호출). 이후 라이센스 요청의 경우 클라이언트는 이미 Leaf 및 Root를 보유하고 있으므로 서버가 새 루트 라이센스를 발급해야 합니다. 향상된 라이선스 체인이 사용되는 경우 DRM 정책에서 루트 암호화 키를 해독하는 데 필요한 자격 증명을 제공하려면 `setRootKeyRetrievalInfo()` 호출해야 합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>정책에서 3.0 고급 라이선스 체인을 지원하지만 클라이언트가 Primetime DRM 2.0인 경우 서버는 2.0 원본 체인 라이센스를 발행합니다. 클라이언트 버전을 확인하려면 를 `LicenseRequestMessage.getClientVersion()`사용합니다.

