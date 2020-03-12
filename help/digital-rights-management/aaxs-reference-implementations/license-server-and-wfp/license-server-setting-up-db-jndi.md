---
seo-title: 데이터베이스 설정 및 JNDI 데이터 소스 구성
title: 데이터베이스 설정 및 JNDI 데이터 소스 구성
uuid: 1326523f-c053-4169-a934-1b2d3907b1f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 데이터베이스 설정 및 JNDI 데이터 소스 구성 {#setting-up-the-database-and-configuring-the-jndi-datasource}

참조 구현 라이센스 서버에는 다음과 같은 기능을 지원하는 데이터베이스가 필요합니다.

* 사용자 인증
* 사용 모델 데모 비즈니스 규칙
* 메타데이터 변환
* 도메인 지원

익명 라이센스 획득은 데이터베이스를 실행할 필요가 없습니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>이 섹션의 지침은 Microsoft Windows 플랫폼용입니다. 다른 운영 체제의 경우 운영 체제에 대한 설명서를 참조하거나 MySQL 설명서를 참조하십시오.

라이센스 서버를 실행하려면 MySQL 5.1.34를 설치하고 구성해야 합니다.

1. MySQL 설치 프로그램을 실행합니다(DVD의 세 번째 Party\MySQL\Installer\5.1 폴더에 있음).
1. 설치 절차가 끝날 때 구성 마법사를 **[!UICONTROL Configure MySQL Server Now]** 시작하려면 을 선택합니다. 5번째 화면에서 허용되는 최대 연결 수를 **[!UICONTROL Online Transaction Processing (OLTP)]** 선택하거나 **[!UICONTROL Manual Setting]** 입력해야 한다는 점을 제외하고 기본 설정을 사용하거나 테스트 목적으로 특정 설정을 선택하십시오.

1. 루트 암호를 기록합니다.
1. MySQL을 다시 설치해야 하는 경우 다음 단계에 따라 이후에 서버를 시작할 때 문제가 발생하지 않도록 하십시오.

   * 폴더 *시스템 드라이브를 삭제합니다.*[!DNL \Documents and Settings\All Users\Application Data\MySQL]Adobe

   * 이전 MySQL 설치 폴더를 삭제합니다.예를 들어 *시스템 드라이브:*[!DNL \Program Files\MySQL\MySQL Server 5.1]Adobe

그런 다음 MySQL JDBC 드라이버 5.1.7을 설치해야 합니다.이렇게 하려면 [!DNL mysql-connector-java-5.1.7-bin.jar] (DVD의 [!DNL Third Party\MySQL\Installer\5.1] 폴더에 있음) Tomcat Server lib 디렉토리로 복사합니다. [!DNL ...\Tomcat6.0\lib]Adobe

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>MySQL JDBC 드라이버 5.1.7은 Tomcat 6.0에서 작동합니다.이전 버전의 Tomcat은 지원되지 않습니다.

데이터베이스 스키마를 설정하고 데이터베이스를 샘플 데이터로 채워 샘플 데이터베이스를 설정합니다. 이렇게 하려면 다음 단계를 수행하십시오.

1. > **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** 으로 이동합니다.
1. 암호를 입력한 후 다음 SQL 스크립트를 실행하여 웹 응용 프로그램을 통해 연결을 설정하는 사용자 계정을 추가하고 데이터베이스 스키마를 `dbuser` 만듭니다(&quot;s;&quot;이 없는 경우 확인). Enter를 누르면 됩니다.)

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 표의 샘플 데이터를 채우는 스크립트를 편집하여 테스트용 데이터를 포함합니다. [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql]Adobe
1. 이 스크립트를 실행하여 2단계에서 수행한 대로 데이터를 채웁니다.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>처음 스크립트를 실행할 때 다음 [!DNL CreateSampleDB.sql] 오류가 표시됩니다.

*오류 1396(HY000):&#39;dbuser&#39;@&#39;localhost&#39; 쿼리 OK에 대한 작업 DROP USER가 실패했습니다. 0개의 행이 영향을 받습니다(0.00초).*

이 오류를 무시해도 됩니다. 이는 이 스크립트를 처음 실행할 때만 발생합니다.

이때 DBCP(데이터베이스 연결 풀링)를 구성해야 합니다. DBCP는 Jakarta-Commons 데이터베이스 연결 풀을 사용합니다. 이 응용 프로그램 서버 연결 풀링을 활용하도록 JNDI Datasource TestDB가 구성됩니다. localhost에 없는 MySQL 서버를 가리키도록 데이터베이스 연결을 변경하려면 에 있는 [!DNL META-INF\context.xml] 파일(라이센스 서버 데이터베이스의 위치, 사용자 이름 및 암호 지정)을 수정하거나 업데이트된 파일을 사용하여 WAR 파일을 수정 [!DNL flashaccess.war][!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 및 다시 만듭니다. 이러한 매개 변수를 변경하려면 WebContent 디렉토리에 [!DNL context.xml] 있는 매개 변수를 편집하고 Ant 스크립트를 사용하여 WAR 파일을 다시 만듭니다. 데이터베이스를 조정하려면 이 파일에서 JNDI 데이터 소스 설정을 변경합니다.

Eclipse 내에서 참조 구현 프로젝트를 디버깅하는 경우 실행/디버그 구성에 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 추가해야 합니다. 독립 실행형 Tomcat 6.0 서버에서 [!DNL flashaccess.war] 파일을 실행하는 경우에는 이 단계가 필요하지 않습니다.
