---
description: HTTP GET 명령을 사용하여 매니페스트 서버와 상호 작용합니다.
title: 매니페스트 서버에 명령 보내기
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 매니페스트 서버에 명령 보내기 {#send-a-command-to-the-manifest-server}

HTTP GET 명령을 사용하여 매니페스트 서버와 상호 작용합니다.

1. 보내기 `HTTP GET` 다음 패턴을 사용하여 생성된 부트스트랩 URL에 대한 요청:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **게시자 자산 ID** 필수. 특정 콘텐츠에 대한 게시자의 고유 ID입니다.

* **컨텐츠 URL** 필수. 매니페스트 서버 URL 내에서 안전하도록 인코딩된 Base64인 콘텐츠 M3U8 파일의 URL입니다. 비트 전송률 스트림이 하나만 있는 경우에도 콘텐츠 URL은 변형 M3U8 파일을 가리켜야 합니다.

* **쿼리 매개 변수** 일부는 필수이고 일부는 선택 사항입니다. 이는 요청의 가장 다양한 부분을 구성합니다. 매니페스트 서버에는 어떤 종류의 클라이언트가 요청을 하고 있는지, 매니페스트 서버가 무엇을 하기를 원하는지 알려줍니다.

   예:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP 요청과 HTTPS 요청 비교**

   매니페스트 서버는 클라이언트 요청의 동일한 HTTP 프로토콜을 사용하여 URL을 만듭니다. 플레이어가 비보안 HTTP(http) 요청을 수행하면 매니페스트 서버는 http 프로토콜을 사용하여 매니페스트 URL 및 감사 추적 URL을 반환합니다. 플레이어가 보안 HTTP(https) 연결, 매니페스트 서버를 만들면 https 프로토콜이 있는 매니페스트 URL 및 감사 추적 URL이 반환됩니다.

   >[!NOTE]
   >
   >매니페스트 서버는 콘텐츠 세그먼트(.ts) 및 타사 추적 비콘의 프로토콜(HTTP 또는 HTTPS)을 변경할 수 없습니다. 원하는 프로토콜을 구성하려면 콘텐츠 및 서드파티 광고 공급자에게 문의해야 합니다.