---
seo-title: 문제 해결
title: 문제 해결
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 문제 해결{#troubleshooting}

* API 수준 10 이상을 실행하는 일부 이전 장치의 경우 권한 문제로 인해 로그 장치를 열 수 없습니다. 다음과 같은 예외가 나타납니다.해결방법 `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **:**

   1. 작업 [!DNL AndroidManifest.xml] 영역의 [!DNL CatalogActivity] 프로젝트 아래에서 엽니다.

   1. 다음 권한을 [!DNL `AndroidManfest.xml`] 파일에 추가합니다.

      ```
      android.permission.READ_LOGS
      ```
