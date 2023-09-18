---
title: 오프라인 재생을 위한 사전 로드 라이선스 개요
description: 오프라인 재생을 위한 사전 로드 라이선스 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 오프라인 재생을 위한 라이선스 미리 로드 {#pre-loading-licenses-for-offline-playback}

Primetime DRM으로 보호된 콘텐츠를 재생하는 데 필요한 라이선스를 미리 로드할 수 있습니다. 사전 로드된 라이선스를 사용하면 활성 인터넷 연결 여부에 관계없이 콘텐츠를 볼 수 있습니다.

사전 로드 프로세스 자체 *다음과 같음* 인터넷 연결이 필요합니다. 다음을 사용할 수 있습니다. `DRMManager.loadVoucher()` 라이센스를 미리 로드할 수 있습니다. 이후, 클라이언트가 원하는 콘텐츠를 재생하고자 할 때, DRM 시스템은 미리 프라이밍되어 보호되는 콘텐츠를 즉시 재생할 수 있다.
