---
title: Adobe에 의해 게시된 CRL을 보완하는 CRL 생성
description: Adobe에 의해 게시된 CRL을 보완하는 CRL 생성
copied-description: true
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Adobe에 의해 게시된 CRL을 보완하는 CRL 생성{#generate-crls-to-supplement-those-published-by-adobe}

Adobe 액세스를 사용하면 Adobe에 의해 게시된 컴퓨터 CRL을 보완하는 CRL을 생성할 수 있습니다. Adobe 액세스 SDK가 Adobe CRL을 확인하고 적용하지만, 추가 컴퓨터 자격 증명을 취소하는 CRL을 만들어 추가 클라이언트 컴퓨터를 허용하지 않을 수 있습니다. 이렇게 하려면 CRL을 Adobe 액세스 SDK에 전달해야 합니다. 그런 다음 라이선스를 발급할 때 SDK는 Adobe CRL과 자체 CRL을 모두 확인합니다.

CRL 생성에 대한 자세한 내용은 `RevocationListFactory` 위치: *Adobe 액세스 API 참조*.
