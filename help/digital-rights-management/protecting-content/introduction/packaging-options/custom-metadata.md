---
title: 사용자 정의 메타데이터
description: 사용자 정의 메타데이터
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 사용자 지정 메타데이터 {#custom-metadata}

서버 응용 프로그램에서 해석할 수 있는 내용 메타데이터에 사용자 정의 키/값 쌍을 추가하려면 이 매개 변수를 사용합니다.

Primetime DRM 콘텐츠의 메타데이터 형식을 사용하면 패키징 시 사용자 정의 키/값 쌍을 포함할 수 있습니다. 그런 다음 이 사용자 지정 메타데이터를 라이센스 발급 중에 라이센스 서버에서 처리할 수 있습니다. 메타데이터는 Primetime DRM 정책과는 별개이며 콘텐츠의 각 섹션에 대해 고유해야 합니다.

사용 사례 예:베타 단계 동안 패키징 시 사용자 지정 속성 `Release:BETA`을(를) 포함할 수 있습니다. 라이센스 서버는 베타 기간 동안 이 컨텐트에 대한 라이센스를 종료할 수 있습니다. 그러나 베타 기간이 만료된 후 라이센스 서버는 콘텐트에 대한 액세스를 허용하지 않습니다.
