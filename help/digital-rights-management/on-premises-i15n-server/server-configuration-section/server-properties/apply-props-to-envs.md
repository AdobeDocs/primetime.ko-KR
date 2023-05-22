---
description: 사용자 환경을 반영하도록 서버 속성을 구성해야 합니다. 다음을 사용하여 이 작업을 수행할 수 있습니다
title: 서버 환경에 속성 적용
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 서버 환경에 속성 적용{#apply-properties-to-server-environments}

사용자 환경을 반영하도록 서버 속성을 구성해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

* [!DNL flashaccess-i15n.properties] - 각 라이브러리에 포함된 샘플 [!DNL .war] 파일

* [!DNL AdobeInitial.properties] - 다음에 있는 샘플 [!DNL /shared] DVD의 폴더

   이 파일을 사용하여 다음과 같이 WAR 파일에 설정된 속성을 재정의할 수 있습니다.

   1. 에서 재정의 속성 값 설정 [!DNL AdobeInitial.properties]
   1. 위치 [!DNL AdobeInitial.properties] 클래스 경로에 있습니다.

   >[!NOTE]
   >
   >Adobe은 [!DNL AdobeInitial.properties] 이 옵션을 사용하면 이전에 수행한 속성 구성 설정이 손실되지 않고 애플리케이션 WAR 파일을 업데이트할 수 있으므로 [!DNL flashaccess-i15n.properties] 파일.

* Java 시스템 속성 메커니즘.

다음과 같은 특정 서버 환경에 개별 속성을 적용할 수 있습니다.

* *개발*
* *스테이징*
* *프로덕션*

이 기능을 사용하면 모든 서버 환경에 동일한 WAR 파일을 사용할 수 있습니다. 특정 환경에 속성을 적용하려면 두 개의 밑줄 문자(&#39;)를 추가합니다 `__`&#39;) 속성에 다음 환경 코드 중 하나를 추가합니다 *이름*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

예를 들어 로그 수준을 로 설정하려면 `INFO` 프로덕션 및 스테이징 서버용 및 `DEBUG` 개발 서버의 경우:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

서버는 속성에 대해 이 검색 순서를 사용합니다.

1. `propertyname_environment` 위치: [!DNL AdobeInitial.properties]

1. `propertyname_environment` 위치: [!DNL flashaccess-15n.properties]

1. `propertyname_environment` Java 시스템 속성에서
1. `propertyname` 위치: [!DNL AdobeInitial.properties]

1. `propertyname` 위치: [!DNL flashaccess-15n.properties]

1. `propertyname` Java 시스템 속성에서

>[!NOTE]
>
>서버를 시작할 때 서버의 환경 이름을 Java System 속성으로 지정해야 합니다. 예를 들어 Tomcat을 시작할 때 [!DNL catalina.bat], 를 설정합니다. `CATALINA_OPTS` 환경 변수를 다음과 같이 지정합니다.
>-DENVIRONMENT_NAME=[ 개발 | 스테이지 | PROD ]
