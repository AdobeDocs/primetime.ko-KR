---
title: AIR 게시자 ID 유틸리티 개요
description: AIR 게시자 ID 유틸리티 개요
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# AIR 게시자 ID 유틸리티 개요 {#air-publisher-id-utility-overview}

AIR 파일을 작성하는 프로세스의 일부로 ADT(AIR Developer Tool)는 Publisher ID를 생성합니다. AIR 파일을 작성하는 데 사용되는 인증서에 고유한 식별자입니다. 여러 AIR 응용 프로그램에 대해 동일한 인증서를 재사용할 경우 동일한 Publisher ID가 사용됩니다.AIR Publisher ID 유틸리티는 AIR 응용 프로그램의 Publisher ID를 계산하는 데 사용됩니다. 1.5.2 이후 AIR 릴리스는 생성된 게시자 ID를 파일에 쓰지 않으므로 AIR 응용 프로그램 허용 목록을 사용하는 경우 이 도구를 사용하여 게시자 ID를 결정해야 합니다.

>[!NOTE]
>
>AIR 허용 목록 실행에 사용되는 게시자 ID는 응용 프로그램의 [!DNL application.xml] 파일에서 응용 프로그램 게시자가 지정한 게시자 ID와 다릅니다.
