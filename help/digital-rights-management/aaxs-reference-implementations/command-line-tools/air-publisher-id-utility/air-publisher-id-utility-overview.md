---
seo-title: AIR 게시자 ID 유틸리티 개요
title: AIR 게시자 ID 유틸리티 개요
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# AIR 게시자 ID 유틸리티 개요 {#air-publisher-id-utility-overview}

AIR 파일 작성 프로세스의 일부로 AIR Developer Tool(ADT)은 Publisher ID를 생성합니다. AIR 파일을 작성하는 데 사용되는 인증서에 고유한 식별자입니다. 여러 AIR 애플리케이션에 대해 동일한 인증서를 재사용하는 경우 동일한 Publisher ID를 갖게 됩니다. AIR Publisher ID 유틸리티는 AIR 애플리케이션에 대한 Publisher ID를 계산하는 데 사용됩니다. 1.5.2 이후 릴리스에서는 생성된 게시자 ID가 파일에 기록되지 않으므로 AIR 응용 프로그램 화이트 리스트를 사용하는 경우 이 도구를 사용하여 게시자 ID를 결정해야 합니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>AIR 허용 목록 실행에 사용되는 게시자 ID는 응용 프로그램 [!DNL application.xml] 파일에서 응용 프로그램 게시자가 지정한 게시자 ID와 다릅니다.

