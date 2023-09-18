---
title: 문제 해결
description: 문제 해결
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 문제 해결{#troubleshooting}

* API 레벨 10 이상을 실행 중인 일부 이전 디바이스의 경우, logcat은 권한 문제로 인해 로그 디바이스를 열 수 없습니다. 다음 예외가 나타납니다. `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **해결 방법:**

   1. 열기 [!DNL AndroidManifest.xml] 다음 아래에 [!DNL CatalogActivity] 작업 공간의 프로젝트입니다.

   1. 에 다음 권한 추가 [!DNL `AndroidManfest.xml`] 파일:

      ```
      android.permission.READ_LOGS
      ```
