---
title: 라이선스 체인
description: 라이선스 체인
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 라이선스 체인{#license-chaining}

라이선스 생성에 사용된 정책이 라이선스 체인 기능을 지원하는 경우 서버는 Leaf 라이선스, Root 라이선스 또는 둘 다 발급할지 여부를 결정해야 합니다. 정책이 지원하는 라이선스 유형을 확인하려면 `Policy.getLicenseChainType()`또는 호출 `Policy.getRootLicenseId()` 정책에 루트 라이선스가 있는지 확인합니다. Adobe 액세스 2.0 라이선스 체인을 사용하면 일반적으로 서버는 사용자가 특정 컴퓨터에 대한 라이선스를 처음 요청할 때 리프 라이선스를 발급하고 그 후 루트 라이선스를 발급합니다. 컴퓨터에 지정된 정책에 대한 리프 라이선스가 이미 있는지 확인하려면 을(를) 호출합니다. `LicenseRequestMessage.clientHasLeafForPolicy()`.
