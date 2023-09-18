---
title: 초기 Flash Access 관리자 설정
description: 초기 Flash Access 관리자 설정
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 초기 Flash Access 관리자 설정 {#initial-flash-access-manager-setup}

Flash Access 관리자를 설정하려면 다음 절차를 따르십시오.

1. Packager 서버 배포. 이 서버는 방화벽 내의 사용자만 사용할 수 있습니다(공개 컴퓨터에 이 소프트웨어를 배포하지 마십시오). 서버 배포에 대한 자세한 내용은 [라이선스 서버 및 감시 폴더 패키지 배포](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * 복사 [!DNL flashaccess-packager.war] Tomcat의 webapps 폴더로 이동합니다.
   * 복사 [!DNL flashaccess-refimpl-packager.properties] 리소스에서 클래스 경로의 위치로 이동합니다.
   * 서버를 시작합니다. 속성 파일에 문제가 있어 몇 가지 오류가 표시됩니다. 속성이 아직 채워지지 않았기 때문에 이러한 오류가 발생할 수 있습니다.

1. 다음을 실행하여 Flash Access 관리자 AIR 애플리케이션 설치 [!DNL .air] 파일(AIR 1.5 이상 필요)
1. Flash Access 관리자 AIR 애플리케이션을 실행합니다.

   서버가 다음 이외의 위치에서 실행 중인 경우 `https://localhost:8080*`에 애플리케이션이 서버에 연결할 수 없다는 오류가 표시됩니다. 오류 대화 상자를 닫고 기본 설정 탭에 Packager 서버 URL에 대한 올바른 URL을 입력합니다. 서버가 지정된 URL에서 실행 중이고 속성 파일이 클래스 경로에 있는 경우 기본 설정 화면은 속성 파일의 값으로 채워집니다. packager 서버 URL을 설정한 후 AIR 애플리케이션은 이 설정을 기억하므로 다음에 애플리케이션을 실행할 때 이 설정을 입력할 필요가 없습니다.
1. [환경 설정] 탭의 값을 입력하고 **[!UICONTROL Save]**.
1. 감시 폴더를 사용하려면 3단계에서 확인한 오류를 복구하기 위해 서버를 다시 시작해야 합니다. 기본 설정이 올바르게 구성된 경우 시작하는 동안 오류가 나타나지 않습니다.
