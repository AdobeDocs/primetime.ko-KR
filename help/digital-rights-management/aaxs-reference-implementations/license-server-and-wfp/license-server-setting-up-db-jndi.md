---
title: 데이터베이스 설정 및 JNDI 데이터 소스 구성
description: 데이터베이스 설정 및 JNDI 데이터 소스 구성
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# 데이터베이스 설정 및 JNDI 데이터 소스 {#setting-up-the-database-and-configuring-the-jndi-datasource} 구성

참조 구현 라이선스 서버에는 다음 기능을 지원하는 데이터베이스가 필요합니다.

* 사용자 인증
* 사용 모델 데모 비즈니스 규칙
* 메타데이터 변환
* 도메인 지원

익명 라이센스 획득은 데이터베이스를 실행할 필요가 없습니다.

>[!NOTE]
>
>이 섹션의 지침은 Microsoft Windows 플랫폼용입니다. 다른 운영 체제의 경우 운영 체제에 대한 설명서를 참조하거나 MySQL 설명서를 참조하십시오.

라이센스 서버를 실행하려면 MySQL 5.1.34 설치 및 구성해야 합니다.

1. MySQL 설치 관리자를 실행합니다(DVD의 세 번째 Party\MySQL\Installer\5.1 폴더에 있음).
1. 설치 절차가 끝난 후 **[!UICONTROL Configure MySQL Server Now]**&#x200B;을 선택하여 구성 마법사를 시작합니다. 5번째 화면에서 **[!UICONTROL Online Transaction Processing (OLTP)]** 또는 **[!UICONTROL Manual Setting]**&#x200B;을 선택하고 허용되는 최대 연결 수를 입력해야 한다는 점을 제외하고 기본 설정을 사용하거나 테스트 목적으로 특정 설정을 선택하십시오.

1. 루트 암호를 적어 둡니다.
1. MySQL을 다시 설치해야 하는 경우 다음 단계에 따라 나중에 서버를 시작할 때 문제가 발생하지 않도록 합니다.

   * *시스템 드라이브:* [!DNL \Documents and Settings\All Users\Application Data\MySQL] 폴더를 삭제합니다.

   * 이전 MySQL 설치 폴더를 삭제합니다.예: *시스템 드라이브:* [!DNL \Program Files\MySQL\MySQL Server 5.1].

다음으로 MySQL JDBC 드라이버 5.1.7을 설치해야 합니다. 이렇게 하려면 [!DNL mysql-connector-java-5.1.7-bin.jar](DVD의 [!DNL Third Party\MySQL\Installer\5.1] 폴더에 있음)을 Tomcat Server lib 디렉토리로 복사합니다.[!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC 드라이버 5.1.7은 Tomcat 6.0에서 작동합니다. 이전 버전의 Tomcat은 지원되지 않습니다.

데이터베이스 스키마를 설정하고 데이터베이스를 샘플 데이터로 채워 샘플 데이터베이스를 설정합니다. 이렇게 하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**&#x200B;로 이동합니다.
1. 암호를 입력한 후 다음 SQL 스크립트를 실행하여 웹 응용 프로그램을 통한 연결을 설정하기 위해 사용자 계정 `dbuser`을(를) 추가하고 데이터베이스 스키마를 만듭니다(&quot;;&quot;이 없습니다.). Enter 키를 누르기만 하면 됩니다.)

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 테이블의 샘플 데이터를 채우는 스크립트를 편집하여 테스트 목적으로 데이터를 포함합니다.[!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. 이 스크립트를 실행하여 2단계에서 수행한 대로 데이터를 채웁니다.

>[!NOTE]
>
>[!DNL CreateSampleDB.sql] 스크립트를 처음 실행하면 다음 오류가 표시됩니다.

*오류 1396(HY000):&#39;dbuser&#39;@&#39;localhost&#39; 쿼리 OK에 대한 작업 DROP USER가 실패했습니다. 영향을 받은 행 0개(0.00초).*

이 오류를 무시해도 됩니다. 이 스크립트는 이 스크립트를 처음 실행할 때만 발생합니다.

이때 DBCP(데이터베이스 연결 풀링)를 구성해야 합니다. DBCP는 Jakarta-Commons 데이터베이스 연결 풀을 사용합니다. 이 응용 프로그램 서버 연결 풀링을 활용하도록 JNDI Datasource TestDB가 구성됩니다. localhost에 없는 MySQL 서버를 가리키도록 데이터베이스 연결을 변경하려면 [!DNL flashaccess.war]에 있는 [!DNL META-INF\context.xml] 파일(라이센스 서버의 데이터베이스의 위치, 사용자 이름 및 암호를 지정)을 수정하거나 [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml]를 수정하고 업데이트된 파일을 사용하여 WAR 파일을 다시 작성합니다. 이러한 매개 변수를 변경하려면 WebContent 디렉토리에 있는 [!DNL context.xml]을 편집하고 Ant 스크립트를 사용하여 WAR 파일을 다시 만듭니다. 데이터베이스를 조정하려면 이 파일에서 JNDI 데이터 소스 설정을 변경합니다.

Eclipse 내에서 참조 구현 프로젝트를 디버깅하는 경우 실행/디버그 구성에 `$CATALINA_HOME\lib\tomcat-dbcp.jar`을(를) 추가해야 합니다. 독립 실행형 Tomcat 6.0 서버에서 [!DNL flashaccess.war] 파일을 실행하는 경우에는 이 단계가 필요하지 않습니다.
