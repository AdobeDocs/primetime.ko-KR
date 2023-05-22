---
description: 토큰 요청을 적절한 Expressplay 토큰 서버로 전송하여 암호화된 콘텐츠에 대한 Expressplay 토큰을 생성할 수 있습니다.
title: Expressplay 토큰
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Expressplay 토큰 {#expressplay-tokens}

토큰 요청을 적절한 Expressplay 토큰 서버로 전송하여 암호화된 콘텐츠에 대한 Expressplay 토큰을 생성할 수 있습니다.

다음 URL을 예로 들 수 있습니다.

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

에 지정된 콘텐츠 암호화 키 저장소 ID 또는 CEKSID `kid` 매개 변수 및 콘텐츠 암호화 키 또는 CEK가 `contentKey` 매개 변수는 패키징에 사용되는 콘텐츠 암호화 키 저장소 ID 및 콘텐츠 암호화 키와 일치해야 합니다. 다음 텍스트는 토큰 서버 응답의 예입니다.

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

그러면 다음 중 하나를 수행할 수 있습니다

* 반환된 URL 및 쿼리를 라이선스 서버 URL로 사용하거나
* url에서 쿼리를 꺼내고 ExpressPlayToken을 HTTP POST 헤더로 별도로 전달합니다
