---
title: 컨텐츠 패키징
description: 컨텐츠 패키징
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 컨텐츠 패키징{#packaging-content}

원격 키 전달을 위한 콘텐츠를 패키징할 때 원격 키 전달이 필요함을 지정하는 정책을 사용합니다. 키 서버 URL은 HLS 콘텐츠의 M3U8(매니페스트 파일)에 포함되어야 합니다. Primetime DRM 키 서버 URL의 형식은 다음과 같습니다.

```
https://key-server-host:port/faxsks/tenant-name/key
```

예: 키 서버 호스트 이름 [!DNL mykeyserver.com] 포트 443에서 수신 대기 및 `tenant1`M3U8에서 지정할 키 서버 URL은 다음과 같습니다.

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS 및 Xbox 360 클라이언트 모두에 동일한 URL을 사용할 수 있습니다. 또는, 서버가 클라이언트 타입별로 별도의 테넌트로 구성된 경우, 서로 다른 URL이 사용될 수 있다.

라이센스 서버 URL이 올바르게 구성된 실행 라이센스 서버를 가리키는 한 키 서버가 필요하지 않은 클라이언트에서 동일한 콘텐츠가 재생될 수 있습니다.
