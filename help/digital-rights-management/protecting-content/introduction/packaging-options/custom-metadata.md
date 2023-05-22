---
title: 사용자 지정 메타데이터
description: 사용자 지정 메타데이터
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 사용자 지정 메타데이터 {#custom-metadata}

서버 애플리케이션에서 해석할 수 있는 콘텐츠 메타데이터에 사용자 지정 키/값 쌍을 추가하려면 이 옵션을 사용합니다.

Primetime DRM 콘텐츠의 메타데이터 형식을 사용하면 패키징 시간에 사용자 지정 키/값 쌍을 포함할 수 있습니다. 그런 다음 라이선스 발행 중에 라이선스 서버에서 이 사용자 지정 메타데이터를 처리할 수 있습니다. 메타데이터는 Primetime DRM 정책과 별개이며, 컨텐츠의 각 섹션에 대해 고유할 수 있습니다.

예제 사용 사례: 베타 단계 동안 사용자 지정 속성을 포함할 수 있습니다 `Release:BETA` 포장 시간에. 라이선스 서버는 Beta 기간 동안 이 콘텐츠에 대한 라이선스를 무효화할 수 있습니다. 그러나 Beta 기간이 만료된 후 라이선스 서버는 콘텐츠에 대한 액세스를 허용하지 않습니다.
