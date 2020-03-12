---
description: '이 표에서는 매출 최적화 알림에 대한 자세한 정보를 제공합니다. '
seo-description: '이 표에서는 매출 최적화 알림에 대한 자세한 정보를 제공합니다. '
seo-title: 수익 최적화 코드
title: 수익 최적화 코드
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 수익 최적화 코드 {#revenue-optimization-code}

이 표에서는 매출 최적화 알림에 대한 자세한 정보를 제공합니다.

## 매출 최적화 보고 활성화 {#enable-revenue-optimization-reporting}

이 보고를 활성화하려면 PTMediaPlayer api를 사용합니다. `[mediaPlayer
setRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`Adobe

[!N참고]:대부분의 정보 알림에는 다운로드하지 못한 리소스의 URL과 같은 관련 메타데이터가 포함되어 있습니다. 일부 알림에는 주 비디오 컨텐츠, 대체 오디오 컨텐츠 또는 광고에서 문제가 발생했는지 여부를 지정하는 메타데이터가 포함되어 있습니다.

|코드|이름|내부 알림|메타데이터 키|주석||—|—|—|—|—|—||401001| REVENUE_OPTIMIZATION_REPORTING| 없음| 다른 이벤트를 기반으로 하는 메타데이터 키는 아래 표를 참조하십시오. | 없음|

| 이벤트 세부 사항 | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** MediaPlayer::replaceCurrentResource가 호출될 때 TVSDK에서 전달됩니다. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignaturesMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** 컨텐츠가 준비 상태로 전환되어 재생할 준비가 되면 TVSDK에서 전달됩니다. 이 이벤트는 모든 매니페스트 업로드에서 전달되지 않습니다. 초기 로드 시에만 전달됩니다. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** 기회가 생성될 때 TVSDK에서 전달됩니다. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 영업 기회 해결을 시작할 때 TVSDK에서 전달됩니다. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** 광고 확인자가 MediaPlayerClient::notifyFailed()를 호출할 때 TVSDK에서 전달됩니다. 데이터 입력 필요 | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** URL로 광고 리소스를 가져올 때 전달됩니다. responseStartTime:요청이 처음 시작될 때의 Unix 타임스탬프 responseTotalTime:로드 응답에 걸린 총 시간(초)입니다. responseStatus:리소스를 가져오는 동안 발생한 상태 코드입니다. status:&quot;error&quot; 또는 &quot;success&quot; referrerAdId:이 리소스의 페치를 요청한 참조 광고 ID(있는 경우)입니다. referrerUrl:이 리소스의 가져오기를 요청한 참조 URL입니다. errorMessage:상태가 &quot;error&quot;인 경우 오류의 원인이 여기에 있습니다. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** CRS가 자산에 적용될 때 TVSDK에 전달되고 m3u8에 대한 응답이 전달됩니다. resourceType:always &quot;crs&quot;. responseStartTime:요청이 처음 시작될 때의 Unix 타임스탬프 responseTotalTime:로드 응답에 걸린 총 시간(초)입니다. responseStatus:리소스를 가져오는 동안 발생한 상태 코드입니다. status:&quot;error&quot; 또는 &quot;success&quot; errorMessage:상태가 &quot;error&quot;인 경우 오류의 원인이 여기에 있습니다. mediaFileUrl:선택한 원본 미디어 파일 URL입니다. mediaFileBitrate:선택한 미디어 파일의 비트 전송률입니다. mediaFileMimeType:선택한 미디어 파일의 MIME 유형입니다. url:최종 자산 URL입니다. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** 타임라인에 adBreak가 배치된 후 TVSDK에서 전달됩니다. 이 이벤트는 각 광고 중단에 대해 한 번 발생합니다. proposedTime: 광고 브레이크가 요청된 시간입니다. actualTime: 광고 브레이크가 실제로 배치된 시간입니다. proposedDuration:삽입을 위해 요청된 광고 브레이크의 지속 시간입니다. 라이브 컨텐츠의 경우 큐 지속 시간이 됩니다. VOD 콘텐츠의 경우 일반적으로 -1입니다. actualDuration:삽입된 광고 분리의 실제 지속 시간입니다. 해당 세그먼트 지속 시간으로 정의된 모든 광고의 합계 지속 시간으로 계산되며, 원래 스트림 타임라인에서 추가 또는 대체됩니다. proposedAds:제안된 광고 브레이크의 광고 수입니다. totalAds:성공적으로 배치한 광고의 수입니다. 광고...n: 성공적으로 삽입된 광고가 여기에 삽입됩니다. 전체 광고 매니페스트 정보는 AD_OPPORTUNITY_RESOLVE_PROCESS에서 검색할 수 있습니다. | opportunityId, status, errorMessage, proposedTime, proposedDuration, actualTime, proposedDuration, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** 광고가 재생을 시작한 후 TVSDK에서 전달됩니다. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** 광고가 재생을 완료한 후 TVSDK에서 전달됩니다. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** adbreak가 재생을 시작할 때 TVSDK에서 전달됩니다. | clientTimestamp, event, opportunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** TVSDK에서 adbreak 재생이 완료될 때 전달됩니다. | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** 컨텐츠가 완료되면 TVSDK에서 전달됩니다.스트림 교체, 플레이어가 오류 상태 입력, 플레이어 재설정 또는 컨텐츠가 실제로 완료된 경우 이 문제가 발생할 수 있습니다. 이 이벤트는 sessionId를 추적하는 데 필요합니다. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** 광고의 재생 오류(변형 스트림 오류)가 발생하면 TVSDK에서 전달됩니다. | event, error, Timestamp, manifestUrl, time, opportunityId, url |