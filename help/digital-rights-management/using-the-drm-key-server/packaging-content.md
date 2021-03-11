---
title: 콘텐츠 패키징
description: 콘텐츠 패키징
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# 콘텐츠 패키징{#packaging-content}

원격 키 전달을 위한 컨텐츠를 패키지화할 때는 원격 키 전달이 필수임을 지정하는 정책을 사용하십시오. 키 서버 URL은 HLS 내용의 M3U8(매니페스트 파일)에 포함되어야 합니다. Primetime DRM 키 서버 URL의 형식은 다음과 같습니다.

```
https://key-server-host:port/faxsks/tenant-name/key
```

예를 들어 포트 443에서 수신 대기 중인 키 서버 호스트 이름 [!DNL mykeyserver.com] 및 `tenant1` 테넌트의 경우 M3U8에서 지정할 키 서버 URL은 다음과 같습니다.

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS 및 Xbox 360 클라이언트 모두에 동일한 URL을 사용할 수 있습니다. 또는 서버가 각 클라이언트 유형에 대해 별도의 테넌트로 구성된 경우 다른 URL을 사용할 수 있습니다.

라이센스 서버 URL이 올바르게 구성된 실행 라이센스 서버를 가리키는 한 키 서버가 필요하지 않은 클라이언트에서도 동일한 컨텐츠를 재생할 수 있습니다.
