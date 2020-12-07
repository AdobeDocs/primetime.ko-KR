---
description: 'null'
seo-description: 'null'
seo-title: 라이센스 서버 데이터베이스 구성
title: 라이센스 서버 데이터베이스 구성
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 라이선스 서버 데이터베이스 구성{#configure-the-license-server-database}

데이터베이스 스키마를 설정하고 데이터베이스를 샘플 데이터로 채워 샘플 데이터베이스를 구성하려면:

1. MySQL 명령줄을 불러옵니다.

   **Windows에서 -** 클릭   **[!UICONTROL Window's Start Menu]** >  **[!UICONTROL MySQL]** >  **[!UICONTROL MySQL Server 5.1]**   **[!UICONTROL MySQL Command Line Client]**

   **Linux 등** - Type  `MySQL`.

1. 다음 SQL 스크립트를 실행합니다.

   mysql> 소스 &quot;`"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   이 스크립트는 사용자 계정 `dbuser`을 추가하고 웹 응용 프로그램을 통해 연결을 설정하고 데이터베이스 스키마를 만듭니다.

   >[!NOTE]
   >
   >스크립트 끝에 세미콜론( `;`)이 없는지 확인합니다.

1. 테이블의 샘플 데이터를 채우는 `PopulateSampleDB.sql` 스크립트를 편집하여 테스트용 데이터를 포함합니다.

   이 스크립트는 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 폴더에 있습니다.
1. [!DNL PopulateSampleDB] 스크립트를 실행하여 2단계에서 수행한 대로 데이터를 채웁니다.

   >[!NOTE]
   >
   >[!DNL CreateSampleDB.sql] 스크립트를 처음 실행할 때 다음 오류가 발생합니다.

   이 오류를 무시해도 됩니다. 이 스크립트는 이 스크립트를 처음 실행할 때만 발생합니다.

Jakarta-Commons 데이터베이스 연결 풀을 사용하는 DBCP(데이터베이스 연결 풀링)를 구성해야 합니다. 이 응용 프로그램 서버 연결 풀링을 활용하도록 JDI Datasource TestDB가 구성됩니다. localhost에 없는 MySQL 서버를 가리키도록 데이터베이스 연결을 변경하려면 다음 파일 중 하나를 수정하십시오.

* [!DNL META-INF\context.xml] 파일로서 [!DNL flashaccess.war] 파일에 있는 라이센스 서버 데이터베이스의 위치, 사용자 이름 및 암호를 지정합니다.

* `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 파일.

업데이트된 파일을 사용하여 WAR 파일을 다시 만듭니다.

이러한 매개 변수를 변경하려면 [!DNL WebContent] 디렉토리에서 [!DNL context.xml] 파일을 편집하고 Ant 스크립트를 사용하여 WAR 파일을 다시 만듭니다. 데이터베이스를 조정하려면 이 파일에서 JNDI 데이터 소스 설정을 변경합니다.

Eclipse에서 참조 구현 프로젝트를 디버깅하는 경우 실행/디버그 구성에 `$CATALINA_HOME\lib\tomcat-dbcp.jar`을 추가합니다.

>[!NOTE]
>
>독립 실행형 Tomcat 6.0 서버에서 [!DNL flashaccess.war] 파일을 실행하는 경우 이 단계가 필요하지 않습니다.

