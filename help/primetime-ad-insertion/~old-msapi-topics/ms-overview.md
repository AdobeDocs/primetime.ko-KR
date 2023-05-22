---
description: 매니페스트 서버는 콘텐츠를 제공하고, 광고를 제공하고, 비디오를 재생하고, 광고를 추적하는 시스템을 조정합니다. 클라이언트 비디오 플레이어가 콘텐츠 공급자로부터 받는 M3U8 인코딩 플레이리스트(매니페스트)를 받고, 광고 공급자의 광고를 매니페스트에 결합하고, 결합된 매니페스트를 비디오 플레이어에 전달합니다. 클라이언트측과 서버측 광고 추적을 모두 지원합니다. HTTP 기반 웹 서비스 인터페이스를 사용하여 상호 작용을 수행합니다.
title: 매니페스트 서버 상호 작용 개요
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# 매니페스트 서버 상호 작용 개요 {#overview-of-manifest-server-interactions}

매니페스트 서버는 콘텐츠를 제공하고, 광고를 제공하고, 비디오를 재생하고, 광고를 추적하는 시스템을 조정합니다. 클라이언트 비디오 플레이어가 콘텐츠 공급자로부터 받는 M3U8 인코딩 플레이리스트(매니페스트)를 받고, 광고 공급자의 광고를 매니페스트에 결합하고, 결합된 매니페스트를 비디오 플레이어에 전달합니다. 클라이언트측과 서버측 광고 추적을 모두 지원합니다. HTTP 기반 웹 서비스 인터페이스를 사용하여 상호 작용을 수행합니다.

일반적인 구성은 다음과 같습니다.

* Primetime 매니페스트 서버
* Primetime CRS(Creative Repackaging Service)
* 클라이언트, 비디오 플레이어 제어
* 일반적으로 콘텐츠 관리 시스템(CMS)을 사용하는 게시자입니다
* CDN(Content Delivery Network)
* 광고 서버
* 광고 추적 보고서 수신자

워크플로우는 CDN이 Akamai인지 또는 클라이언트가 광고 추적을 수행하는 지와 같은 여러 요인에 따라 달라집니다. 클라이언트측 광고 추적을 위한 워크플로에 대한 다이어그램은 을 참조하십시오. [클라이언트측 추적 워크플로](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

매니페스트 서버는 HTTP GET 요청을 수신하고 이에 응답하여 비디오 게재 클라이언트와 상호 작용합니다. 응답은 자세한 광고 추적 지침을 포함하는 JSON 또는 VMAP 구조(사이드카)를 선택적으로 포함하여 광고 결합 콘텐츠를 설명하는 M3U8 인코딩 매니페스트입니다(참조) [파일 형식](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

일반적인 워크플로우는 다음과 같습니다.

1. 게시자는 광고 서버에 대한 콘텐츠 URL 및 정보를 클라이언트에 보냅니다.
1. 클라이언트는 게시자의 정보를 사용하여 매니페스트 서버 URL을 생성하고 해당 URL에 GET 요청을 보냅니다. 이를 Bootstrap URL이라고 합니다.
1. 매니페스트 서버는 클라이언트와 세션을 설정합니다.
1. 매니페스트 서버는 CDN에서 콘텐츠 매니페스트를 가져오며, 여기에는 광고 브레이크 정보가 포함될 수 있습니다.
1. 매니페스트 서버는 클라이언트에 대해 생성한 마스터/변형 매니페스트로 클라이언트를 리디렉션합니다.

   >[!NOTE]
   >
   >Bootstrap URL 쿼리 매개 변수에 `pttrackingmode=simple` 또는 `ptplayer=ios-mobileweb` 을 설정하면 매니페스트 서버가 JSON 개체의 마스터/변형 매니페스트 URL을 반환하고 클라이언트가 해당 변형 매니페스트 URL에 GET 요청을 보냅니다.

1. 클라이언트가 생성된 변형 매니페스트에서 재생할 스트림을 선택하여 매니페스트 서버에 광고 정보를 보냅니다.
1. 매니페스트 서버는 클라이언트가 제공한 정보를 광고 서버에 전달하고 광고 서버로부터 광고 및 광고 추적 URL을 수신합니다. 제공된 광고가 HLS 포맷이 아닌 경우 매니페스트 서버는 HLS로의 전환을 위해 CRS로 광고를 전송합니다.
1. 매니페스트 서버는 광고를 콘텐츠 매니페스트에 결합하고 결합된 새 매니페스트를 클라이언트에 보냅니다.
1. 클라이언트는 결합된 광고와 함께 콘텐츠를 재생하고 지정된 시간에 지정된 추적 URL에 대한 요청을 수행합니다.

Primetime ad insertion은 많은 비디오 게재 플랫폼에서 클라이언트를 지원합니다. 모든 클라이언트가 Primetime TVSDK 패키지에 빌드된 것은 아니지만, 모든 클라이언트가 동일한 기본 URL에 GET 요청을 보냅니다. 쿼리 매개 변수는 매니페스트 서버에 다음과 같이 알려 하나의 클라이언트 요청을 구별합니다.

* 어떤 클라이언트가 요청을 하고 있는지,
* 고객이 원하는 건
* 및 제공할 광고 추적 정보입니다.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

매니페스트 서버는 CORS(원본 간 리소스 공유 표준)를 사용합니다. 다음을 찾습니다. `Origin` 받은 요청의 헤더입니다. 헤더가 있으면 다음으로 응답합니다.

* `Access-Control-Allow-Origin: *`Origin 헤더의 문자열`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

그렇지 않으면 답글 작성:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`