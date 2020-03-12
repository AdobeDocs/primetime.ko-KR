---
seo-title: CRL을 생성하여 Adobe에서 게시한 CRL을 보완합니다.
title: CRL을 생성하여 Adobe에서 게시한 CRL을 보완합니다.
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# CRL을 생성하여 Adobe에서 게시한 CRL을 보완합니다.{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access를 사용하면 CRL을 만들어 Adobe에서 게시한 시스템 CRL을 보완할 수 있습니다. Adobe Access SDK는 Adobe CRL을 확인하고 적용하지만 추가 시스템 자격 증명을 취소하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 이렇게 하려면 CRL을 Adobe Access SDK로 전달해야 합니다. 그런 다음 라이센스를 발급할 때 SDK가 Adobe CRL과 사용자의 CRL을 모두 확인합니다.

CRL 생성에 대한 자세한 내용은 Adobe Access API `RevocationListFactory` Reference *를 참조하십시오*.
