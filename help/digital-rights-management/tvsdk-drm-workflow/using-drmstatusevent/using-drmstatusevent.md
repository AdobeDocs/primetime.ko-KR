---
title: DRMStatusEvent 클래스 개요 사용
description: DRMStatusEvent 클래스 개요 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# DRMStatusEvent 클래스 개요 사용 {#using-the-drmstatusevent-class-overview}

Primetime DRM으로 보호되는 콘텐츠의 재생이 성공적으로 시작되면 `DRMStatusEvent` 개체가 전달됩니다. (성공 시 라이선스가 확인되고 사용자가 인증되고 컨텐츠를 볼 수 있는 권한이 있음을 의미합니다.)

`DRMStatusEvent` 개체에는 라이센스를 오프라인으로 사용할 수 있는지, 라이센스가 만료되었는지에 따라 컨텐트를 더 이상 볼 수 없는지 등 라이센스와 관련된 정보가 포함되어 있습니다.
