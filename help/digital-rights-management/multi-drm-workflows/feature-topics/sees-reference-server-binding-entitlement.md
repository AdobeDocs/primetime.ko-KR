---
description: SEE 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 부여 서비스를 활성화하는 방법을 보여줍니다.
seo-description: SEE 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 부여 서비스를 활성화하는 방법을 보여줍니다.
seo-title: 참조 서비스 장치 바인딩 권한
title: 참조 서비스 장치 바인딩 권한
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 참조 서비스:장치 바인딩 권한 {#reference-service-device-binding-entitlement}

SEE 참조 서버는 ExpressPlay를 사용하여 장치 바인딩 권한 부여 서비스를 활성화하는 방법을 보여줍니다.

>[!NOTE]
>
>장치 바인딩된 권한 부여 서비스는 시간 제한이 있거나 대여 기간을 제공할 수도 있습니다.

정보를 부트스트랩하려면 더미 M3U8 컨텐츠를 재생합니다. `device_id` 그런 다음 ExpressPlay 토큰에 쿠키를 포함시키고 SPC(이 `device_id`포함)를 생성하고 ExpressPlay Server `getToken` 로 보낼 수 있습니다.

![](assets/fees-device-binding.png)

시퀀스는 더미 M3U8을 재생하여 시작합니다. ExpressPlay 토큰 URL을 가져오기 위해 SEES 서버로 쿠키가 전송됩니다. 쿠키 바인딩된 ExpressPlay 토큰 URL을 받은 후 다음 단계에서는 SPC를 생성하여 ExpressPlay 서버로 보냅니다. ExpressPlay 서버는 SPC에서 `device_id` 쿠키를 추출하고 ExpressPlay 토큰 URL에서 쿠키를 추출하여 쿠키와 트랜잭션 로그에 `device_id` 넣습니다.

클라이언트는 SEES에 동일한 쿠키를 전송하도록 실제 라이센스를 요청합니다. SEES는 쿠키를 사용하여 ExpressPlay 서버에서 `device_id` 을 검색합니다.

SEES는 시간 제한뿐만 아니라 장치 바인딩된 ExpressPlay 토큰을 요청하고 해당 토큰을 클라이언트에 반환합니다.

클라이언트가 ExpressPlay 토큰을 사용하여 라이센스 요청을 합니다.

ExpressPlay 서버는 SPC의 `device_id` 내용을 ExpressPlay 토큰의 `device_id` SPC와 비교합니다. ExpressPlay 서버는 두 `device_id` 값이 일치하는 경우에만 라이센스를 발행합니다.
