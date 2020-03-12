---
title: 매니페스트 서버 디버깅 도구
seo-title: 매니페스트 서버 디버깅 도구
description: 매니페스트 서버 디버깅 도구
seo-description: 매니페스트 서버 디버깅 도구
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: b77f4988103b68d0ce8926407d2ccb2e0c68e322

---


# 매니페스트 서버 디버깅 도구 {#manifest-server-debugging-tool}

## 디버깅 도구 개요 {#overview-of-debugging-tool}

디버깅 도구를 사용하면 발행자는 HTTP 헤더에서 매니페스트 서버에서 실시간으로 반환되는 디버깅 정보를 검사하거나, 더 자세한 정보가 필요할 때 팩트 후에 세션 로그를 검사하여 비용이 많이 드는 광고 삽입 문제를 조사할 수 있습니다. Akamai와 같은 Adobe 파트너는 이 툴을 사용하여 Primetime 광고 결정과의 통합을 디버깅할 수 있습니다.

이 도구는 기본 매니페스트 서버 및 추적 구성에서 디버깅 및 삽입 문제를 지원합니다.

* TVSDK 기반의 플레이어를 사용한 클라이언트측 추적
* TVSDK를 기반으로 하지 않는 플레이어가 포함된 클라이언트측 추적
* 서버측 추적

이러한 모든 경우를 지원하기 위해 도구는 플레이어 게시자 코드를 요구하거나 사용하지 않습니다.

매니페스트 서버 세션을 시작할 때 요청 URL에 매개 변수를 설정하여 디버깅 정보를 기록하도록 요청할 수 있습니다. 이 매개 변수의 다른 값을 사용하면 매니페스트 서버에 지정된 디버깅 정보를 HTTP 헤더에 반환하도록 요청할 수 있지만 헤더에는 제한된 양의 정보만 포함할 수 있습니다. Adobe에서 자격 증명을 얻어 전체 로그 파일에 액세스할 수 있습니다. 이 자격 증명 서버는 아카이브 서버에 주기적으로(예: 시간별) 저장됩니다. 해당 서버에 대한 자격 증명이 있으면 언제든지 직접 액세스할 수 있습니다.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 디버깅 도구 옵션 {#debugging-tool-options}

디버깅 도구를 호출할 때 매니페스트 서버가 HTTP 헤더에서 반환하는 정보에 대한 여러 옵션이 있습니다. 이 옵션은 매니페스트 서버가 로그 파일에 가져오는 내용에는 영향을 주지 않습니다.

### ptdebug 지정 {#specifying-ptdebug}

매니페스트 서버 세션에 대한 디버그 로깅을 시작할 때 요청 URL에 ptdebug 매개 변수를 추가하여 매니페스트 서버가 HTTP 헤더에서 반환하는 정보에 대해 다음 옵션을 지정할 수 있습니다.

* ptdebug=true 레코드를 제외한 `TRACE_HTTP_HEADER` 대부분의 `call/response data` 레코드를 `TRACE_AD_CALL` 제외한 모든 레코드
* ptdebug=AdCall 전용 TRACE_AD_*type* (예: TRACE_AD_CALL) 레코드
* ptdebug=Header만 TRACE_HTTP_HEADER 레코드

이 옵션은 매니페스트 서버가 로그 파일에 저장하는 내용에는 영향을 주지 않습니다. 사용자는 이를 제어할 수 없지만 로그 파일은 텍스트 파일이므로 다양한 툴을 적용하여 원하는 정보를 추출하고 서식을 다시 지정할 수 있습니다.

다음은 반환된 HTTP 헤더의 예입니다 `ptdebug=Header`. 일부 16진수 문자열이 명확성을 `. . .` 위해 대체됩니다.

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

각 로그 레코드에는 유형 및 필드 세트가 있으며 이러한 필드 중 일부는 선택 사항일 수 있습니다. 레코드 유형까지 모든 레코드의 필드는 동일합니다. 이러한 타임스탬프는 세션에 대한 정보를 제공합니다. 레코드 유형은 로깅되는 이벤트의 종류를 식별하며, 그 다음 필드는 기록된 이벤트에 대한 정보를 제공합니다.

로그 레코드의 구조는 다음과 같습니다.

`datetime request_id session_id zone_id record_type` *기타 필드.*

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| datetime | 문자열 | 타임스탬프 |
| request_id | 문자열 | 매니페스트 서버에서 사용하는 요청 ID(unix 타임스탬프) |
| session_id | 문자열 | 매니페스트 서버에서 사용하는 세션 ID |
| zone_id | 정수 | 영역 ID |
| record_type | 문자열 | 로깅되는 이벤트 유형 |
| 기타 필드 | *** | 이벤트 유형에 따라 다름 |

### TRACE_REQUEST_INFO 레코드 {#trace-request-info-records}

이 유형의 레코드는 HTTP 요청의 결과를 기록합니다. TRACE_REQUEST_INFO 이외의 필드는 표에 표시된 순서대로 탭으로 구분되어 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| request_method | 문자열 | HTTP 메서드(GET 또는 POST) |
| request_uri | 문자열 | HTTP 요청 URI(호스트 없음) |
| request_length | 정수 | 요청 길이(바이트) |
| response_length | 정수 | 응답 길이(바이트) |
| 델타 | 정수 | 요청을 처리하는 시간(밀리초) |
| module_type | 문자열 | 변형, 스트림 또는 VOD |
| remote_address_aud_client_ip | 문자열 | (참고 참조) |
| remote_address_x_fwd_for_hdr_key | 문자열 | (참고 참조) |
| remote_host_port | 문자열 | (참고 참조) |

>[!NOTE]
>
>마지막 세 필드는 선택 사항입니다.

예:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER 레코드 {#trace-http-header-records}

매니페스트 서버와 클라이언트, 광고 서버 또는 컨텐츠 서버 간의 HTTP 호출 중에 교환된 이 유형의 로그 HTTP 헤더의 레코드입니다. TRACE_HTTP_HEADER를 벗어나는 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

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

### TRACE_AD_CALL 레코드 {#trace-ad-call-records}

이 유형의 레코드는 매니페스트 서버 광고 요청의 결과를 기록합니다. TRACE_AD_CALL 이외의 필드는 표에 표시된 순서대로 탭으로 구분되어 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| request_duration | 정수 | 요청에서 응답에 이르는 시간(밀리초) |
| ad_server_query_url | 문자열 | 쿼리 매개 변수를 포함한 광고 호출에 대한 URL |
| ad_system_id | 문자열 | 광고 시스템, 광고 서버 응답에서(지정되지 않은 경우 Auditude) |
| available_id | 문자열 | 콘텐츠 매니페스트 파일의 광고 큐에서 사용 가능한 ID(VOD의 경우 N/A) |
| available_duration | number | 컨텐츠 매니페스트 파일의 광고 큐에서 사용 가능한 기간(초)(VOD의 경우 N/A) |
| ad_server_response | 문자열 | 광고 서버로부터의 Base64 인코딩 응답 |

예:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE 및 TRACE_AD_REDIRECT 레코드 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

이 유형의 레코드는 레코드 유형으로 표시된 광고 요청의 결과를 기록합니다. 레코드 유형을 벗어나는 필드는 표에 표시된 순서대로 탭으로 구분되어 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| available_id | 문자열 | 콘텐츠 매니페스트 파일(라이브) 또는 매니페스트 서버(VOD)의 광고 큐에서 사용 가능한 ID |
| ad_type | 문자열 | 광고 유형(DIRECT 또는 REDIRECT) |
| ad_duration | 정수 | 광고 서버 응답에서 광고 지속 시간(초) |
| ad_content_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL |
| ad_content_url_actual | 문자열 | 삽입된 광고의 매니페스트 파일의 URL입니다. TRACE_AD_REDIRECT에 대해 비어 있습니다. |
| ad_system_id | 문자열 | 광고 시스템, 광고 서버 응답에서(지정되지 않은 경우 Auditude) |
| ad_id | 문자열 | 광고 서버 응답에서 광고 ID |
| creative_id | 문자열 | 광고 서버 응답에서 광고 노드에서 크리에이티브의 ID |
| ad_call_id | 문자열 | 사용되지 않습니다. 나중에 사용할 수 있도록 예약되었습니다. |
| 델타 | 정수 | 이 이벤트에 걸린 시간(밀리초) |
| misc | 문자열 | 이유 광고를 건너뛰었습니다. |

>[!NOTE]
>
>ad_content_url_actual, ad_call_id 및 misc 필드는 선택 사항입니다.

TRACE_AD_RESOLVE 및 TRACE_AD_INSERT의 경우, ad_content_url_actual 필드의 URL은 트랜스코딩된 광고에 대한 URL입니다(있는 경우). 그렇지 않으면 TRACE_AD_RESOLVE에 대해 필드가 비어 있거나 TRACE_AD_INSERT에 대해 ad_content_url과 같습니다.

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

### TRACE_TRACKING_URL 레코드 {#trace-tracking-url-records}

이 유형의 레코드는 매니페스트 서버 광고 요청의 결과를 기록합니다. TRACE_TRACKING_URL을 벗어나는 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| pts | number | 프로그램 타임스탬프. 비디오 내에서 URL을 호출하는 시간. |
| ad_system | 문자열 | 광고 시스템(Auditude 또는 Freewheel) |
| url | 문자열 | URL 핑됨 |
| status | 문자열 | Ping에서 반환된 HTTP 상태 |

예:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE 레코드 {#trace-transcoding-no-media-to-transcode-records}

이 유형의 레코드는 누락된 광고 크리에이티브를 기록합니다. TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE 이외의 유일한 필드가 표에 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| ad_id | 문자열 | 정규화된 광고 ID `(FQ_AD_ID: Q_AD_ID[;Q_AD_ID[;Q_AD_ID...]`] Q_AD_ID:[ `PROTOCOL:AD_SYSTEM:AD_ID[:CREATIVE_ID[:MEDIA_ID]`프로토콜:AUDITUDE, VAST) |

### TRACE_TRANSCODING_REQUESTED 레코드 {#trace-transcoding-requested-records}

이 유형의 레코드는 매니페스트 서버가 CRS에 전송하는 트랜스코딩 요청 결과를 기록합니다. TRACE_TRANSCODING_REQUESTED 이외의 필드는 표에 표시된 순서대로 탭으로 구분되어 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| ad_id | 문자열 | 정규화된 광고 ID |
| ad_manifest_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL |
| creative_type | 문자열 | 미디어 유형 |
| 플래그 | 문자열 | ID3는 코드 변환 요청에 ID3 태그 추가 요청이 포함되어 있는지 여부를 나타냅니다. |
| target_duration | 문자열 | 트랜스코딩된 크리에이티브의 대상 기간(초) |

### TRACE_TRACKING_REQUEST 레코드 {#trace-tracking-request-records}

이 유형의 레코드는 서버 측 추적을 수행하는 요청을 나타냅니다. TRACE_TRACKING_REQUEST 이외의 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| tracking_url_count | 정수 | 추적 URL 수 |
| start | float | PTS 조각 시작 시간(밀리초 정밀도의 초) |
| end | float | PTS 조각 종료 시간(밀리초 정밀도의 초) |

### TRACE_TRACKING_REQUEST_URL 레코드 {#trace-tracking-request-url-records}

이 유형의 레코드는 서버 측 추적을 위한 추적 URL을 제공합니다. TRACE_TRACKING_REQUEST_URL 이외의 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| timestamp | float | 추적 URL에 ping할 재생 세션 내의 시간(초, 정밀도 .001) |
| ad_system | 문자열 | 광고 시스템(예: Auditude) |
| url | 문자열 | ping에 대한 URL |

### TRACE_WEBVTT_REQUEST 레코드 {#trace-webvtt-request-records}

이 유형의 로그 레코드는 매니페스트 서버가 WEBVTT 캡션에 대해 수행하는 요청을 기록합니다. TRACE_WEBVTT_REQUEST 이외의 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| vtt_uri | 문자열 | 요청 URL |
| start | float | 시작 시간 분할(밀리초 단위의 정확성을 통해 초) |
| end | float | 종료 시간 분할(밀리초 단위의 정확성을 통해 초) |

### TRACE_WEBVTT_RESPONSE 레코드 {#trace-webvtt-response-records}

이 ``of ``로그 ``type ````responses ``서버 ``manifest ``서버 ``sends ``캡션을 SequenceCaptions ``clients ``에 `` `answer` ``기록합니다 ``requests `` `for` ``WEBVTT ``. TRACE_WEBVTT_RESPONSE를 벗어나는 필드는 분리된 `by`탭에 표에 표시된 순서대로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| 응답 | 문자열 | Base64 인코딩 응답이 클라이언트에 전송됨 |

### TRACE_WEBVTT_SOURCE 레코드 {#trace-webvtt-source-records}

매니페스트 서버가 WEBVTT 캡션에 대해 수행하는 요청에 대한 이 유형의 로그 응답 기록 TRACE_WEBVTT_SOURCE를 벗어나는 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | 반환된 HTTP 상태 코드 |
| 소스 | 문자열 | Base64 인코딩 원본 VTT 파섹 |


### TRACE_MISC 레코드 {#trace-misc-records}

이 유형의 레코드를 사용하면 매니페스트 서버가 광고를 가져올 때 별도로 계획되지 않은 이벤트와 정보를 기록할 수 있습니다. TRACE_MISC를 벗어나는 필드는 메시지 문자열로 구성됩니다. 표시되는 메시지는 다음과 같습니다.

* 무시된 광고:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdManifestURL=*adManifestURL*, duration *=*&#x200B;초&#x200B;*, ignore=* ignore *, redirectAd=redirect* AdRedirectAdPriority,*priority=seconds*
* 광고 배치가 null을 반환했습니다.
* 성공적으로 스티칭되었습니다.
* 광고 호출 실패: *오류 메시지*.
* 원시 매니페스트를 가져오기 위해 사용자-에이전트 추가: *사용자 에이전트*.
* 원시 매니페스트를 가져오기 위해 쿠키 추가: [쿠키]
* 잘못된 URL *요청 URL 오류 메시지*. (변형 URL을 구문 분석하지 못했습니다.)
* 호출된 url:URL *반환:응답*&#x200B;코드를 참조하십시오. (라이브 URL)
* 호출된 url:URL *반환 코드:응답*&#x200B;코드를 참조하십시오. (VOD URL)
* 광고를 해결하는 동안 충돌이 발견되었습니다.mid-roll 시작 또는 mid-roll 끝 중 하나가 VOD(Mid-Roll)에 포함된 프리롤 또는 프리롤 내에 해당합니다.
* URI에 대한 처리기가 throw한 처리되지 않은 예외가 검색되었습니다.URL *요청*.
* 변형 매니페스트를 생성했습니다. (변형)
* 변형 매니페스트를 생성했습니다.
* VAST 리디렉션 *리디렉션 URL *오류 처리 예외: *오류 메시지*.
* 광고 *매니페스트 URL에 대한 광고의 재생 목록을 가져오지 못했습니다*.
* 타깃팅된 매니페스트를 생성하지 못했습니다. (HLSManifestResolver)
* 첫 번째 광고 호출 응답을 구문 분석하지 못했습니다. *오류 메시지*.
* 경로에 대한 *GET|POST *요청을 처리하지 못했습니다.URL *요청*. (실시간/VOD)
* 라이브 매니페스트 요청을 처리하지 못했습니다.URL *요청*. (라이브)
* 변형 매니페스트를 반환하지 못했습니다. *오류 메시지*.
* 그룹 ID의 유효성을 확인하지 못했습니다. *그룹 ID*.
* 원시 매니페스트 가져오기: *컨텐츠 URL*. (라이브)
* 다음 VAST 리디렉션: *리디렉션 URL*.
* 빈 사용 가능 항목을 찾았습니다. (VOD)
* *숫자 *광고를 찾았습니다. (VOD)
* HTTP 요청을 받았습니다. (첫 번째 메시지)
* 광고 응답 기간(*ad 응답 기간 *초)과 실제 광고 지속 시간(*실제 지속 시간 *초)의 차이가 제한보다 커서 광고를 무시합니다. (HLSManifestResolver)
* ID 값을 제공하지 않은 사용 가능한 값을 무시합니다. (GroupAdResolver.java)
* 잘못된 시간 값을 제공한 사용 가능을 무시합니다.*time *for availableId = *사용 가능한 ID*.
* 잘못된 기간 값을 제공한 사용 가능이 무시됩니다.*duration *for availableId = *사용 가능한 ID*.
* 새 세션을 초기화합니다. (변형)
* HTTP 메서드가 잘못되었습니다. GET이어야 합니다. (VOD)
* HTTP 메서드가 잘못되었습니다. 추적 요청은 GET이어야 합니다. (라이브)
* URL *요청 URL 오류 메시지가*&#x200B;잘못되었습니다. (변형)
* 그룹이 잘못되었습니다. (HLSManifestResolver)
* 잘못된 요청입니다. 캡션은 올바른 추적 요청이 아닙니다. (VOD)
* 잘못된 요청입니다. 캡션 요청은 세션이 설정된 후에 해야 합니다. (VOD)
* 잘못된 요청입니다. 추적 요청은 세션이 설정된 후에 수행해야 합니다. (VOD)
* 오버로드 그룹 ID에 대한 서버 인스턴스가 잘못되었습니다. *그룹 ID*. (라이브)
* VAST 리디렉션 제한 - *숫자*.
* 광고 통화:URL *광고 호출*.
* 다음에 대한 매니페스트를 찾을 수 없습니다. *컨텐츠 URL*. (라이브)
* 사용 가능한 ID에 대해 일치하는 사용 가능한 방법이 없습니다.사용 *가능한 ID*. (HLSManifestResolver)
* 재생 세션을 찾을 수 없습니다. (HLSManifestResolver)
* 매니페스트 *콘텐츠 URL에 대한 VOD 요청을 처리합니다*.
* 변형 처리 중.
* 매니페스트 *콘텐츠 URL에 대한 캡션 요청을 처리합니다*.
* 추적 요청을 처리하는 중입니다. (VOD)
* 리디렉션 광고 응답이 비어 있습니다. (VASTStAX)
* 요청:URL **.
* 재생 세션을 찾을 수 없으므로 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 내부 서버 오류로 인해 GET 요청에 대한 오류 응답을 반환합니다.
* 잘못된 자산을 지정하는 GET 요청에 대한 오류 응답 반환: *광고 요청 ID*. (VOD)
* 잘못된 그룹 ID나 빈 그룹 ID를 지정하는 GET 요청에 대한 오류 응답 반환: *그룹 ID*. (VOD)
* 잘못된 추적 위치 값을 지정하는 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 잘못된 구문으로 GET 요청에 대한 오류 응답 반환 - *요청 URL*. (실시간/VOD)
* 지원되지 않는 HTTP 메서드가 있는 요청에 대한 오류 응답 반환:GET *|POST*. (실시간/VOD)
* 캐시에서 매니페스트를 반환합니다. (VOD)
* 서버가 오버로드되었습니다. 광고 스티치 요청 없이 계속 진행합니다. (변형)
* 타깃팅된 매니페스트 생성을 시작합니다. (HLSManifestResolver)
* 다음 위치에서 변형 매니페스트 생성을 시작합니다. *컨텐츠 URL*. (변형)
* 광고를 매니페스트로 결합합니다. (VODHLSResolver)
* HH:MM: *SS에서 광고를 스티칭하는 중*:AdManifestURL=*광고 매니페스트 URL*, durationSeconds *,* seconds *,* ignore *, 리디렉션*&#x200B;광고 리디렉션=**&#x200B;리디렉션 및 무시, 우선 순위=우선 순위입니다. (HLSManifestResolver)
* 잘못된 타임라인으로 인해 광고를 가져올 수 없습니다. 광고 없이 콘텐츠를 반환했습니다. (VOD)
* 광고를 가져올 수 없습니다. 광고 없이 콘텐츠를 반환했습니다. (VOD)
* 광고 쿼리를 가져올 수 없고 콘텐츠 URL이 지정되지 않았습니다. (VOD)
* 유효한 URL을 받았습니다. (VOD/변형)
* 변형 M3U8을 찾을 수 없습니다. (변형)

### TRACE_TRACKING_URL 레코드 {#trace-tracking-url-records-1}

매니페스트 서버는 서버측 추적 작업 과정 동안 추적 URL을 호출한 후 이러한 종류의 레코드를 생성합니다. TRACE_TRACKING_URL을 벗어나는 필드는 표에 표시된 순서대로 탭으로 표시됩니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| pts | number | 스트림 내 PTS 시간 |
| ad_system | 문자열 | 광고 시스템(Auditude 또는 Freewheel) |
| url | 문자열 | URL 핑됨 |
| state | 문자열 | HTTP 상태 코드 |

### TRACE_PLAYBACK_PROGRESS 레코드 {#trace-playback-progress-records}

매니페스트 서버는 서버측 추적 작업 과정 동안 재생 진행에 대한 신호를 받으면 이러한 종류의 레코드를 생성합니다. TRACE_PLAYBACK_PROGRESS 이외의 필드는 표에 표시된 순서대로 탭으로 구분되어 나타납니다.

| 필드 | 유형 | 설명 |
|--- |--- |--- |
| status | 문자열 | HTTP 상태 코드 |
| 대역폭 | 정수 | 스트림의 대역폭 |
| pts | 정수 | 스트림 내 PTS 시간 |
| ms_time | 정수 | 매니페스트 서버가 추적 URL을 생성한 시간 |
| url | 문자열 | 리디렉션 URL |
| header_user_agent | 문자열 | HTTP User-Agent 헤더 |
| header_dnt | 정수 | HTTP do-not-track 헤더 |
| effective_remote_address | 문자열 | IPv4 유효 원격 주소 |
| remote_address | 문자열 | IPv4 원격 주소 |

>[!NOTE]
>
>마지막 네 필드는 선택 사항입니다.

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.
