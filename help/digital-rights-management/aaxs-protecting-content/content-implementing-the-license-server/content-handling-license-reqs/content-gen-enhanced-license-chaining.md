---
seo-title: 향상된 라이센스 체인
title: 향상된 라이센스 체인
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# 향상된 라이센스 체인 {#enhanced-license-chaining}

Adobe Access 3.0의 향상된 라이선스 체인을 사용하면 사용자가 처음으로 특정 컴퓨터에 대한 라이선스를 요청할 때 리프와 루트를 모두 발행하는 것이 좋습니다. 사용자가 이미 루트 라이선스를 보유하고 있는 경우 서버는 Leaf만 발행할 수 있습니다(클라이언트에 이미 3.0 향상된 루트가 있는지 확인하기 `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` 위해 호출). 이후 라이선스 요청의 경우 클라이언트는 이미 Leaf 및 Root를 가지고 있음을 표시하므로 서버가 새 루트 라이센스를 발급해야 합니다. 향상된 라이센스 체인이 사용되는 경우 정책에서 루트 암호화 키를 해독하는 데 필요한 자격 증명을 제공하도록 `setRootKeyRetrievalInfo()` 호출되어야 합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>정책에서 3.0 고급 라이센스 체인을 지원하지만 클라이언트가 Adobe Access 2.0인 경우 서버는 2.0 원본 체인 라이센스를 발행합니다. 클라이언트 버전을 확인하려면 LicenseRequestMessage.getClientVersion()을 사용하십시오.

