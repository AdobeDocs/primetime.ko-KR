---
title: 자세한 정보 로깅
description: 자세한 정보 로깅
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# 자세한 정보 로깅 {#verbose-logging}

## ptdebug/logging 이벤트 설명 {#ptdebug-logging-events}

매니페스트 서버 세션에 대한 디버그 로깅을 시작할 때 `ptdebug` 매니페스트 서버가 HTTP 헤더에서 반환하는 정보에 대한 다음 옵션을 지정하기 위한 요청 URL의 매개 변수입니다.

* `ptdebug=true`
TRACE_HTTP_HEADER 및 TRACE_AD_CALL 레코드의 대부분의 호출/응답 데이터를 제외한 모든 레코드.

* `ptdebug=AdCall`
TRACE_AD_ 유형(예: TRACE_AD_CALL)만 레코드.

* `ptdebug=Header`
TRACE_HTTP_HEADER 레코드만

## 로그 레코드 형식 {#log-record-formats}

각 로그 레코드에는 유형 및 필드 세트가 있으며 그 중 일부는 선택 사항일 수 있습니다. 레코드 유형까지 모든 레코드의 필드는 동일합니다. 타임스탬프와 세션에 대한 정보를 제공합니다. 기록 유형은 기록되는 이벤트의 종류를 식별하며, 후속 필드에는 기록된 이벤트에 대한 정보가 제공됩니다.

로그 레코드의 구조는 다음과 같습니다.

`datetime request_id session_id zone_id record_type other fields`.

| 필드 | 유형 | 설명 |
|---|---|---|
| datetime | 문자열 | 타임스탬프 |
| request_id | 문자열 | 매니페스트 서버에서 사용하는 요청 ID(Unix 타임스탬프) |
| session_id | 문자열 | 매니페스트 서버에서 사용하는 세션 ID |
| zone_id | 정수 | 영역 |
| record_type | 문자열 | 기록되는 이벤트 유형 |
| 기타 필드 | 다양함 | 이벤트 유형에 따라 다름 |

이 유형의 레코드는 HTTP 요청의 결과를 기록합니다. 다음 범위 밖의 필드 `TRACE_REQUEST_INFO` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| request_method | 문자열 | HTTP 메서드(GET 또는 POST) |
| request_uri | 문자열 | HTTP 요청 URI(호스트 없음) |
| request_length | 정수 | 요청 길이(바이트) |
| response_length | 정수 | 응답 길이(바이트) |
| 델타 | 정수 | 요청을 처리하는 시간(밀리초) |
| module_type | 문자열 | 변형, 스트림 또는 VOD |
| remote_address_aud_client_ip | 문자열 | **‡** |
| remote_address_x_fwd_for_hdr_key | 문자열 | **‡** |
| remote_host_port | 문자열 | **‡** |

**‡** 마지막 세 필드는 선택 사항입니다.

**예**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE HTTP_HEADER 레코드 {#trace-http-header-records}

이 유형의 레코드는 매니페스트 서버와 클라이언트, 광고 서버 또는 콘텐츠 서버 간의 HTTP 호출 동안 교환된 로그 HTTP 헤더입니다. TRACE_HTTP_HEADER 이상의 필드는 탭에 의해 구분되어 테이블에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| request_type | 문자열 | 요청 유형(MAIN 또는 UNKNOWN) |
| request_response | 문자열 | 응답 헤더(요청 또는 응답) |
| header_name | 문자열 | HTTP 헤더 이름 |
| header_value | 문자열 | Base64 인코딩 HTTP 헤더 값 |

>[!NOTE]
>
>다음 `request_type` 및 `header_value` 필드는 선택 사항입니다.

**예**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE 광고 호출 레코드 {#tracing-ad-call-records}

이 유형의 레코드는 매니페스트 서버 광고 요청의 결과를 기록합니다. 다음 범위 밖의 필드 `TRACE_AD_CALL` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| request_duration | 정수 | 요청에서 응답까지의 시간(밀리초) |
| ad_server_query_url | 문자열 | 쿼리 매개 변수를 포함한 광고 호출용 URL |
| ad_system_id | 문자열 | 광고 서버 응답의 광고 시스템(지정되지 않은 경우 감사) |
| availail_id | 문자열 | 콘텐츠 매니페스트 파일의 광고 큐에서 사용할 수 있는 ID(VOD의 경우 N/A) |
| availail_duration | 숫자 | 콘텐츠 매니페스트 파일의 광고 큐에서 사용 가능한 기간(초)(VOD의 경우 N/A) |
| ad_server_response | 문자열 | 광고 서버의 Base64 인코딩 응답 |

예:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT, TRACE_AD_RESOLVE 및 TRACE_AD_REDIRECT 레코드 {#trace-ad-insert-resolve-redirect}

이 유형의 레코드는 레코드 유형으로 표시된 광고 요청의 결과를 기록합니다. 레코드 유형 이상의 필드는 탭에 의해 구분되어 표에 표시된 순서로 나타납니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | HTTP 상태 코드가 반환되었습니다. |
| availail_id | 문자열 | 콘텐츠 매니페스트 파일의 광고 큐(라이브) 또는 매니페스트 서버(VOD)에서 사용할 수 있는 ID입니다. |
| ad_type | 문자열 | 광고 유형(직접 또는 리디렉션). |
| ad_duration | 정수 | 광고 서버 응답에서 광고 기간(초)입니다. |
| ad_content_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL. |
| **†** ad_content_url_actual | 문자열 | 삽입된 광고의 매니페스트 파일 URL. TRACE_AD_REDIRECT에 대해 비어 있음. |
| ad_system_id | 문자열 | 광고 서버 응답의 광고 시스템(지정되지 않은 경우 감사). |
| ad_id | 문자열 | 광고 서버 응답의 광고 ID. |
| creative_id | 문자열 | 광고 노드, 광고 서버 응답의 크리에이티브 ID. |
| **†** ad_call_id | 문자열 | 사용되지 않습니다. 향후 사용을 위해 예약되었습니다. |
| 델타 | 정수 | 이 이벤트에 걸린 시간(밀리초)입니다. |
| **†** 기타 | 문자열 | 이유 광고를 건너뛰었습니다. |

**†** `ad_content_url_actual`, `ad_call_id`, 및 `misc` 필드는 선택 사항입니다.

>[!NOTE]
>
>대상 `TRACE_AD_RESOLVE` 및 `TRACE_AD_INSERT`, 의 URL `ad_content_url_actual` 필드는 트랜스코딩된 광고(있는 경우)에 대한 것입니다. 그렇지 않으면 다음에 대한 필드가 비어 있음 `TRACE_AD_RESOLVE` 또는 과 동일 `ad_content_url` 대상 `TRACE_AD_INSERT`.

예:

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE 레코드 {#trace-transcoding-no-media-to-transcode}

이 유형의 레코드는 누락된 광고 크리에이티브를 기록합니다. 그 너머에 있는 유일한 필드 `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` 가 테이블에 나타납니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| ad_id | 문자열 | 정규화된 광고 ID(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: 프로토콜:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] 프로토콜: AUDITUDE,VAST) |

이 유형의 레코드는 매니페스트 서버가 CRS에 보내는 트랜스코딩 요청의 결과를 기록합니다. 다음 범위 밖의 필드 `TRACE_TRANSCODING_REQUESTED` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| ad_id | 문자열 | 정규화된 광고 ID |
| ad_manifest_url | 문자열 | 광고 서버 응답에서 광고 매니페스트 파일의 URL |
| creative_type | 문자열 | 미디어 유형 |
| 플래그 | 문자열 | ID3는 트랜스코딩 요청에 ID3 태그를 추가하라는 요청이 포함되어 있는지 여부를 나타낸다 |
| target_duration | 문자열 | 트랜스코딩된 크리에이티브의 Target 기간(초) |

이 유형의 레코드는 서버측 추적을 수행하기 위한 요청을 나타냅니다. 다음 범위 밖의 필드 `TRACE_TRACKING_REQUEST` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| tracking_url_count | 정수 | 추적 URL 수 |
| 시작 | 부동 | PTS 조각 시작 시간(초, 밀리초 단위) |
| 종료 | 부동 | PTS 조각 종료 시간(초, 밀리초 단위) |

이 유형의 레코드는 서버측 추적을 위한 추적 URL을 제공합니다. 다음 범위 밖의 필드 `TRACE_TRACKING_REQUEST_URL` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| timestamp | 부동 | 재생 세션 내에서 추적 URL을 ping할 시간(초, 전체 자릿수 .001). |
| ad_system | 문자열 | 광고 시스템(예: auditude) |
| url | 문자열 | ping할 URL |

매니페스트 서버에서 만드는 이 유형의 로그 요청 레코드 `WEBVTT` 캡션 다음 범위 밖의 필드 `TRACE_WEBVTT_REQUEST` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| vtt_uri | 문자열 | 요청용 URL |
| 시작 | 부동 | 분할 시작 시간(초, 밀리초 단위 정밀도) |
| 종료 | 부동 | 분할 종료 시간(초, 밀리초 단위 정밀도) |

매니페스트 서버가 클라이언트에 보내는 이러한 유형의 로그 응답 레코드 `answer` 에 대한 요청으로 `WEBVTT` 캡션 다음 범위 밖의 필드 `TRACE_WEBVTT_RESPONSE` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| 응답 | 문자열 | 클라이언트로 보낸 Base64 인코딩 응답 |

매니페스트 서버에서 수행하는 요청에 대한 이 유형의 로그 응답 레코드 `WEBVTT` 캡션 다음 범위 밖의 필드 `TRACE_WEBVTT_SOURCE` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | 반환된 HTTP 상태 코드 |
| 소스 | 문자열 | Base64로 인코딩된 원본 VTT 콘텐츠 |

이 유형의 레코드를 사용하면 매니페스트 서버에서 이벤트를 기록하고 광고를 수집할 때 별도로 계획되지 않은 정보를 기록할 수 있습니다. 그 너머의 분야 `TRACE_MISC` 는 메시지 문자열로 구성됩니다. 다음과 같은 메시지가 표시될 수 있습니다.

* 무시된 광고: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= seconds, ignore= ignore, redirectAd= redirectAd, priority= priority
* 광고 배치가 null을 반환했습니다.
* 광고가 성공적으로 결합되었습니다.
* 광고 호출 실패 : 오류 메시지.
* 원시 매니페스트를 가져오기 위해 User-Agent를 추가하는 중: user-agent.
* 원시 매니페스트를 가져오기 위해 쿠키 추가 중: #
* 잘못된 URL 요청 URL 오류 메시지. (변형 URL 구문 분석 실패)
* 호출된 url: URL이 반환됨: 응답 코드. ( 라이브 URL)
* 호출된 url: URL 반환 코드: 응답 코드. ( VOD URL)
* 광고를 해결하는 도중 충돌 발견: 미드롤 시작 또는 미드롤 끝 중 하나가 미드롤(VOD)에 포함된 프리롤 또는 프리롤 내에 속합니다.
* URI: 요청 URL에 대한 처리기에서 예외가 throw되었습니다.
* 변형 매니페스트 생성을 완료했습니다. (변형)
* 변형 매니페스트 생성을 완료했습니다.
* VAST 리디렉션 *리디렉션 URL *오류: 오류 메시지를 처리하는 동안 예외가 발생했습니다.
* 광고 매니페스트 URL에 대한 광고의 재생 목록을 가져오지 못했습니다.
* 타깃팅된 매니페스트를 생성하지 못했습니다. (HLSManifestResolver)
* 첫 번째 광고 호출 응답을 구문 분석하지 못했습니다. 오류 메시지.
* 경로: 요청 URL에 대해 *GET|POST *요청을 처리하지 못했습니다. (라이브/VOD)
* 라이브 매니페스트 요청을 처리하지 못했습니다. 요청 URL. (라이브)
* 변형 매니페스트를 반환하지 못했습니다. 오류 메시지.
* 그룹 ID: 그룹 ID의 유효성을 검사하지 못했습니다.
* 원시 매니페스트를 가져오는 중: 컨텐츠 URL. (라이브)
* 다음 VAST 리디렉션: 리디렉션 URL.
* 빈 공간을 찾았습니다. (VOD)
* 찾음 *숫자* 광고. (VOD)
* HTTP 요청을 받았습니다. (첫 번째 메시지)
* 광고 응답 기간(*광고 응답 기간 *초)과 실제 광고 기간(*실제 기간 *초)의 차이가 제한보다 크므로 광고를 무시합니다. (HLSManifestResolver)
* ID 값을 제공하지 않은 가용성을 무시합니다. (GroupAdResolver.java)
* 잘못된 시간 값을 제공한 사용을 무시합니다. *time *for availId = avail ID.
* 잘못된 기간 값을 제공한 사용을 무시합니다. *duration *for availId = avail ID.
* 새 세션 초기화. (변형)
* 잘못된 HTTP 메서드. GET 모양이군요. (VOD)
* 잘못된 HTTP 메서드. 추적 요청은 GET여야 합니다. (라이브)
* 잘못된 URL 요청 URL 오류 메시지. (변형)
* 잘못된 그룹입니다. (HLSManifestResolver)
* 잘못된 요청입니다. 캡션은 유효한 추적 요청이 아닙니다. (VOD)
* 잘못된 요청입니다. 캡션 요청은 세션이 설정된 후에 수행해야 합니다. (VOD)
* 잘못된 요청입니다. 추적 요청은 세션이 설정된 후에 수행해야 합니다. (VOD)
* 오버로드 그룹 ID: 그룹 ID에 대한 서버 인스턴스가 잘못되었습니다. (라이브)
* VAST 리디렉션 한도에 도달했습니다 - 수.
* 광고 호출 수행: 광고 호출 URL.
* 다음에 대한 매니페스트를 찾을 수 없음: 콘텐츠 URL. (라이브)
* Avail ID: avail ID에 대해 일치하는 항목을 찾을 수 없습니다. (HLSManifestResolver)
* 재생 세션을 찾을 수 없습니다. (HLSManifestResolver)
* 매니페스트 콘텐츠 URL에 대한 VOD 요청을 처리하는 중입니다.
* 변형 처리 중
* 매니페스트 콘텐츠 URL에 대한 캡션 요청을 처리하는 중입니다.
* 추적 요청을 처리하는 중입니다. (VOD)
* 리디렉션 광고 응답이 비어 있습니다. ( VASTStAX)
* 요청: URL.
* 재생 세션을 찾을 수 없어 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 내부 서버 오류로 인해 GET 요청에 대한 오류 응답을 반환합니다.
* 잘못된 자산을 지정하는 GET 요청에 대한 오류 응답 반환: 광고 요청 ID. (VOD)
* 잘못되거나 빈 그룹 ID: 그룹 ID를 지정하는 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 잘못된 추적 위치 값을 지정하는 GET 요청에 대한 오류 응답을 반환합니다. (VOD)
* 잘못된 구문 - 요청 URL을 가진 GET 요청에 대한 오류 응답을 반환합니다. (라이브/VOD)
* 지원되지 않는 HTTP 메서드: GET|POST이 있는 요청에 대한 오류 응답을 반환합니다. (라이브/VOD)
* 캐시에서 매니페스트를 반환합니다. (VOD)
* 서버가 오버로드되었습니다. 광고 결합 요청 없이 진행합니다. (변형)
* 타깃팅된 매니페스트를 생성하기 시작합니다. (HLSManifestResolver)
* 다음 위치에서 변형 매니페스트 생성을 시작: 콘텐츠 URL. (변형)
* 광고를 매니페스트로 결합합니다. (VODHLSResolver)
* 광고 결합 시도 중 `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durationSeconds= seconds, ignore= ignore, redirectAd= 리디렉션 광고, 우선순위= 우선순위.\] \(HLSManifestResolver\)
* 잘못된 pttimeline으로 인해 광고를 가져올 수 없습니다. - 광고가 없는 콘텐츠를 반환했습니다. (VOD)
* 광고를 가져올 수 없음 - 광고 없이 콘텐츠를 반환했습니다. (VOD)
* 광고 쿼리를 가져올 수 없으며 콘텐츠 URL이 제공되지 않았습니다. (VOD)
* 유효한 URL이 수신되었습니다. (VOD/Variant)
* 변형 M3U8을 찾을 수 없습니다. (변형)

### TRACE_재생_진행 레코드 {#trace-playback-progress-records}

매니페스트 서버는 서버측 추적 워크플로 중에 재생 진행에 대한 신호를 수신하면 이러한 종류의 레코드를 생성합니다. 다음 범위 밖의 필드 `TRACE_PLAYBACK_PROGRESS` 표에 표시된 순서대로 표시되며 탭으로 구분됩니다.

| 필드 | 유형 | 설명 |
|---|---|---|
| 상태 | 문자열 | HTTP 상태 코드 |
| 대역폭 | 정수 | 스트림의 대역폭 |
| pts | 정수 | 스트림 내 PTS 시간 |
| ms_time | 정수 | 매니페스트 서버에서 추적 URL을 생성한 시간 |
| url | 문자열 | 리디렉션 URL |
| **0** header_user_agent | 문자열 | HTTP 사용자 에이전트 헤더 |
| **0** header_dnt | 정수 | HTTP do-not-track 헤더 |
| **0** effective_remote_address | 문자열 | IPv4 유효 원격 주소 |
| **0** remote_address | 문자열 | IPv4 원격 주소 |

**0** 마지막 네 필드는 선택 사항입니다.

## 여러 비트 전송률 스트림 {#multiple-bitrate-streams}

광고 삽입에 대한 클라이언트 요청은 일반적으로 변형 M3U8 형식 재생 목록에서 두 개 이상의 비트 전송률을 지정합니다. 매니페스트 서버는 각 비트 전송률에 대해 별도의 M3U8 링크가 포함된 새로운 변형 M3U8 파일을 생성하여 반환합니다. 또한 고유한 그룹 ID를 생성하여 이러한 M3U8을 함께 연결합니다.

매니페스트 서버는 클라이언트의 Bootstrap URL 요청에 있는 정보를 사용하여 콘텐츠 변형 플레이리스트를 검색합니다. 스트림 수준 콘텐츠에 대한 매니페스트 서버 링크를 포함하는 새 변형 재생 목록을 생성합니다. 클라이언트는 이러한 매개 변수를 사용하여 광고 삽입 요청을 구성합니다. 매니페스트 서버의 스트림 수준 콘텐츠 링크는 다음 형식을 갖습니다.

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
매니페스트 서버는 콘텐츠의 재생 목록 유형을 기반으로 이 값을 설정합니다. 라이브/선형(
`#EXT-X-PLAYLIST-TYPE:EVENT`) 또는 VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **게시자 자산 ID**
Bootstrap URL 요청에 제공된 특정 컨텐츠에 대한 게시자의 고유 ID.

* **렌디션**
매니페스트 서버는 다음을 기반으로 이 값을 설정합니다. 
`BANDWIDTH` 컨텐츠 스트림의 값이며, 광고 비트 전송률을 컨텐츠의 비트 전송률과 일치시키기 위해 사용합니다. 비트 전송률이 가장 낮은 광고 렌디션이 초과하지 않는 한 광고 비트 전송률은 콘텐츠의 비트 전송률을 초과할 수 없습니다.

* **groupID**
매니페스트 서버는 이 값을 생성하여 클라이언트가 요청하는 비트율 렌디션에 관계없이 광고를 일관되게 배치하는 데 사용합니다.

* **비트 전송률 스트림의 base64 인코딩 url**
매니페스트 서버 URL-safe base64는 콘텐츠 스트림의 절대 URL을 인코딩합니다. 각 스트림에는 자체 URL이 있습니다.

* **쿼리 매개 변수**
Bootstrap URL 요청에 제공된 쿼리 매개 변수입니다.
