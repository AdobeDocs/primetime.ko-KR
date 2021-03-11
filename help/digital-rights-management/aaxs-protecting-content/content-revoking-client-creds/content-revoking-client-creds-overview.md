---
title: 클라이언트 자격 증명을 취소하는 중
description: 클라이언트 자격 증명을 취소하는 중
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 클라이언트 자격 증명을 취소하는 중{#revoking-client-credentials}

특정 조건 하에서 클라이언트의 자격 증명을 취소하거나 지정된 자격 증명 세트가 이미 해지되었는지 확인해야 합니다. 자격 증명이 손상되면 자격 증명을 취소할 수 있습니다. 이러한 경우 악용된 고객에게 라이선스가 더 이상 발급되지 않습니다.

Adobe은 손상된 클라이언트를 취소하기 위해 CRL(인증서 해지 목록)을 유지합니다. 이러한 CRL은 SDK에 의해 자동으로 적용됩니다. 라이센스 서버는 특정 컴퓨터 자격 증명 또는 특정 버전의 DRM 및 런타임 자격 증명을 허용하지 않아 클라이언트를 추가로 제한할 수 있습니다. 시스템 자격 증명을 취소하려면 `RevocationList`을(를) 만들어 SDK에 전달할 수 있습니다. 특정 DRM/런타임 버전은 정책 수준(재생 오른쪽의 모듈 제한을 설정) 또는 전역적(`HandlerConfiguration`에서 모듈 제한 사항을 설정)에서 취소할 수 있습니다.

이 장의 토론은 클라이언트 자격 증명을 취소하는 것에 중점을 둡니다.
