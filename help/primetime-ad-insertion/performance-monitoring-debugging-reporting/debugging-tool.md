---
title: 매니페스트 서버 디버깅 도구
description: 매니페스트 서버 디버깅 도구
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# 매니페스트 서버 디버깅 도구 {#manifest-server-debugging-tool}

디버깅 도구를 사용하면 게시자가 HTTP 헤더에서 매니페스트 서버에 의해 실시간으로 반환되는 디버깅 정보를 검사하거나, 더 자세한 정보가 필요한 경우 사후 세션 로그를 검사하여 비용이 많이 들 수 있는 광고 삽입 문제를 조사할 수 있습니다. Akamai와 같은 Adobe 파트너는 이 도구를 사용하여 Primetime ad decisioning과의 통합을 디버그할 수 있습니다.

이 도구는 기본 매니페스트 서버 광고 추적 구성에서 디버깅 광고 삽입 문제를 지원합니다.

* TVSDK 기반의 플레이어로 클라이언트측 추적.
* TVSDK를 기반으로 하지 않는 플레이어로 클라이언트측 추적.
* 서버측 추적.

이러한 모든 경우를 지원하기 위해 도구에는 플레이어 게시자 코드가 필요하거나 사용되지 않습니다.

매니페스트 서버 세션을 시작할 때 요청 URL에 매개 변수를 설정하여 디버깅 정보를 기록하도록 요청할 수 있습니다. 해당 매개 변수의 다른 값을 사용하여 매니페스트 서버에 HTTP 헤더에서 지정된 디버깅 정보를 반환하도록 요청할 수도 있지만 헤더에는 제한된 양의 정보만 포함될 수 있습니다. 매니페스트 서버가 보관 서버에 주기적으로(예: 시간별) 저장하는 전체 로그 파일에 액세스하기 위해 Adobe에서 자격 증명을 가져올 수 있습니다. 해당 서버에 대한 자격 증명이 있으면 언제든지 직접 액세스할 수 있습니다.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 디버깅 도구 옵션 {#debugging-tool-options}

디버깅 도구를 호출할 때 매니페스트 서버가 HTTP 헤더에서 반환하는 정보에 대한 몇 가지 옵션이 있습니다. 옵션은 매니페스트 서버가 로그 파일에 배치하는 내용에 영향을 주지 않습니다.

### ptdebug 지정 {#specifying-ptdebug}

매니페스트 서버 세션에 대한 디버그 로깅을 시작할 때 요청 URL에 ptdebug 매개 변수를 추가하여 매니페스트 서버가 HTTP 헤더에서 반환하는 정보에 대해 다음 옵션을 지정할 수 있습니다.

* ptdebug=true 다음을 제외한 모든 레코드 `TRACE_HTTP_HEADER` 및 가장 `call/response data` 출처: `TRACE_AD_CALL` 레코드.
* ptdebug=AdCall 전용 TRACE_AD_*유형* (예: TRACE_AD_CALL) 레코드.
* ptdebug=Header Only TRACE_HTTP_HEADER 레코드

옵션은 매니페스트 서버가 로그 파일에 배치하는 내용에 영향을 주지 않습니다. 이를 제어할 수는 없지만 로그 파일은 텍스트 파일이므로 다양한 도구를 적용하여 원하는 정보를 추출하고 형식을 다시 지정할 수 있습니다.

다음은 다음과 같은 경우에 반환되는 HTTP 헤더의 예입니다 `ptdebug=Header`. 일부 16진수 긴 문자열은 로 대체됩니다. `. . .` 명확성을 위해

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## 로그 레코드 형식 {#formats-of-log-records}

각 로그 레코드에는 유형 및 필드 세트가 있으며 그 중 일부는 선택 사항일 수 있습니다. 레코드 유형까지 모든 레코드의 필드는 동일합니다. 타임스탬프와 세션에 대한 정보를 제공합니다. 기록 유형은 기록되는 이벤트의 종류를 식별하며, 후속 필드에는 기록된 이벤트에 대한 정보가 제공됩니다.

로그 레코드의 구조는 다음과 같습니다.

`datetime request_id session_id zone_id record_type` *기타 필드.*

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| datetime | 문자열 | 타임스탬프 |
| request_id | 문자열 | 매니페스트 서버에서 사용하는 요청 ID(unix 타임스탬프) |
| session_id | 문자열 | 매니페스트 서버에서 사용하는 세션 ID |
| zone_id | 정수 | 영역 ID |
| record_type | 문자열 | 기록되는 이벤트 유형 |
| 기타 필드 | *** | 이벤트 유형에 따라 다름 |

### TRACE 요청 정보 레코드 {#trace-request-info-records}

이 유형의 레코드는 HTTP 요청의 결과를 기록합니다. TRACE_REQUEST_INFO 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| request_method | 문자열 | HTTP 메서드(GET 또는 POST) |
| request_uri | 문자열 | HTTP 요청 URI(호스트 없음) |
| request_length | 정수 | 요청 길이(바이트) |
| response_length | 정수 | 응답 길이(바이트) |
| 델타 | 정수 | 요청을 처리하는 시간(밀리초) |
| module_type | 문자열 | 변형, 스트림 또는 VOD |
| remote_address_aud_client_ip | 문자열 | (메모 참조) |
| remote_address_x_fwd_for_hdr_key | 문자열 | (메모 참조) |
| remote_host_port | 문자열 | (메모 참조) |

>[!NOTE]
>
>마지막 세 필드는 선택 사항입니다.

예:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE HTTP_HEADER 레코드 {#trace-http-header-records}

이 유형의 레코드는 매니페스트 서버와 클라이언트, 광고 서버 또는 콘텐츠 서버 간의 HTTP 호출 동안 교환된 로그 HTTP 헤더입니다. TRACE_HTTP_HEADER 이상의 필드는 탭에 의해 구분되어 테이블에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| request_type | 문자열 | 요청 유형(MAIN 또는 UNKNOWN) |
| request_response | 문자열 | 응답 헤더(요청 또는 응답) |
| header_name | 문자열 | HTTP 헤더 이름 |
| header_value | 문자열 | Base64 인코딩 HTTP 헤더 값 |

>[!NOTE]
>
>request_type 및 header_value 필드는 선택 사항입니다.

예:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACE 광고 호출 레코드 {#trace-ad-call-records}

이 유형의 레코드는 매니페스트 서버 광고 요청의 결과를 기록합니다. TRACE_AD_CALL 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| request_duration | 정수 | 요청에서 응답까지의 시간(밀리초) |
| ad_server_query_url | 문자열 | 쿼리 매개 변수를 포함한 광고 호출용 URL |
| ad_system_id | 문자열 | 광고 서버 응답의 광고 시스템(지정되지 않은 경우 감사) |
| availail_id | 문자열 | 콘텐츠 매니페스트 파일의 광고 큐에서 사용할 수 있는 ID(VOD의 경우 N/A) |
| availail_duration | 숫자 | 콘텐츠 매니페스트 파일의 광고 큐에서 사용 가능한 기간(초)(VOD의 경우 N/A) |
| ad_server_response | 문자열 | 광고 서버의 Base64 인코딩 응답 |

예:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE 및 TRACE_AD_REDIRECT 레코드 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

이 유형의 레코드는 레코드 유형으로 표시된 광고 요청의 결과를 기록합니다. 레코드 유형 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| availail_id | 문자열 | 콘텐츠 매니페스트 파일의 광고 큐(라이브) 또는 매니페스트 서버(VOD)에서 사용할 수 있는 ID입니다 |
| ad_type | 문자열 | 광고 유형(직접 또는 리디렉션) |
| ad_duration | 정수 | 광고 서버 응답에서 광고 기간(초) |
| ad_content_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL |
| ad_content_url_actual | 문자열 | 삽입된 광고의 매니페스트 파일 URL. TRACE_AD_REDIRECT에 대해 비어 있음. |
| ad_system_id | 문자열 | 광고 서버 응답의 광고 시스템(지정되지 않은 경우 감사) |
| ad_id | 문자열 | 광고 서버 응답의 광고 ID |
| creative_id | 문자열 | 광고 노드, 광고 서버 응답의 크리에이티브 ID |
| ad_call_id | 문자열 | 사용되지 않습니다. 향후 사용을 위해 예약되었습니다. |
| 델타 | 정수 | 이 이벤트에 걸린 시간(밀리초) |
| 기타 | 문자열 | 광고 건너뛰기 사유 |

>[!NOTE]
>
>ad_content_url_actual, ad_call_id 및 기타 필드는 선택 사항입니다.

TRACE_AD_RESOLVE 및 TRACE_AD_INSERT의 경우 ad_content_url_actual 필드의 URL은 트랜스코딩된 광고(사용 가능한 경우)에 대한 것입니다. 그렇지 않으면 필드가 비어 있거나 TRACE_AD_RESOLVE에 대한 TRACE_AD_INSERT에 대한 ad_content_url과 같습니다.

예:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### TRACE 추적 URL 레코드 {#trace-tracking-url-records}

이 유형의 레코드는 매니페스트 서버 광고 요청의 결과를 기록합니다. TRACE_TRACKING_URL 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| pts | 숫자 | 프로그램 타임스탬프. 비디오 내에서 URL을 호출하는 데 걸리는 시간입니다. |
| ad_system | 문자열 | 광고 시스템(감사 또는 프리휠) |
| url | 문자열 | URL 핑됨 |
| 상태 | 문자열 | ping에서 반환된 HTTP 상태 |

예:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE 레코드 {#trace-transcoding-no-media-to-transcode-records}

이 유형의 레코드는 누락된 광고 크리에이티브를 기록합니다. TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE 이외의 필드만 테이블에 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| ad_id | 문자열 | 정규화된 광고 ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` 프로토콜: AUDITUDE,VAST) |

### TRACE_TRANSCODING_REQUESTED 레코드 {#trace-transcoding-requested-records}

이 유형의 레코드는 매니페스트 서버가 CRS에 보내는 트랜스코딩 요청의 결과를 기록합니다. TRACE_TRANSCODING_REQUESTED 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| ad_id | 문자열 | 정규화된 광고 ID |
| ad_manifest_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL |
| creative_type | 문자열 | 미디어 유형 |
| 플래그 | 문자열 | ID3는 트랜스코딩 요청에 ID3 태그를 추가하라는 요청이 포함되어 있는지 여부를 나타낸다 |
| target_duration | 문자열 | 트랜스코딩된 크리에이티브의 Target 기간(초) |

### TRACE 추적 요청 레코드 {#trace-tracking-request-records}

이 유형의 레코드는 서버측 추적을 수행하기 위한 요청을 나타냅니다. TRACE_TRACKING_REQUEST 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| tracking_url_count | 정수 | 추적 URL 수 |
| 시작 | 부동 | PTS 조각 시작 시간(초, 밀리초 단위) |
| 종료 | 부동 | PTS 조각 종료 시간(초, 밀리초 단위) |

### TRACE_TRACKING_REQUEST_URL 레코드 {#trace-tracking-request-url-records}

이 유형의 레코드는 서버측 추적을 위한 추적 URL을 제공합니다. TRACE_TRACKING_REQUEST_URL 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| timestamp | 부동 | 재생 세션 내에서 추적 URL을 ping하는 시간(초, 전체 자릿수 .001) |
| ad_system | 문자열 | 광고 시스템(예: auditude) |
| url | 문자열 | ping할 URL |

### TRACE_WEBVTT_REQUEST 레코드 {#trace-webvtt-request-records}

이 유형의 로그 레코드는 매니페스트 서버가 WEBVTT 캡션에 대해 수행하는 요청을 요청합니다. TRACE_WEBVTT_REQUEST 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| vtt_uri | 문자열 | 요청용 URL |
| 시작 | 부동 | 분할 시작 시간(초, 밀리초 단위 정밀도) |
| 종료 | 부동 | 분할 종료 시간(초, 밀리초 단위 정밀도) |

### TRACE_WEBVTT_RESPONSE 레코드 {#trace-webvtt-response-records}

레코드 ``of ``이 ``type ``log ``responses ``다음 ``manifest ``server ``sends ``끝 ``clients ``위치: `` `answer` ``끝 ``requests `` `for` ``WEBVTT ``캡션 TRACE_WEBVTT_RESPONSE 이상의 필드는 표에 표시된 순서대로 구분되어 나타납니다 `by`탭.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| 응답 | 문자열 | 클라이언트로 보낸 Base64 인코딩 응답 |

### TRACE_WEBVTT_SOURCE 레코드 {#trace-webvtt-source-records}

매니페스트 서버에서 WEBVTT 캡션에 대해 수행하는 요청에 대한 이 유형의 로그 응답 레코드입니다. TRACE_WEBVTT_SOURCE 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| 소스 | 문자열 | Base64로 인코딩된 원본 VTT 콘텐츠 |


### TRACE 기타 레코드 {#trace-misc-records}

이 유형의 레코드를 사용하면 매니페스트 서버에서 이벤트를 기록하고 광고를 수집할 때 별도로 계획되지 않은 정보를 기록할 수 있습니다. TRACE_MISC 뒤에 있는 필드는 메시지 문자열로 구성됩니다. 다음과 같은 메시지가 표시될 수 있습니다.

* 무시된 광고:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*초*, 무시=*무시*, redirectAd=*redirectAd*, 우선 순위=*우선 순위*
* 광고 배치가 null을 반환했습니다.
* 광고가 성공적으로 결합되었습니다.
* 광고 호출 실패: *오류 메시지*.
* 원시 매니페스트를 가져오기 위해 사용자 에이전트를 추가하는 중: *사용자 에이전트*.
* 원시 매니페스트를 가져오기 위해 쿠키 추가: [쿠키]
* 잘못된 URL *요청한 URL 오류 메시지*. (변형 URL 구문 분석 실패)
* 호출된 url: URL *got return: 응답 코드*. ( 라이브 URL)
* 호출된 url: URL *반환 코드: 응답 코드*. ( VOD URL)
* 광고를 해결하는 도중 충돌 발견: 미드롤 시작 또는 미드롤 끝 중 하나가 미드롤(VOD)에 포함된 프리롤 또는 프리롤 내에 속합니다.
* URI에 대한 처리기에서 throw한 처리되지 않은 예외가 감지되었습니다. *요청 URL*.
* 변형 매니페스트 생성을 완료했습니다. (변형)
* 변형 매니페스트 생성을 완료했습니다.
* VAST 리디렉션 *리디렉션 URL *오류를 처리할 때 예외 발생: *오류 메시지*.
* 에 대한 광고 재생 목록을 가져오지 못했습니다. *광고 매니페스트 URL*.
* 타깃팅된 매니페스트를 생성하지 못했습니다. (HLSManifestResolver)
* 첫 번째 광고 호출 응답을 구문 분석하지 못했습니다. *오류 메시지*.
* 다음 경로에 대한 *GET|POST *요청을 처리하지 못했습니다. *요청 URL*. (라이브/VOD)
* 라이브 매니페스트 요청을 처리하지 못했습니다. *요청 URL*. (라이브)
* 변형 매니페스트를 반환하지 못했습니다. *오류 메시지*.
* 그룹 ID의 유효성을 검사하지 못했습니다. *그룹 ID*.
* 원시 매니페스트를 가져오는 중: *콘텐츠 URL*. (라이브)
* 다음 VAST 리디렉션: *리디렉션 URL*.
* 빈 공간을 찾았습니다. (VOD)
* *개 *광고를 찾았습니다. (VOD)
* HTTP 요청을 받았습니다. (첫 번째 메시지)
* 광고 응답 기간(*광고 응답 기간 *초)과 실제 광고 기간(*실제 기간 *초)의 차이가 제한보다 크므로 광고를 무시합니다. (HLSManifestResolver)
* ID 값을 제공하지 않은 가용성을 무시합니다. (GroupAdResolver.java)
* 잘못된 시간 값을 제공한 가용성을 무시합니다. *time *for availId = *사용 가능 ID*.
* 잘못된 기간 값을 제공한 가용성을 무시합니다. *duration *for availId = *사용 가능 ID*.
* 새 세션 초기화. (변형)
* 잘못된 HTTP 메서드. GET 모양이군요. (VOD)
* 잘못된 HTTP 메서드. 추적 요청은 GET여야 합니다. (라이브)
* 잘못된 URL *요청한 URL 오류 메시지*. (변형)
* 잘못된 그룹입니다. (HLSManifestResolver)
* 잘못된 요청입니다. 캡션은 유효한 추적 요청이 아닙니다. (VOD)
* 잘못된 요청입니다. 캡션 요청은 세션이 설정된 후에 수행해야 합니다. (VOD)
* 잘못된 요청입니다. 추적 요청은 세션이 설정된 후에 수행해야 합니다. (VOD)
* 오버로드 그룹 ID에 대한 잘못된 서버 인스턴스: *그룹 ID*. (라이브)
* VAST 리디렉션 제한에 도달했습니다. - *숫자*.
* 광고 호출 수행: *광고 호출 URL*.
* 다음에 대한 매니페스트를 찾을 수 없음: *콘텐츠 URL*. (라이브)
* 사용 가능한 ID에 대해 일치하는 사용 가능한 항목이 없습니다. *사용 가능 ID*. (HLSManifestResolver)
* 재생 세션을 찾을 수 없습니다. (HLSManifestResolver)
* 매니페스트에 대한 VOD 요청 처리 중 *콘텐츠 URL*.
* 변형 처리 중
* 매니페스트에 대한 캡션 요청을 처리하는 중 *콘텐츠 URL*.
* 추적 요청을 처리하는 중입니다. (VOD)
* 리디렉션 광고 응답이 비어 있습니다. ( VASTStAX)
* 요청 중: *URL*.
* 재생 세션을 찾을 수 없어 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 내부 서버 오류로 인해 GET 요청에 대한 오류 응답을 반환합니다.
* 잘못된 자산을 지정하는 GET 요청에 대한 오류 응답 반환: *광고 요청 ID*. (VOD)
* 잘못되거나 빈 그룹 ID를 지정하는 GET 요청에 대한 오류 응답 반환: *그룹 ID*. (VOD)
* 잘못된 추적 위치 값을 지정하는 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 구문이 잘못된 GET 요청에 대한 오류 응답 반환 - *요청 URL*. (라이브/VOD)
* 지원되지 않는 HTTP 메서드를 사용하는 요청에 대한 오류 응답을 반환합니다. *GET|POST*. (라이브/VOD)
* 캐시에서 매니페스트를 반환합니다. (VOD)
* 서버가 오버로드되었습니다. 광고 결합 요청 없이 진행합니다. (변형)
* 타깃팅된 매니페스트를 생성하기 시작합니다. (HLSManifestResolver)
* 변형 매니페스트 생성 시작 위치: *콘텐츠 URL*. (변형)
* 광고를 매니페스트로 결합합니다. (VODHLSResolver)
* 광고 결합 시도 중 `HH:MM:SS`: AdPlacement \[adManifestURL=*광고 매니페스트 URL*, durationSeconds=*초*, 무시=*무시*, redirectAd=*광고 리디렉션*, 우선 순위=*우선 순위*.\]
* 잘못된 pttimeline으로 인해 광고를 가져올 수 없습니다. - 광고가 없는 콘텐츠를 반환했습니다. (VOD)
* 광고를 가져올 수 없음 - 광고 없이 콘텐츠를 반환했습니다. (VOD)
* 광고 쿼리를 가져올 수 없으며 콘텐츠 URL이 제공되지 않았습니다. (VOD)
* 유효한 URL이 수신되었습니다. (VOD/Variant)
* 변형 M3U8을 찾을 수 없습니다. (변형)

### TRACE 추적 URL 레코드 {#trace-tracking-url-records-1}

매니페스트 서버는 서버측 추적 워크플로 중에 추적 URL을 호출한 후 이러한 종류의 레코드를 생성합니다. TRACE_TRACKING_URL 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| pts | 숫자 | 스트림 내 PTS 시간 |
| ad_system | 문자열 | 광고의 광고 시스템(감사 또는 프리휠) |
| url | 문자열 | URL 핑됨 |
| 상태 | 문자열 | HTTP 상태 코드 |

### TRACE_재생_진행 레코드 {#trace-playback-progress-records}

매니페스트 서버는 서버측 추적 워크플로 중에 재생 진행에 대한 신호를 수신하면 이러한 종류의 레코드를 생성합니다. TRACE_PLAYBACK_PROGRESS 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| 상태 | 문자열 | HTTP 상태 코드 |
| 대역폭 | 정수 | 스트림의 대역폭 |
| pts | 정수 | 스트림 내 PTS 시간 |
| ms_time | 정수 | 매니페스트 서버에서 추적 URL을 생성한 시간 |
| url | 문자열 | 리디렉션 URL |
| header_user_agent | 문자열 | HTTP 사용자 에이전트 헤더 |
| header_dnt | 정수 | HTTP do-not-track 헤더 |
| effective_remote_address | 문자열 | IPv4 유효 원격 주소 |
| remote_address | 문자열 | IPv4 원격 주소 |

>[!NOTE]
>
>마지막 네 필드는 선택 사항입니다.

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
