---
description: 콘텐츠를 패키징할 때 라이선스 서버 URL을 지정해야 합니다.
title: 컨텐츠 패키징
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# 컨텐츠 패키징{#packaging-content}

콘텐츠를 패키징할 때 라이선스 서버 URL을 지정해야 합니다.

Adobe Primetime DRM 서버 URL은 다음 형식을 사용합니다.

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

예를 들어 라이센스 서버 호스트 이름의 경우 `mylicenseserver.com` 는 포트 8080에서 수신 대기하며 테넌트는 *`tenant1`*, 콘텐츠를 패키징할 때 지정하는 라이선스 서버 URL에 대해 다음 구문을 사용합니다.

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

각 테넌트가 서로 다른 라이선스 서버 및 전송 자격 증명을 사용하는 경우 패키지 관리자에서 올바른 테넌트의 인증서를 지정해야 합니다.

서버에서 알려진 패키저의 콘텐츠에만 라이선스를 발급하는지 확인하려면 테넌트 구성 파일의 packager 허용 목록에 packager 인증서를 포함해야 합니다.
