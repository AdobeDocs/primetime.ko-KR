---
seo-title: 콘텐츠 패키징
title: 콘텐츠 패키징
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# 콘텐츠 패키징{#packaging-content}

원격 키 전달을 위한 컨텐츠를 패키지화할 때는 원격 키 전달이 필수임을 지정하는 정책을 사용합니다. 키 서버 URL은 HLS 컨텐츠의 M3U8(매니페스트 파일)에 포함되어야 합니다. Primetime DRM 키 서버 URL의 형식은 다음과 같습니다.

```
https://key-server-host:port/faxsks/tenant-name/key
```

예를 들어 포트 443에서 [!DNL mykeyserver.com] 수신하는 키 서버 호스트 이름과 이름이 명명된 테넌트의 경우 M3U8에서 지정할 주요 서버 URL `tenant1`은 다음과 같습니다.

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

iOS와 Xbox 360 클라이언트 모두에 동일한 URL을 사용할 수 있습니다. 또는 서버가 각 클라이언트 유형에 대해 별도의 임차인으로 구성된 경우 다른 URL을 사용할 수 있습니다.

라이센스 서버 URL이 올바르게 구성된 실행 중인 라이센스 서버를 가리키는 한, 키 서버가 필요하지 않은 클라이언트에서도 동일한 컨텐츠를 재생할 수 있습니다.
