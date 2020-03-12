---
description: '매니페스트를 다운로드할 때 TVSDK가 네트워크 연결 상태를 무시하도록 하는 새로운 API가 도입되었습니다. '
seo-description: '매니페스트를 다운로드할 때 TVSDK가 네트워크 연결 상태를 무시하도록 하는 새로운 API가 도입되었습니다. '
seo-title: Android를 사용한 오프라인 재생
title: Android를 사용한 오프라인 재생
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Android를 사용한 오프라인 재생 {#offline-playback-with-android}

매니페스트를 다운로드할 때 TVSDK에서 네트워크 연결 상태를 무시하도록 하는 다음 API가 도입되었습니다. 네트워크 연결 상태는 일반적으로 ABR(응용 비트 전송률) 스트리밍 중에 사용되며, 네트워크를 다시 시작할 때 대비할지를 결정합니다.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

이 설정을 활성화하고 네트워크 연결을 무시할 수 있습니다.

true `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` 로 설정합니다. 부울 값의 기본값은 false입니다.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
