---
seo-title: 패키지된 컨텐츠 테스트
title: 패키지된 컨텐츠 테스트
uuid: 99df417a-85ce-45da-bfcf-33df2197bf5b
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b

---


# 패키지된 컨텐츠 테스트 {#test-the-packaged-content}

공개적으로 사용 가능한 Adobe Primetime 데스크탑 플레이어(Flash Player를 통해)를 사용하여 패키징 작업이 성공했는지 확인해야 합니다. 이 플레이어는 HDS 컨텐츠만 지원할 수 있습니다. HLS 콘텐츠를 테스트하려면 Primetime 브라우저 TVSDK 지원 플레이어가 필요합니다.

1. 웹 서버에서 컨텐츠를 호스팅합니다.
1. https://drmtest2.adobe.com:8080/AccessPlayer/player.html에서 Primetime DRM(이전 Adobe Access) 플레이어를 시작합니다.
1. HDS 매니페스트( [!DNL .f4m])에 URL을 복사하여 플레이어의 탐색 필드에 붙여 넣고 **[!UICONTROL Play]** 단추를 클릭합니다.
