---
title: 향상된 라이선스 체인
description: 향상된 라이선스 체인
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 향상된 라이선스 체인 {#enhanced-license-chaining}

Adobe 액세스 3.0에서 향상된 라이선스 체인을 사용하면 사용자가 특정 컴퓨터에 대한 라이선스를 처음 요청할 때 Leaf와 Root를 모두 실행하는 것이 좋습니다. 사용자가 이미 루트 라이선스를 가지고 있는 경우 서버는 Leaf(호출)만 발급할 수 있습니다. `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 를 사용하여 클라이언트에 이미 3.0 Enhanced Root가 있는지 확인합니다. 후속 라이센스 요청의 경우 클라이언트는 이미 Leaf 및 Root가 있음을 나타내므로 서버에서 새 Root 라이센스를 발급해야 합니다. 향상된 라이선스 체인이 사용되는 경우, `setRootKeyRetrievalInfo()` 정책에서 루트 암호화 키를 해독하는 데 필요한 자격 증명을 제공하기 위해 를 호출해야 합니다.

>[!NOTE]
>
>정책에서 3.0 향상된 라이선스 체인을 지원하지만 클라이언트가 Adobe 액세스 2.0인 경우 서버는 2.0 원본 체인 라이선스를 발급합니다. 클라이언트 버전을 확인하려면 LicenseRequestMessage.getClientVersion() 을 사용합니다.
