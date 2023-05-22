---
title: 개요
description: 개요
copied-description: true
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 개요{#overview}

클라이언트의 자격 증명을 취소하거나 특정 조건에서 지정된 자격 증명 세트가 이미 취소되었는지 확인해야 할 수 있습니다. 자격 증명이 손상되는 경우 자격 증명이 취소될 수 있습니다. 이러한 문제가 발생하면 손상된 클라이언트에게 더 이상 라이선스가 발급되지 않습니다.

Adobe은 손상된 클라이언트를 해지하기 위해 CRL(인증서 해지 목록)을 유지 관리합니다. 이러한 CRL은 SDK에 의해 자동으로 적용됩니다. 라이센스 서버는 특정 컴퓨터 자격 증명 또는 DRM 및 런타임 자격 증명의 특정 버전을 허용하지 않음으로써 클라이언트를 추가로 제한할 수 있습니다. A `RevocationList` 를 만든 후 SDK에 전달하여 컴퓨터 자격 증명을 취소할 수 있습니다. 특정 DRM/런타임 버전은 재생 권한에서 모듈 제한을 설정하여 DRM 정책 수준에서 해지하거나 `HandlerConfiguration`.

논의는 클라이언트 자격 증명 취소에 중점을 둡니다.
