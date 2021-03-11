---
title: 문제 해결
description: 문제 해결
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# 문제 해결{#troubleshooting}

* API 수준 10 이상을 실행 중인 일부 이전 장치의 경우 권한 문제로 인해 logcat가 로그 장치를 열 수 없습니다. 다음과 같은 예외가 나타납니다.`java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **해결 방법:**

   1. 작업 영역의 [!DNL CatalogActivity] 프로젝트 아래에 있는 [!DNL AndroidManifest.xml]을(를) 엽니다.

   1. [!DNL `AndroidManfest.xml`] 파일에 다음 권한을 추가합니다.

      ```
      android.permission.READ_LOGS
      ```
