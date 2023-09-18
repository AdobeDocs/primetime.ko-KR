---
title: 모니터링
description: 모니터링
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 모니터링{#monitoring}

개별화 서버와 키 생성 서버에는 각각 상태 페이지가 있으며, 이 페이지를 사용하여 서버의 상태를 확인할 수 있습니다.

* **개별화 상태 페이지:** [!DNL https://SERVER:PORT/flashaccess/status]

   * 앱 서버가 실행 중이고 앱이 키 생성 서버에 GET 요청을 할 수 있는 경우 &quot;활성&quot;으로 보고합니다
   * 페이지가 &quot;활성 상태&quot; 또는 &quot;없음&quot;을 보고합니다. 애플리케이션에 대한 정보가 표시되지 않으므로 이 페이지는 방화벽 외부에서 모니터링하는 데 사용할 수 있습니다.

* **키 생성 상태 페이지:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 앱 서버가 실행 중인 경우 &quot;활성&quot; 보고서
   * 모든 키 생성 URL은 내부적으로만 액세스할 수 있어야 합니다.

* **개별화 통계 페이지:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 제공된 요청 수 및 캐시에서 사용할 수 있는 키 수와 같은 개별화 서버에 대한 통계를 포함합니다
   * 이 페이지는 내부적으로만 액세스할 수 있어야 합니다.

* **키 생성 통계 페이지:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 제공되는 요청 수 및 디스크에서 사용할 수 있는 키 파일 수와 같은 키 생성 서버에 대한 통계를 포함합니다
   * 모든 키 생성 URL은 내부적으로만 액세스할 수 있어야 합니다.
