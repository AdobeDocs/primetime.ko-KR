---
description: 경우에 따라 콘텐츠를 구매하거나 대여할 때 최종 사용자가 여러 디바이스에서 콘텐츠를 재생하지 못하도록 제한할 수 있습니다. 고객이 Expressplay를 사용하는 경우 Expressplay API를 사용하여 사용자의 Expressplay 토큰을 사용자 컴퓨터에 바인딩하면 됩니다.
title: 장치 바인딩
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 장치 바인딩{#device-binding}

경우에 따라 콘텐츠를 구매하거나 대여할 때 최종 사용자가 여러 디바이스에서 콘텐츠를 재생하지 못하도록 제한할 수 있습니다. 고객이 Expressplay를 사용하는 경우 Expressplay API를 사용하여 사용자의 Expressplay 토큰을 사용자 컴퓨터에 바인딩하면 됩니다.

다음과 같은 방법으로 API를 사용할 수 있습니다.

1. 쿠키를 생성합니다.
1. 생성된 쿠키가 쿼리 문자열로 첨부된 더미 토큰 생성 요청을 보냅니다(cookie=`<cookie>`) 또는 를 헤더로 사용하십시오.
1. 사용자 컴퓨터에서 더미 콘텐츠를 재생하는 등의 방법으로 위의 토큰을 사용하여 Expressplay 라이선스 서버에 라이선스 요청을 보내도록 합니다.

   이 더미 라이센스 요청이 성공하면 사용자의 device_id(사용자의 장치에서 DRM 구현에 의해 계산되거나 생성됨)를 Expressplay 백 엔드의 쿠키에 연결합니다. 그런 다음 이 쿠키는 다음과 같은 방식으로 사용됩니다.

   * 콘텐츠 구매/대여 시, 코드는 관련 쿠키( )를 전송하여 사용자의 device_id에 대한 Expressplay 백 엔드를 쿼리합니다. [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * 위의 cookie 및 device_id를 각각 로 첨부하여 구매한 콘텐츠의 키(CEK), 키 ID(CEKSID), 정책 및 기타 정보로 토큰 생성 요청을 보냅니다. `cookie` 상관 관계 매개 변수 및 `deviceid` 토큰 제한 매개 변수.

   * 이 토큰을 사용자에게 제공합니다.

     이 프로세스는 사용자의 device_id에 바인딩된 컨텐츠에 대한 토큰을 생성합니다. 사용자의 컴퓨터에서 이 토큰이 포함된 라이선스 요청을 보내면 Expressplay 백 엔드가 토큰의 device_id와 라이선스 요청의 device_id를 상호 확인합니다.

     샘플 Expressplay 권한 서버는 이 워크플로를 구현합니다.
