---
description: 이 표에서는 수익 최적화 알림에 대한 자세한 정보를 제공합니다.
title: 수익 최적화 코드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 수익 최적화 코드 {#revenue-optimization-code}

이 표에서는 수익 최적화 알림에 대한 자세한 정보를 제공합니다.

## 수익 최적화 보고 활성화 {#enable-revenue-optimization-reporting}

이 보고를 사용하려면 PTMediaPlayer API를 사용하십시오. `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>대부분의 정보 알림에는 관련 메타데이터(예: 다운로드하지 못한 리소스의 URL)가 포함되어 있습니다. 일부 알림에는 기본 비디오 콘텐츠, 대체 오디오 콘텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함됩니다.

| 코드 | 이름 | 내부 알림 | 메타데이터 키 | 댓글 |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | 없음 | 다른 이벤트를 기반으로 하는 메타데이터 키는 아래 표를 참조하십시오. | 없음 |

| 이벤트 세부 정보 | 컨텍스트 메타데이터 |
|---|---|
| **CONTENT_RESOURCE_START** MediaPlayer::replaceCurrentResource가 호출될 때 TVSDK에서 전달됩니다. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** 콘텐츠가 준비된 상태에 들어가고 재생할 준비가 되면 TVSDK에서 발송됩니다. 이 이벤트는 모든 매니페스트 업로드 시 발송되지 않으며 초기 로드 시에만 발송됩니다. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** 영업 기회가 생성되면 TVSDK에서 발송됩니다. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 기회 해결이 시작되면 TVSDK에서 발송됩니다. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** ad resolver가 MediaPlayerClient::notifyFailed()를 호출할 때 TVSDK에서 발송됩니다. 데이터 입력 필요 | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** URL로 광고 리소스를 가져오는 경우 발송됩니다. responseStartTime:요청이 처음 시작된 시간의 Unix 타임스탬프입니다. responseTotalTime:응답이 로드되는 데 걸린 총 시간(초)입니다. responseStatus:리소스를 가져오는 동안 발생한 상태 코드입니다. status:&quot;error&quot; 또는 &quot;success&quot; referrerAdId:이 리소스의 가져오기를 요청한 참조 광고 ID입니다(있는 경우). referrerUrl:이 리소스의 가져오기를 요청한 참조 URL입니다. errorMessage:상태가 &quot;error&quot;이면 오류 원인이 여기에 있습니다. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** CRS가 자산에 적용되면 TVSDK에서 발송되고 m3u8에 대한 응답도 발송됩니다. resourceType:always &quot;crs&quot;. responseStartTime:요청이 처음 시작된 시간의 Unix 타임스탬프입니다. responseTotalTime:응답이 로드되는 데 걸린 총 시간(초)입니다. responseStatus:리소스를 가져오는 동안 발생한 상태 코드입니다. 상태: &quot;error&quot; 또는 &quot;success&quot; errorMessage:상태가 &quot;error&quot;이면 오류 원인이 여기에 있습니다. mediaFileUrl:선택한 원래 미디어 파일 URL입니다. mediaFileBitrate: 선택한 미디어 파일의 비트율입니다. mediaFileMimeType: 선택한 미디어 파일의 mime 유형입니다. url:최종 에셋 url. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** 타임라인에 adBreak가 배치된 후 TVSDK에서 발송됩니다. 이 이벤트는 각 광고 브레이크에 대해 한 번 발생합니다. proposedTime:광고 브레이크를 배치할 것을 요청한 시간입니다. actualTime:광고 브레이크가 실제로 배치된 시간입니다. proposedDuration:삽입이 요청된 광고 브레이크의 기간입니다. 라이브 콘텐츠의 경우 큐 지속 시간이 됩니다. VOD 콘텐츠의 경우 일반적으로 -1입니다. actualDuration:삽입된 광고 브레이크의 실제 기간입니다. 원래 스트림 타임라인에서 추가되거나 대체된 각 세그먼트 기간으로 정의된 모든 광고의 합계 기간으로 계산됩니다. proposedAds:제안된 광고 브레이크의 광고 수입니다. totalAds:성공적으로 배치된 광고 수입니다. ads...n:성공적으로 삽입한 광고가 여기에 삽입됩니다. AD_OPPORTUNITY_RESOLVE_PROCESS에서 전체 광고 매니페스트 정보를 검색할 수 있습니다. | opportunityId, status, errorMessage, proposedTime, proposedDuration, actualTime, actualDuration, proposedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** 광고가 재생을 시작한 후 TVSDK에서 발송됩니다. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** 광고가 재생을 완료한 후 TVSDK에서 발송됩니다. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** Adbreak가 재생을 시작할 때 TVSDK에서 전달됩니다. | clientTimestamp, event, opportunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Adbreak가 재생을 완료할 때 TVSDK에서 전달됩니다. | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** 컨텐츠가 완료되면 TVSDK에서 발송됩니다. 이는 스트림이 교체되거나, 플레이어가 오류 상태에 들어가거나, 플레이어가 재설정되거나, 컨텐츠가 실제로 완료되면 발생할 수 있습니다. 이 이벤트는 sessionId를 추적하는 데 필요합니다. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_오류** 광고 재생 도중 오류 발생(변형 스트림 오류) 시 TVSDK에서 발송됩니다. | event, error, Timestamp, manifestUrl, time, opportunityId, url |
