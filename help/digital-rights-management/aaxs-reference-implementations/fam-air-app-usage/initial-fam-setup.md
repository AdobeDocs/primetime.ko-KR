---
description: 'null'
seo-description: 'null'
seo-title: 초기 Flash Access 관리자 설정
title: 초기 Flash Access 관리자 설정
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# 초기 Flash Access 관리자 설정 {#initial-flash-access-manager-setup}

Flash Access 관리자를 설정하려면 다음 절차를 따르십시오.

1. Packager 서버 배포. 이 서버는 방화벽 내의 사용자만 사용할 수 있어야 합니다(공개 컴퓨터에 이 소프트웨어를 배포하지 마십시오). 서버 배포에 대한 자세한 내용은 [라이선스 서버 배포 및 관리되는 폴더 패키지](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md)를 참조하십시오.

   * [!DNL flashaccess-packager.war]을 Tomcat의 웹 앱 폴더에 복사합니다.
   * 리소스의 [!DNL flashaccess-refimpl-packager.properties]을 클래스 경로의 위치로 복사합니다.
   * 서버를 시작합니다. 속성 파일에 문제가 있어 몇 가지 오류가 표시됩니다.속성이 아직 채워지지 않았기 때문에 가능합니다.

1. [!DNL .air] 파일을 실행하여 Flash Access Manager AIR 응용 프로그램을 설치합니다(AIR 1.5 이상 필요).
1. Flash Access Manager AIR 애플리케이션을 실행합니다.

   서버가 `https://localhost:8080*` 이외의 다른 곳에서 실행 중이면 응용 프로그램이 서버에 연결할 수 없다는 오류가 표시됩니다. 오류 대화 상자를 닫고 [환경 설정] 탭에서 Packager Server URL에 대한 올바른 URL을 입력합니다. 서버가 지정된 URL에서 실행되고 속성 파일이 클래스 경로에 있는 경우 [환경 설정] 화면이 속성 파일의 값으로 채워집니다. Packager 서버 URL을 설정하면 AIR 응용 프로그램에서 이 설정을 기억하므로 다음에 응용 프로그램을 실행할 때 이 설정을 입력하지 않아도 됩니다.
1. 환경 설정 탭에서 값을 채우고 **[!UICONTROL Save]**&#x200B;을 클릭합니다.
1. 감시된 폴더를 사용하려면 3단계에서 발생한 오류를 복구하려면 서버를 다시 시작해야 합니다. 기본 설정이 제대로 구성되면 시작 중에 오류가 나타나지 않습니다.

