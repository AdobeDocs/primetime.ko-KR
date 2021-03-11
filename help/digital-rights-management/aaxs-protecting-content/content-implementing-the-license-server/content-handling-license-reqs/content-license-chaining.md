---
title: 라이선스 체인
description: 라이선스 체인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 라이선스 체인{#license-chaining}

라이센스 체인을 생성하는 데 사용된 정책이 라이센스 체인을 지원하는 경우 서버는 리프 라이센스, 루트 라이센스 또는 둘 다를 발급할지 여부를 결정해야 합니다. 정책에 지원되는 라이선스 체인 유형을 결정하려면 `Policy.getLicenseChainType()`을 사용하거나 `Policy.getRootLicenseId()`을 호출하여 정책에 루트 라이센스가 있는지 확인합니다. Adobe Access 2.0 라이선스 체인으로 인해 서버는 일반적으로 사용자가 특정 컴퓨터에 대한 라이선스를 처음 요청할 때 리프 라이센스를 발급하고 이후 루트 라이센스를 요청합니다. 컴퓨터에 지정된 정책에 대한 리프 라이선스가 이미 있는지 확인하려면 `LicenseRequestMessage.clientHasLeafForPolicy()`을(를) 호출하십시오.
