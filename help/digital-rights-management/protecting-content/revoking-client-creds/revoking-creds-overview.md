---
seo-title: 개요
title: 개요
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 개요{#overview}

클라이언트의 자격 증명을 취소하거나 특정 조건 하에서 특정 자격 증명 세트가 이미 해지되었는지 확인해야 할 수 있습니다. 자격 증명이 손상되면 해지될 수 있습니다. 이러한 문제가 발생하면 손상된 클라이언트에 대한 라이선스가 더 이상 발행되지 않습니다.

Adobe는 CRL(Certificate Revocation Lists)을 유지 관리하여 훼손된 클라이언트를 취소합니다. 이러한 CRL은 SDK에 의해 자동으로 적용됩니다. 라이센스 서버는 특정 컴퓨터 자격 증명 또는 특정 버전의 DRM 및 런타임 자격 증명을 허용하지 않아 클라이언트를 추가로 제한할 수 있습니다. 시스템 자격 증명을 취소하기 위해 SDK에 를 만들어 전달할 `RevocationList` 수 있습니다. 특정 DRM/런타임 버전은 DRM 정책 수준에서 재생 권한 또는 에서 모듈 제한 사항을 설정하여 DRM 정책 수준에서 취소할 수 `HandlerConfiguration`있습니다.

토론은 클라이언트 자격 증명을 취소하는 것에 중점을 둡니다.
