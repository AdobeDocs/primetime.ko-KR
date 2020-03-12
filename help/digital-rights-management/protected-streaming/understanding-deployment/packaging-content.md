---
description: 콘텐트를 패키지할 때 라이센스 서버 URL을 지정해야 합니다.
seo-description: 콘텐트를 패키지할 때 라이센스 서버 URL을 지정해야 합니다.
seo-title: 콘텐츠 패키징
title: 콘텐츠 패키징
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 콘텐츠 패키징{#packaging-content}

콘텐트를 패키지할 때 라이센스 서버 URL을 지정해야 합니다.

Adobe Primetime DRM Server URL은 다음 형식을 사용합니다.

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

예를 들어, 포트 8080에서 수신하는 라이센스 서버 호스트 이름과 `mylicenseserver.com` *`tenant1`*&#x200B;호출하는 테넌트의 경우 컨텐츠를 패키지화할 때 지정하는 라이센스 서버 URL에 대해 다음 구문을 사용합니다.

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

각 테넌트가 다른 라이선스 서버 및 전송 자격 증명을 사용하는 경우 패키저에서 올바른 테넌트의 인증서를 지정해야 합니다.

서버에서 알려진 패키저에서 제공한 컨텐츠에만 라이선스를 발행하는지 확인하려면 테넌트 구성 파일의 패키지 허용 목록에 패키지의 인증서를 포함해야 합니다.
