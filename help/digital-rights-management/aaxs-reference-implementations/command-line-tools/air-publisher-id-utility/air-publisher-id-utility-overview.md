---
title: AIR Publisher ID 유틸리티 개요
description: AIR Publisher ID 유틸리티 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# AIR Publisher ID 유틸리티 개요 {#air-publisher-id-utility-overview}

AIR 파일을 작성하는 과정의 일부로 AIR 개발자 도구(ADT)는 게시자 ID를 생성합니다. AIR 파일을 작성하는 데 사용되는 인증서에 고유한 식별자입니다. 여러 AIR 응용 프로그램에 대해 동일한 인증서를 재사용하는 경우 동일한 게시자 ID를 갖게 됩니다.AIR 게시자 ID 유틸리티는 AIR 응용 프로그램에 대한 게시자 ID를 계산하는 데 사용됩니다. 1.5.2 이후의 AIR 릴리스에서는 생성된 게시자 ID를 파일에 쓰지 않으므로 AIR 애플리케이션 허용 목록을 사용하는 경우 이 도구를 사용하여 게시자 ID를 확인해야 합니다.

>[!NOTE]
>
>AIR 허용 목록 적용에 사용되는 게시자 ID가 애플리케이션의 [!DNL application.xml] 파일.
