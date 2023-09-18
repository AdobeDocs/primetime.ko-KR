---
title: 클라이언트 자격 증명 취소
description: 클라이언트 자격 증명 취소
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 클라이언트 자격 증명 취소{#revoking-client-credentials}

특정 조건에서 클라이언트의 자격 증명을 취소하거나 지정된 자격 증명 세트가 이미 취소되었는지 확인해야 합니다. 자격 증명이 손상된 경우 자격 증명이 취소될 수 있습니다. 이 경우 손상된 클라이언트에게는 더 이상 라이선스가 발급되지 않습니다.

Adobe은 손상된 클라이언트를 해지하기 위해 CRL(인증서 해지 목록)을 유지 관리합니다. 이러한 CRL은 SDK에 의해 자동으로 적용됩니다. 라이센스 서버는 특정 컴퓨터 자격 증명 또는 DRM 및 런타임 자격 증명의 특정 버전을 허용하지 않음으로써 클라이언트를 추가로 제한할 수 있습니다. A `RevocationList` 를 만든 후 SDK에 전달하여 컴퓨터 자격 증명을 취소할 수 있습니다. 특정 DRM/런타임 버전은 정책 수준에서(재생 권한에서 모듈 제한을 설정하여) 해지할 수도 있고, 전역적으로(에서 모듈 제한을 설정하여) 해지할 수도 있습니다. `HandlerConfiguration`).

이 장에서는 클라이언트 자격 증명 취소를 중심으로 논의합니다.
