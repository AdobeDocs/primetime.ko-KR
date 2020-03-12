---
seo-title: 라이선스 서버 빌드
title: 라이선스 서버 빌드
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 라이선스 서버 빌드 {#building-the-license-server}

참조 구현 라이센스 서버에는 라이센스 서버를 배포하기 위한 WAR 파일이 포함되어 있습니다. 또한 모든 라이선스 서버 소스 코드와 Ant 빌드 스크립트(Implementation\Server\refimpl\build-refimpl.xml 참조)가 포함되어 있으므로 코드를 손쉽게 변경할 수 있습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>이 단계는 소스 코드를 수정하려는 경우에만 필요합니다. 평가를 위해 이 단계를 건너뛰고 배송된 WAR 파일을 사용할 수 있습니다.

Ant 스크립트를 실행하기 전에 스크립트를 수정하여 Adobe Access SDK, Tomcat, MySQL 및 Log4J의 위치를 지정합니다. 텍스트 편집기에서 build-refimpl.xml을 열고 속성 값을 편집합니다 `sdkdir, tomcatdir, mysqldir, and log4jdir`. 소스 코드를 컴파일하고 참조 구현을 위한 WAR 파일을 만들려면 Ant 스크립트를 포함하는 `ant -f build-refimpl.xml all` 디렉토리에서 스크립트를 사용하여 실행합니다. 스크립트가 완료되면 서버 WAR 파일이 들어 있는 [!DNL refimpl-build/wars] 디렉토리가 생성됩니다.
