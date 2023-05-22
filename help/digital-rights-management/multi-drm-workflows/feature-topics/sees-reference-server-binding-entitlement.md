---
description: SEES 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 서비스를 활성화하는 방법을 보여 줍니다.
title: 참조 서비스 장치 바인딩 권한
exl-id: 91f9d406-f3f9-47d3-aa50-f47c4e81b9fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# 참조 서비스: 장치 바인딩 권한 {#reference-service-device-binding-entitlement}

SEES 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 서비스를 활성화하는 방법을 보여 줍니다.

>[!NOTE]
>
>장치 바인딩된 권한 부여 서비스는 시간 바인딩되거나 임대 기간을 제공할 수도 있습니다.

부트스트랩하려면 `device_id` 정보, 더미 M3U8 콘텐츠를 재생합니다. 그런 다음 ExpressPlay 토큰에 쿠키를 임베드하고 를 포함하는 SPC를 생성할 수 있습니다. `device_id`) 및 `getToken` ExpressPlay 서버에 연결합니다.

![](assets/fees-device-binding.png)

시퀀스는 더미 M3U8을 재생함으로써 시작된다. ExpressPlay 토큰 URL을 가져오기 위해 SEES 서버로 쿠키가 전송됩니다. 쿠키로 바인딩된 ExpressPlay 토큰 URL을 받은 후 다음 단계는 SPC를 생성하여 ExpressPlay 서버에 보내는 것입니다. ExpressPlay 서버는 `device_id` spc에서 ExpressPlay 토큰 URL의 쿠키를 가져온 다음 `device_id` 트랜잭션 로그에서.

클라이언트는 동일한 쿠키 전송을 보기 위해 실제 라이센스를 요청합니다. 는 쿠키를 사용하여 `device_id` ExpressPlay 서버에서 가져옵니다.

에서는 장치 바인딩되고 시간 바인딩된 ExpressPlay 토큰을 요청하고 해당 토큰을 클라이언트에 반환합니다.

클라이언트는 ExpressPlay 토큰을 사용하여 라이센스를 요청합니다.

ExpressPlay 서버는 `device_id` 을 사용하여 SPC에서 `device_id` ExpressPlay 토큰에 포함됩니다. ExpressPlay 서버는 두 가지 경우에 대해서만 라이센스를 발행합니다 `device_id` 값이 일치합니다.
