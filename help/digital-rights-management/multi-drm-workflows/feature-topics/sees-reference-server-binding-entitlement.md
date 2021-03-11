---
description: SEES 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 부여 서비스를 활성화하는 방법을 보여줍니다.
title: 참조 서비스 장치 바인딩 권한
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# 참조 서비스:장치 바인딩 자격 부여 {#reference-service-device-binding-entitlement}

SEES 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 부여 서비스를 활성화하는 방법을 보여줍니다.

>[!NOTE]
>
>디바이스 제공 권한 부여 서비스는 시간 제한이나 대여 기간을 제공할 수도 있습니다.

`device_id` 정보를 부트스트래핑하려면 더미 M3U8 컨텐츠를 재생합니다. 그런 다음 ExpressPlay 토큰에 쿠키를 포함하여 SPC(`device_id`이 포함)를 생성하고 `getToken`을 ExpressPlay 서버로 보낼 수 있습니다.

![](assets/fees-device-binding.png)

시퀀스는 더미 M3U8을 재생하여 시작합니다. ExpressPlay 토큰 URL을 가져오기 위해 SEES 서버로 쿠키가 전송됩니다. 쿠키 바인딩된 ExpressPlay 토큰 URL을 받은 후 다음 단계는 SPC를 생성하여 ExpressPlay 서버로 보내는 것입니다. ExpressPlay 서버는 SPC에서 `device_id`, ExpressPlay 토큰 URL의 쿠키를 추출하고, 이 쿠키와 `device_id`을 거래 로그에 넣습니다.

클라이언트는 SEES에 동일한 쿠키를 전송하는 실제 라이센스를 요청합니다. SEES는 쿠키를 사용하여 ExpressPlay 서버에서 `device_id`을 검색합니다.

SEES는 시간 바인딩뿐만 아니라 장치 바인딩된 ExpressPlay 토큰을 요청하고 해당 토큰을 클라이언트에 반환합니다.

클라이언트가 ExpressPlay 토큰으로 라이센스 요청을 합니다.

ExpressPlay 서버는 SPC의 `device_id`을 ExpressPlay 토큰의 `device_id`과 비교합니다. ExpressPlay 서버는 두 `device_id` 값이 일치하는 경우에만 라이센스를 발행합니다.
