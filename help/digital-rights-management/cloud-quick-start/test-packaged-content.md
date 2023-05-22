---
title: 패키지된 콘텐츠 테스트
description: 패키지된 콘텐츠 테스트
copied-description: true
exl-id: 98456bf8-5d4d-47a7-905a-e6dac1e826ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 패키지된 콘텐츠 테스트 {#test-the-packaged-content}

공개적으로 사용 가능한 Adobe Primetime 데스크탑 플레이어를 사용하여 패키징 작업이 성공했는지 확인해야 합니다(Flash Player 이용). 이 플레이어는 HDS 콘텐츠만 지원할 수 있습니다. HLS 콘텐츠를 테스트하려면 Primetime 브라우저 TVSDK를 사용할 수 있는 플레이어가 필요합니다.

1. 웹 서버에서 콘텐츠를 호스팅합니다.
1. https://drmtest2.adobe.com:8080/AccessPlayer/player.html에서 Primetime DRM(이전 명칭: Adobe 액세스) 플레이어를 시작합니다.
1. HDS 매니페스트에 URL 붙여넣기( [!DNL .f4m])을 클릭하여 플레이어의 탐색 필드를 선택합니다. **[!UICONTROL Play]** 단추를 클릭합니다.
