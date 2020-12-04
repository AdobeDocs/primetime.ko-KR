---
description: 일부 경우 컨텐츠를 구매하거나 임대할 때 최종 사용자가 여러 장치에서 콘텐츠를 재생하지 못하도록 제한할 수 있습니다. 고객이 Express를 사용하는 경우 ExpressPlay API를 사용하여 사용자의 ExpressPlay 토큰을 사용자의 시스템에 바인딩하면 됩니다.
seo-description: 일부 경우 컨텐츠를 구매하거나 임대할 때 최종 사용자가 여러 장치에서 콘텐츠를 재생하지 못하도록 제한할 수 있습니다. 고객이 Express를 사용하는 경우 ExpressPlay API를 사용하여 사용자의 ExpressPlay 토큰을 사용자의 시스템에 바인딩하면 됩니다.
seo-title: 장치 바인딩
title: 장치 바인딩
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 장치 바인딩{#device-binding}

일부 경우 컨텐츠를 구매하거나 임대할 때 최종 사용자가 여러 장치에서 콘텐츠를 재생하지 못하도록 제한할 수 있습니다. 고객이 Express를 사용하는 경우 ExpressPlay API를 사용하여 사용자의 ExpressPlay 토큰을 사용자의 시스템에 바인딩하면 됩니다.

API는 다음과 같이 사용할 수 있습니다.

1. 쿠키를 생성합니다.
1. 생성된 쿠키가 쿼리 문자열(cookie=`<cookie>`)이나 헤더로 첨부된 더미 토큰 생성 요청을 보냅니다.
1. 사용자의 컴퓨터에서 위 토큰을 사용하여 라이센스 요청을 Express 라이선스 서버로 보내도록 합니다. 예를 들어 더미 컨텐츠를 재생합니다.

   이 더미 라이선스 요청은 성공하면 사용자의 device_id(사용자 장치의 DRM 구현에 의해 계산되거나 생성됨)를 Express 백 엔드의 쿠키에 연결합니다. 이 쿠키는 다음과 같은 방법으로 사용됩니다.

   * 컨텐츠 구매/대여 시 코드는 연결된 쿠키( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))를 보내 사용자의 device_id에 대한 Express 백 엔드를 쿼리합니다.
   * 구입한 컨텐츠의 키(CEK), keyID(CEKSID), 정책 및 기타 정보와 함께 토큰 생성 요청을 보내고 각각 위의 쿠키와 device_id를 추가합니다.`cookie``deviceid`

   * 이 토큰을 사용자에게 제공합니다.

      이 프로세스에서는 사용자의 device_id에 바인딩된 컨텐츠에 대한 토큰을 생성합니다. 사용자의 컴퓨터에서 이 토큰으로 라이센스 요청을 보내면 Express 백 엔드가 해당 토큰의 device_id와 라이센스 요청의 device_id를 교차하여 확인합니다.

      샘플 Express 권한 부여 서버가 이 워크플로를 구현합니다.
