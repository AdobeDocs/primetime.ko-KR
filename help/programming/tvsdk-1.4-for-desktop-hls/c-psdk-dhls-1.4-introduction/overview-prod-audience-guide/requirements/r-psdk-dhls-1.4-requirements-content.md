---
description: DRM 암호화 키를 포함하여 스트림 및 재생 목록(매니페스트)에 대한 제한 및 요구 사항을 확인하십시오.
title: 컨텐츠 및 매니페스트 요구 사항
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 컨텐츠 및 매니페스트 요구 사항 {#content-and-manifest-requirements}

DRM 암호화 키를 포함하여 스트림 및 재생 목록(매니페스트)에 대한 제한 및 요구 사항을 확인하십시오.

| 포함 및 설정 `RESOLUTION` 매니페스트 파일의 각 ABR 스트림에 대한 속성입니다. Flash Player 14 이상을 사용해야 합니다. |
|---|
| DRM 보호 스트림이 MBR(Multiple Bit Rate)인 경우, MBR에 사용되는 DRM 암호화 키는 모든 비트 레이트 스트림에서 사용되는 키와 동일해야 한다. |
| 기본 콘텐츠 렌디션과 동일한 비트율 렌디션을 가져야 합니다. |
