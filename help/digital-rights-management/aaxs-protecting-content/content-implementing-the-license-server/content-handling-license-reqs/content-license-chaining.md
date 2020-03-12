---
seo-title: 라이선스 체인
title: 라이선스 체인
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 체인{#license-chaining}

라이센스 체인을 생성하는 데 사용된 정책이 라이센스 체인을 지원하는 경우 서버는 리프 라이센스, 루트 라이센스 또는 둘 다를 발행할지 여부를 결정해야 합니다. 정책에 루트 라이센스가 있는지 여부를 결정하기 위해 정책에서 지원하는 라이선스 유형을 `Policy.getLicenseChainType()`결정하거나, 사용하거나, `Policy.getRootLicenseId()` 호출할 수 있습니다. Adobe Access 2.0 라이센스 체인을 사용하면 일반적으로 서버는 사용자가 처음 특정 컴퓨터에 대한 라이센스를 요청하고 이후 루트 라이센스를 요청할 때 리프 라이센스를 발행합니다. 컴퓨터에 이미 지정된 정책에 대한 리프 라이선스가 있는지 확인하려면 을(를) `LicenseRequestMessage.clientHasLeafForPolicy()`호출합니다.
