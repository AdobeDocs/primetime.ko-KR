---
description: TVSDK는 실시간 및 VOD(Video-On-Demand) 미디어의 경우 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에서 정의한 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록과 관련 미디어를 신속하게 선택하고 다운로드 프로세스를 계속합니다.
seo-description: TVSDK는 실시간 및 VOD(Video-On-Demand) 미디어의 경우 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에서 정의한 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록과 관련 미디어를 신속하게 선택하고 다운로드 프로세스를 계속합니다.
seo-title: 미디어 재생 및 장애 조치
title: 미디어 재생 및 장애 조치
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 미디어 재생 및 장애 조치{#media-playback-and-failover}

TVSDK는 실시간 및 VOD(Video-On-Demand) 미디어의 경우 중간 해상도 비트 전송률과 연관된 재생 목록을 다운로드하여 재생을 시작하고 해당 재생 목록에서 정의한 미디어 세그먼트를 다운로드합니다. 고해상도 비트 전송률 재생 목록과 관련 미디어를 신속하게 선택하고 다운로드 프로세스를 계속합니다.

## 재생 목록 장애 조치(failover)가 없습니다. {#section_E6B6A15930894F56A0A8501577B35E7F}

예를 들어 최상위 매니페스트 파일에 지정된 M3U8 파일이 다운로드되지 않으면 TVSDK가 복구를 시도합니다. 복구할 수 없는 경우 애플리케이션에서 다음 단계를 결정합니다.

중간 해상도 비트 전송률과 연결된 재생 목록이 없는 경우 TVSDK는 동일한 해상도의 변형 재생 목록을 검색합니다. 동일한 해상도를 찾으면, 일치하는 위치에서 변형 재생 목록과 세그먼트를 다운로드하기 시작합니다. TVSDK 파섹 비트 전송률이 바로 낮아지는 것이 첫 번째 선택이고, 그 다음 변형이 그 순입니다. 유효한 재생 목록을 찾기 위해 낮은 비트 전송률 재생 목록과 변형이 모두 소진된 경우 TVSDK는 최상위 비트 전송률로 이동하여 계산됩니다. 유효한 재생 목록을 찾을 수 없으면 프로세스가 실패하고 플레이어가 오류 상태로 이동합니다.

애플리케이션에서 이 상황을 처리하는 방법을 결정할 수 있습니다. 예를 들어 플레이어 활동을 닫고 사용자에게 카탈로그 활동으로 안내할 수 있습니다. 관심 이벤트는 `STATUS_CHANGED` 이벤트이고 해당 콜백은 `onStatusChange` 메서드입니다. 플레이어가 내부 상태를 ERROR로 변경하는지 여부를 모니터링하는 코드는 다음과 같습니다.

자세한 내용은 `PSDKDemo` 파일을 참조하십시오. 이벤트 리스너는 MediaPlayer 인스턴스에 연결됩니다.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

클라이언트 측 네트워크가 다운된 경우 이 코드를 사용하여 확인할 수 있습니다.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API는 클라이언트측 네트워크가 다운되었는지 확인하는 데 사용되는 URL을 제공합니다. http 요청에 대해 http 응답 코드 200을 반환하는 유효한 URL이어야 합니다.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

setNetworkDownVerificationUrl이 설정되지 않은 경우 TVSDK는 기본적으로 MainManifest url을 사용하여 네트워크가 다운되었는지 확인합니다.

## 누락된 세그먼트 장애 조치 {#section_ED8CF666289042D39E9914D42BDD9BA4}

세그먼트가 누락된 경우(예: 특정 세그먼트가 다운로드되지 않는 경우) TVSDK는 다양한 장애 조치 시도를 통해 복구를 시도합니다. 복구할 수 없는 경우 오류가 발생합니다.

예를 들어 매니페스트 파일이 없기 때문에 서버에 세그먼트가 없는 경우, 세그먼트를 다운로드할 수 없는 등의 이유로 TVSDK는 다음 옵션을 시도하여 페일오버를 시도합니다.

1. 변형 파일에서 동일한 비트 전송률로 동일한 세그먼트에 대한 장애 조치를 시도합니다.
1. 동일한 파일에서 대체 비트 전송률(ABR 스위치)으로 전환합니다.
1. 사용 가능한 모든 변형의 모든 비트 전송률을 순환합니다.
1. 세그먼트를 건너뛰고 경고를 표시합니다.

TVSDK에서 대체 세그먼트를 가져올 수 없는 경우 `CONTENT_ERROR` 오류 알림이 트리거됩니다. 이 알림에는 코드 `DOWNLOAD_ERROR` 코드가 포함된 내부 알림이 포함되어 있습니다. 문제가 있는 스트림이 대체 오디오 트랙인 경우 TVSDK에서 `AUDIO_TRACK_ERROR` 오류 알림을 생성합니다.

비디오 엔진이 지속적으로 세그먼트를 가져올 수 없는 경우 연속 세그먼트를 5로 건너뛰면 재생이 중지되고 TVSDK가 코드 5와 `NATIVE_ERROR` 함께 문제를 해결합니다.

>[!NOTE]
>
>ABR(응용 비트 전송률) 제어 매개 변수는 장애 조치(failover)가 발생할 때 고려되지 않습니다. 이는 페일오버 메커니즘이 비트 전송률 프로필에 관계없이 현재 사용 가능한 재생 목록을 백업 스트림으로 사용하도록 설계되었기 때문입니다.
>
>장애 조치(failover) 작업 중에 프로필 전환이 있을 수 있습니다. 재생 목록 세그먼트 중 하나를 다운로드하는 동안 오류가 발생하면 ABR 제어 매개 변수(허용되는 최소/최대 비트 전송률)는 무시됩니다.

