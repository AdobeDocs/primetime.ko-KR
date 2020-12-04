---
seo-title: 오프라인 재생을 위한 라이선스 미리 로드 개요
title: 오프라인 재생을 위한 라이선스 미리 로드 개요
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 오프라인 재생을 위한 라이선스 사전 로드{#pre-loading-licenses-for-offline-playback}

Primetime DRM으로 보호되는 콘텐츠를 재생하는 데 필요한 라이선스를 미리 로드할 수 있습니다. 사전 로드된 라이선스를 통해 사용자는 인터넷에 연결되어 있는지 여부에 상관없이 컨텐츠를 볼 수 있습니다.

미리 로드 프로세스 자체에는 *이(가) 인터넷 연결이 필요합니다.* 미리 `DRMManager.loadVoucher()`을(를) 사용하여 라이선스를 미리 로드할 수 있습니다. 나중에 클라이언트가 원하는 컨텐츠를 재생하려고 할 때 DRM 시스템이 사전 지정되어 보호된 컨텐츠를 즉시 재생할 수 있습니다.
