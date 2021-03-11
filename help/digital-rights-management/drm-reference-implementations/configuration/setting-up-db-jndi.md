---
title: 라이센스 서버 데이터베이스 설정
description: 라이센스 서버 데이터베이스 설정
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 라이선스 서버 데이터베이스 설정{#set-up-the-license-server-database}

참조 구현 라이선스 서버에서는 다음을 지원할 데이터베이스가 필요합니다.

* 사용자 인증
* 사용 모델 데모 비즈니스 규칙
* 메타데이터 변환
* 도메인 지원

익명 라이센스 획득은 데이터베이스를 실행할 필요가 없습니다.

>[!NOTE]
>
>이 절차는 Microsoft Windows에만 적용됩니다. 다른 운영 체제의 경우 운영 체제에 대한 설명서를 참조하거나 MySQL 설명서를 참조하십시오.

라이센스 서버를 실행하려면 MySQL을 설치하고 구성해야 합니다.

1. DVD에서 [!DNL Third Party\MySQL\Installer\5.1] 폴더로 이동하여 설치 프로그램을 시작합니다.
1. MySQL 설치를 완료합니다.
1. **[!UICONTROL Configure MySQL Server Now]**&#x200B;을 선택하여 구성 마법사를 시작합니다.
1. 다섯 번째 화면에 이르기까지 기본 설정을 사용하거나 테스트의 특정 설정을 선택합니다.
1. 다섯 번째 화면에서 **[!UICONTROL Online Transaction Processing (OLTP)]** 또는 **[!UICONTROL Manual Setting]**&#x200B;을 선택하고 허용되는 최대 연결 수를 입력합니다.
1. 루트 암호를 입력합니다.
1. MySQL을 다시 설치하려면 나중에 서버를 시작해야 하는 경우 다음 단계를 수행하십시오.
   1. *시스템 드라이브:* 폴더를 삭제합니다.

      이 폴더는 [!DNL \Documents and Settings\All Users\Application Data\MySQL]에 있습니다.
   1. 이전 MySQL 설치 폴더를 삭제합니다.

      예를 들어 *시스템 드라이브:*&#x200B;는 [!DNL \Program Files\MySQL\MySQL Server 5.1]에 있습니다.
1. MySQL JDBC 드라이버 5.1.7을 설치하려면 DVD의 [!DNL Third Party\MySQL\Installer\5.1] 폴더에 있는 [!DNL mysql-connector-java-5.1.7-bin.jar] 파일을 Tomcat Server의 [!DNL ...\Tomcat6.0\lib] 디렉토리로 복사합니다.

   >[!NOTE]
   >
   >MySQL JDBC 드라이버 5.1.7은 Tomcat 6.0에서 작동합니다. 이전 버전의 Tomcat은 더 이상 지원되지 않습니다.

