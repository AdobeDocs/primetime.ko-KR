---
description: DRM 암호화 키를 비롯한 스트림 및 재생 목록(매니페스트)에 대한 제한 사항과 요구 사항을 확인합니다.
seo-description: DRM 암호화 키를 비롯한 스트림 및 재생 목록(매니페스트)에 대한 제한 사항과 요구 사항을 확인합니다.
seo-title: 콘텐츠 및 매니페스트 요구 사항
title: 콘텐츠 및 매니페스트 요구 사항
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 콘텐츠 및 매니페스트 요구 사항 {#content-and-manifest-requirements}

DRM 암호화 키를 비롯한 스트림 및 재생 목록(매니페스트)에 대한 제한 사항과 요구 사항을 확인합니다.

| 매니페스트 파일에 있는 각 ABR 스트림에 대해 `RESOLUTION` 속성을 포함 및 설정합니다. Flash Player 14 이상을 사용해야 합니다. |
|---|
| DRM으로 보호되는 스트림이 여러 비트 전송률(MBR)인 경우 MBR에 사용되는 DRM 암호화 키는 모든 비트율 스트림에 사용되는 키와 동일해야 합니다. |
| 기본 컨텐츠의 표현물과 동일한 비트 전송률 변환이 있어야 합니다. |