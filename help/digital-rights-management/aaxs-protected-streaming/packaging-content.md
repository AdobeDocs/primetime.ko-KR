---
title: 컨텐츠 패키징
description: 컨텐츠 패키징
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 컨텐츠 패키징{#packaging-content}

콘텐츠를 패키징할 때 라이선스 서버 URL을 지정해야 합니다. Adobe Access Server URL의 형식은 다음과 같습니다.

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

예를 들어, 포트 8080에서 수신하는 라이선스 서버 호스트 이름 &quot;mylicenseserver.com&quot; 및 &quot;tenant1&quot;이라는 테넌트의 경우 패키징 시 지정할 라이선스 서버 URL은 다음과 같습니다.

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

각 테넌트가 서로 다른 라이선스 서버 및 전송 자격 증명을 사용하는 경우 패키지 관리자에서 올바른 테넌트의 인증서를 지정해야 합니다.

서버가 알려진 패키저로 패키징된 콘텐츠에만 라이선스를 발급하는지 확인하려면 테넌트 구성 파일의 packager 허용 목록에 packager 인증서를 포함하십시오.
