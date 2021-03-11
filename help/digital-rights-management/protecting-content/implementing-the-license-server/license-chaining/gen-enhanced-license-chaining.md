---
title: 향상된 라이선스 체인
description: 향상된 라이선스 체인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 향상된 라이선스 체인 {#enhanced-license-chaining}

DRM 정책을 사용하여 라이선스 체인을 지원하는 라이선스를 생성하는 경우 서버는 리프 라이선스, 루트 라이선스 또는 둘 다를 발급할지 여부를 결정해야 합니다. DRM 정책이 지원하는 라이선스 체인 유형을 결정하려면 `Policy.getLicenseChainType()`을 사용하거나 `Policy.getRootLicenseId()`을(를) 호출하여 DRM 정책에 루트 라이센스가 있는지 확인합니다. Adobe Primetime DRM 2.0 라이선스 체인으로 인해 서버는 일반적으로 사용자가 특정 컴퓨터에 대한 라이선스를 처음 요청했을 때 리프 라이센스를 발급하고 이후 루트 라이센스를 요청합니다. 컴퓨터에 지정된 정책에 대한 리프 라이선스가 이미 있는지 확인하려면 `LicenseRequestMessage.clientHasLeafForPolicy()`을(를) 호출해야 합니다.

Adobe Primetime DRM 3.0의 향상된 라이선스 체인에서는 사용자가 처음으로 특정 컴퓨터에 대한 라이선스를 요청할 때 리프와 루트를 모두 실행하는 것이 좋습니다. 사용자가 이미 루트 라이선스를 보유하고 있는 경우 서버는 리프(클라이언트가 이미 3.0 향상된 루트를 보유하고 있는지 확인하기 위해 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()`을(를) 호출함)만 발행할 수 있습니다. 이후 라이센스 요청의 경우 클라이언트는 리프 및 루트가 이미 있음을 나타내므로 서버가 새 루트 라이센스를 발급해야 합니다. 향상된 라이선스 체인을 사용하는 경우 DRM 정책의 루트 암호화 키를 해독하는 데 필요한 자격 증명을 제공하려면 `setRootKeyRetrievalInfo()`을(를) 호출해야 합니다.

>[!NOTE]
>
>정책이 3.0 고급 라이선스 체인을 지원하지만 클라이언트가 Primetime DRM 2.0인 경우 서버는 원래 연결된 2.0 라이선스를 발행합니다. 클라이언트 버전을 확인하려면 `LicenseRequestMessage.getClientVersion()`을(를) 사용합니다.

