---
title: 문제 해결
description: 문제 해결
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
