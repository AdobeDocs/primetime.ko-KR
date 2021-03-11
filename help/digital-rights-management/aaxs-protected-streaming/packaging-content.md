---
title: 콘텐츠 패키징
description: 콘텐츠 패키징
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 콘텐츠 패키징{#packaging-content}

콘텐트를 패키지화할 때 라이선스 서버 URL을 지정해야 합니다. Adobe Access Server URL의 형식은 다음과 같습니다.

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

예를 들어 포트 8080에서 수신되는 라이선스 서버 호스트 이름 &quot;mylicenserver.com&quot;과 &quot;tenant1&quot;이라는 테넌트의 경우 패키징 시에 지정할 라이선스 서버 URL은 다음과 같습니다.

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

각 테넌트가 다른 라이선스 서버 및 전송 자격 증명을 사용하는 경우 패키저에서 올바른 테넌트의 인증서를 지정해야 합니다.

서버에서 알려진 패키저에서 패키지한 컨텐츠에만 라이선스를 발행하도록 하려면 테넌트 구성 파일의 패키지 허용 목록에 패키지 관리자의 인증서를 포함하십시오.
