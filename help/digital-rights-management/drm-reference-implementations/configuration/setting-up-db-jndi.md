---
title: 라이선스 서버 데이터베이스 설정
description: 라이선스 서버 데이터베이스 설정
copied-description: true
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 라이선스 서버 데이터베이스 설정{#set-up-the-license-server-database}

참조 구현 라이선스 서버에는 다음을 지원하는 데이터베이스가 필요합니다.

* 사용자 인증
* 사용 모델 데모 비즈니스 규칙
* 메타데이터 전환
* 도메인 지원

익명 라이선스 획득에서는 데이터베이스를 실행할 필요가 없습니다.

>[!NOTE]
>
>이 절차는 Microsoft Windows에만 적용됩니다. 다른 운영 체제의 경우 해당 운영 체제에 대한 설명서 또는 MySQL 설명서를 참조하십시오.

라이선스 서버를 실행하려면 MySQL을 설치하고 구성해야 합니다.

1. DVD에서 [!DNL Third Party\MySQL\Installer\5.1] 폴더를 만들고 설치 프로그램을 시작합니다.
1. MySQL 설치를 테스트합니다.
1. 선택 **[!UICONTROL Configure MySQL Server Now]** 구성 마법사를 시작합니다.
1. 다섯 번째 화면까지 기본 설정을 사용하거나 테스트를 위한 특정 설정을 선택합니다.
1. 다섯 번째 화면에서 을 선택합니다. **[!UICONTROL Online Transaction Processing (OLTP)]** 또는 **[!UICONTROL Manual Setting]** 허용되는 최대 연결 수를 입력합니다.
1. 루트 암호를 기록하십시오.
1. MySQL을 다시 설치하려면 나중에 서버를 시작해야 하는 경우 다음 단계를 완료하십시오.
   1. 삭제 *시스템 드라이브:* 폴더를 삭제합니다.

      이 폴더는에 있습니다. [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. 이전 MySQL 설치 폴더를 삭제합니다.

      예를 들어, *시스템 드라이브:*, 위치 [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. MySQL JDBC 드라이버 5.1.7을 설치하려면 다음을 복사합니다. [!DNL mysql-connector-java-5.1.7-bin.jar] 파일 위치: [!DNL Third Party\MySQL\Installer\5.1] DVD의 폴더를 [!DNL ...\Tomcat6.0\lib] Tomcat 서버의 디렉토리입니다.

   >[!NOTE]
   >
   >MySQL JDBC 드라이버 5.1.7은 Tomcat 6.0에서 작동합니다. 이전 버전의 Tomcat은 더 이상 지원되지 않습니다.
