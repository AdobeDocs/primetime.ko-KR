---
title: 데이터베이스 설정 및 JNDI 데이터 소스 구성
description: 데이터베이스 설정 및 JNDI 데이터 소스 구성
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 데이터베이스 설정 및 JNDI 데이터 소스 구성 {#setting-up-the-database-and-configuring-the-jndi-datasource}

참조 구현 라이선스 서버에는 다음 기능을 지원하는 데이터베이스가 필요합니다.

* 사용자 인증
* 사용 모델 데모 비즈니스 규칙
* 메타데이터 전환
* 도메인 지원

익명 라이선스 획득에서는 데이터베이스를 실행할 필요가 없습니다.

>[!NOTE]
>
>이 섹션의 지침은 Microsoft Windows 플랫폼을 위한 것입니다. 다른 운영 체제의 경우 해당 운영 체제에 대한 설명서 또는 MySQL 설명서를 참조하십시오.

라이선스 서버를 실행하려면 MySQL 5.1.34를 설치하고 구성해야 합니다.

1. DVD의 세 번째 Party\MySQL\Installer\5.1 폴더에 있는 MySQL 설치 관리자를 실행합니다.
1. 설치 절차가 끝나면 다음을 확인합니다. **[!UICONTROL Configure MySQL Server Now]** 구성 마법사를 시작합니다. 기본 설정을 사용하거나 테스트 목적으로 특정 설정을 선택합니다. 단, 5번째 화면에서는 선택해야 합니다. **[!UICONTROL Online Transaction Processing (OLTP)]** 또는 **[!UICONTROL Manual Setting]** 허용되는 최대 연결 수를 입력합니다.

1. 루트 암호를 기록합니다.
1. MySQL을 다시 설치해야 하는 경우 다음 단계에 따라 이후에 서버를 시작할 때 문제가 발생하지 않도록 하십시오.

   * 폴더 삭제 *시스템 드라이브:* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * 이전 MySQL 설치 폴더를 삭제합니다. 예: *시스템 드라이브:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

그런 다음 MySQL JDBC Driver 5.1.7을 설치해야 합니다. 이렇게 하려면 다음을 복사하십시오. [!DNL mysql-connector-java-5.1.7-bin.jar] (다음에서 찾음: [!DNL Third Party\MySQL\Installer\5.1] DVD의 폴더를 Tomcat Server 라이브러리 디렉터리로 복사합니다. [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC 드라이버 5.1.7은 Tomcat 6.0에서 작동합니다. 이전 버전의 Tomcat은 지원되지 않습니다.

데이터베이스 스키마를 설정하고 샘플 데이터로 데이터베이스를 채워 샘플 데이터베이스를 설정합니다. 이렇게 하려면 다음 단계를 수행하십시오.

1. 다음으로 이동  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. 암호를 입력한 후 다음 SQL 스크립트를 실행하여 사용자 계정을 추가합니다 `dbuser` 웹 애플리케이션을 통해 연결을 설정하고 데이터베이스 스키마를 만듭니다(끝에 &quot;;&quot;가 없는지 확인). Enter 키를 누릅니다.):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 테스트 목적으로 데이터를 포함하도록 테이블의 샘플 데이터를 채우는 스크립트를 편집합니다. [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. 이 스크립트를 실행하여 2단계에서와 같이 데이터를 채웁니다.

>[!NOTE]
>
>를 처음 실행할 때 [!DNL CreateSampleDB.sql] 스크립트에 다음 오류가 표시됩니다.

*오류 1396(HY000): &#39;dbuser&#39;@&#39;localhost&#39; 쿼리 확인에 대한 사용자 삭제 작업이 실패했습니다. 영향을 받는 행이 0개(0.00초)입니다.*

이 오류는 무시해도 됩니다. 이 작업은 이 스크립트를 처음 실행할 때만 수행됩니다.

이 시점에서 DBCP(데이터베이스 연결 풀링)를 구성해야 합니다. DBCP는 Jakarta-Commons 데이터베이스 연결 풀을 사용합니다. JNDI 데이터 소스 TestDB가 이 응용 프로그램 서버 연결 풀링을 활용하도록 구성되어 있습니다. localhost에 없는 MySQL 서버를 가리키도록 데이터베이스 연결을 변경하려면 [!DNL META-INF\context.xml] 다음 위치에 있는 파일(라이센스 서버 데이터베이스의 위치, 사용자 이름 및 암호 지정) [!DNL flashaccess.war], 또는 수정 [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 그리고 업데이트된 파일을 사용하여 WAR 파일을 다시 생성합니다. 이러한 매개 변수를 변경하려면 [!DNL context.xml] WebContent 디렉터리에 있으며 Ant 스크립트를 사용하여 WAR 파일을 다시 만듭니다. 데이터베이스를 조정하려면 이 파일에서 JNDI 데이터 소스 설정을 변경합니다.

Eclipse 내에서 참조 구현 프로젝트를 디버깅하는 경우 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 을 클릭하여 실행/디버그 구성에 추가합니다. 다음을 실행하는 경우에는 이 단계가 필요하지 않습니다. [!DNL flashaccess.war] 독립 실행형 Tomcat 6.0 서버에 있는 파일입니다.
