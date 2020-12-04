---
seo-title: 문제 해결
title: 문제 해결
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# 문제 해결{#troubleshooting}

* API 수준 10 이상을 실행 중인 일부 이전 장치의 경우 권한 문제로 인해 로그 장치를 열 수 없습니다. 다음 예외가 나타납니다.`java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **해결 방법:**

   1. 작업 공간의 [!DNL CatalogActivity] 프로젝트 아래에 있는 [!DNL AndroidManifest.xml]을 엽니다.

   1. 다음 권한을 [!DNL `AndroidManfest.xml`] 파일에 추가합니다.

      ```
      android.permission.READ_LOGS
      ```
