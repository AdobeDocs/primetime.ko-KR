---
description: HTTP GET 명령을 사용하여 매니페스트 서버와 상호 작용합니다.
seo-description: HTTP GET 명령을 사용하여 매니페스트 서버와 상호 작용합니다.
seo-title: 매니페스트 서버로 명령 보내기
title: 매니페스트 서버로 명령 보내기
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 매니페스트 서버 {#send-a-command-to-the-manifest-server}에 명령 보내기

HTTP GET 명령을 사용하여 매니페스트 서버와 상호 작용합니다.

1. 다음 패턴을 사용하여 생성된 부트스트랩 URL에 대한 `HTTP GET` 요청을 전송합니다.

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetIDR이** 필요합니다. 특정 컨텐츠에 대한 게시자의 고유 ID.

* **컨텐츠** URLRrequired. 매니페스트 서버 URL 내에서 안전하도록 인코딩된 M3U8 파일의 URL입니다. 콘텐츠 URL은 비트 전송률 스트림이 하나만 있는 경우에도 변형 M3U8 파일을 가리켜야 합니다.

* **쿼리** 매개 변수일부는 필수, 일부는 선택 사항입니다. 이것들은 그 요청에서 가장 다양한 부분이다. 매니페스트 서버에는 요청을 수행하는 클라이언트 정렬 및 매니페스트 서버가 수행할 작업을 알려 줍니다.

   예:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP와 HTTPS 요청 비교**

   매니페스트 서버는 클라이언트의 요청과 동일한 HTTP 프로토콜을 사용하여 URL을 만듭니다. 플레이어가 비보안 HTTP(http) 요청을 수행하는 경우 매니페스트 서버는 http 프로토콜을 사용하여 매니페스트 URL 및 Auditude 추적 URL을 반환합니다. 플레이어가 보안 HTTP(https) 연결 매니페스트 서버를 만들면 HTTPS 프로토콜을 사용하는 매니페스트 URL 및 Auditude 추적 URL을 반환합니다.

   >[!NOTE]
   >
   >매니페스트 서버는 컨텐츠 세그먼트(.ts) 및 타사 추적 비콘의 프로토콜(HTTP 또는 HTTPS)을 변경할 수 없습니다. 원하는 프로토콜을 구성하려면 컨텐츠 및 타사 광고 공급자에 문의해야 합니다.