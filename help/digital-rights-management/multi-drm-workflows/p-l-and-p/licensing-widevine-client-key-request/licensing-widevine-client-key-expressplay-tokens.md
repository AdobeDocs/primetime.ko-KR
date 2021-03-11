---
description: 토큰 요청을 해당 ExpressPlay 토큰 서버로 보내 암호화된 내용에 대한 Express 토큰을 생성할 수 있습니다.
title: 표현식 토큰
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# 표현식 토큰 {#expressplay-tokens}

토큰 요청을 해당 ExpressPlay 토큰 서버로 보내 암호화된 내용에 대한 Express 토큰을 생성할 수 있습니다.

예를 들면 다음과 같은 URL이 있습니다.

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

`kid` 매개 변수에 지정된 컨텐츠 암호화 키 저장소 ID 또는 CEKSID와 `contentKey` 매개 변수에 지정된 컨텐츠 암호화 키 또는 CEK는 패키징에 사용되는 컨텐츠 암호화 키 저장소 ID 및 컨텐츠 암호화 키와 일치해야 합니다. 다음 텍스트는 토큰 서버 응답의 예입니다.

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

그런 다음

* 반환된 URL 및 쿼리를 라이선스 서버 URL로 사용하거나
* URL에서 쿼리를 가져와서 ExpressPlayToken을 HTTP POST 헤더로 개별적으로 전달합니다.