---
title: 라이선스 서버 데이터베이스 구성
description: 라이선스 서버 데이터베이스 구성
copied-description: true
exl-id: 1d5d988e-d22a-4405-8f39-1763f1f65094
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 라이선스 서버 데이터베이스 구성{#configure-the-license-server-database}

데이터베이스 스키마를 설정하고 샘플 데이터로 데이터베이스를 채워 샘플 데이터베이스를 구성하려면 다음을 수행합니다.

1. MySQL 명령줄을 표시합니다.

   **Windows에서 -** 클릭  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **Linux 등의** - 유형 `MySQL`.

1. 다음 SQL 스크립트를 실행합니다.

   mysql> 소스 &quot; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   이 스크립트는 사용자 계정을 추가합니다. `dbuser`는 웹 애플리케이션을 통해 연결을 설정하고 데이터베이스 스키마를 만듭니다.

   >[!NOTE]
   >
   >세미콜론()이 없는지 확인합니다. `;`)을 클릭하여 스크립트를 만듭니다.

1. 편집 `PopulateSampleDB.sql` 테스트용 데이터를 포함하도록 테이블의 샘플 데이터를 채우는 스크립트입니다.

   이 스크립트는에 있습니다 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 폴더를 삭제합니다.
1. 실행 [!DNL PopulateSampleDB] 2단계에서 스크립트로 데이터를 채웁니다.

   >[!NOTE]
   >
   >를 처음 실행할 때 [!DNL CreateSampleDB.sql] 스크립트 다음 오류가 발생합니다.

   이 오류는 무시해도 됩니다. 이 스크립트는 처음 실행할 때만 발생합니다.

Jakarta-Commons 데이터베이스 연결 풀을 사용하는 DBCP(데이터베이스 연결 풀링)를 구성해야 합니다. JNDI 데이터 소스 TestDB가 이 응용 프로그램 서버 연결 풀링을 활용하도록 구성되어 있습니다. localhost에 없는 MySQL 서버를 가리키도록 데이터베이스 연결을 변경하려면 다음 파일 중 하나를 수정합니다.

* 다음 [!DNL META-INF\context.xml] 파일에 있는 라이센스 서버 데이터베이스의 위치, 사용자 이름 및 암호를 지정합니다. [!DNL flashaccess.war] 파일.

* 다음 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 파일.

그리고 업데이트된 파일을 사용하여 WAR 파일을 다시 생성합니다.

이러한 매개 변수를 변경하려면 [!DNL context.xml] 파일 위치: [!DNL WebContent] 디렉터리를 만들고 Ant 스크립트를 사용하여 WAR 파일을 다시 만듭니다. 데이터베이스를 조정하려면 이 파일에서 JNDI 데이터 소스 설정을 변경합니다.

Eclipse에서 참조 구현 프로젝트를 디버깅하는 경우 다음을 추가합니다. `$CATALINA_HOME\lib\tomcat-dbcp.jar` 을 클릭하여 실행/디버그 구성에 추가합니다.

>[!NOTE]
>
>다음을 실행하는 경우 [!DNL flashaccess.war] 독립 실행형 Tomcat 6.0 서버에 있는 파일이므로 이 단계는 필요하지 않습니다.
