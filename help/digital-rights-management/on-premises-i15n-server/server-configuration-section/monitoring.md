---
title: 모니터링
description: 모니터링
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 모니터링{#monitoring}

Indification Server 및 Key Generation Server에는 각각 서버의 상태를 확인하는 데 사용할 수 있는 상태 페이지가 있습니다.

* **개인화 상태 페이지:** [!DNL https://SERVER:PORT/flashaccess/status]

   * 앱 서버가 실행 중이며 앱이 키 생성 서버에 GET 요청을 할 수 있는 경우 &quot;Alive&quot;를 보고합니다
   * 이 페이지는 &quot;Alive&quot;나 아무 것도 보고하지 않습니다. 응용 프로그램에 대한 정보가 표시되지 않으므로 이 페이지는 방화벽 외부에서 모니터링할 수 있습니다.

* **키 생성 상태 페이지:** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 앱 서버가 실행 중인 경우 &quot;Alive&quot;를 보고합니다.
   * 모든 키 생성 URL은 내부적으로만 액세스할 수 있어야 합니다.

* **개인화 통계 페이지:** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 제공된 요청 수 및 캐시에서 사용 가능한 키 수와 같은 개인화 서버에 대한 통계를 포함합니다
   * 이 페이지는 내부적으로만 액세스할 수 있어야 합니다.

* **주요 생성 통계 페이지:** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 제공된 요청 수 및 디스크에서 사용할 수 있는 주요 파일 수와 같은 키 생성 서버에 대한 통계를 포함합니다.
   * 모든 키 생성 URL은 내부적으로만 액세스할 수 있어야 합니다.

