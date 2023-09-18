---
description: 매니페스트를 다운로드할 때 TVSDK에 네트워크 연결 상태를 무시하도록 지시하는 새 API가 도입되었습니다.
title: Android에서 오프라인 재생
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Android에서 오프라인 재생 {#offline-playback-with-android}

매니페스트를 다운로드할 때 TVSDK에 네트워크 연결 상태를 무시하도록 지시하는 다음 API가 도입되었습니다. 네트워크 연결 상태는 일반적으로 ABR(적응형 비트 전송률 스트리밍) 중에 폴백을 시도할지 또는 네트워크가 다시 시작될 때까지 기다리는지 확인하는 데 사용됩니다.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

이 설정을 사용하고 네트워크 연결을 무시할 수 있습니다.

설정 `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` true로 설정합니다. 부울의 기본값은 false입니다.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
