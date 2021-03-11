---
description: '환경을 반영하도록 서버 속성을 구성해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다. '
title: 서버 환경에 속성 적용
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 서버 환경에 속성 적용{#apply-properties-to-server-environments}

환경을 반영하도록 서버 속성을 구성해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

* [!DNL flashaccess-i15n.properties] - 각 파일에 포함된  [!DNL .war] 샘플

* [!DNL AdobeInitial.properties] - DVD의  [!DNL /shared] 폴더에 있는 샘플

   이 파일을 사용하여 다음과 같이 WAR 파일에 설정된 속성을 재정의할 수 있습니다.

   1. [!DNL AdobeInitial.properties]에서 재정의 속성 값을 설정합니다.
   1. 클래스 경로에 [!DNL AdobeInitial.properties]을(를) 배치합니다.

   >[!NOTE]
   >
   >[!DNL AdobeInitial.properties] 파일을 사용하는 것이 좋습니다. 이렇게 하면 [!DNL flashaccess-i15n.properties] 파일에서 수행한 이전 속성 구성 설정의 손실을 무릅쓰고 응용 프로그램 WAR 파일을 업데이트할 수 있습니다.

* Java System 속성 메커니즘입니다.

다음과 같은 특정 서버 환경에 개별 속성을 적용할 수 있습니다.

* *개발*
* *스테이징*
* *프로덕션*

이 기능을 사용하면 모든 서버 환경에 동일한 WAR 파일을 사용할 수 있습니다. 특정 환경에 속성을 적용하려면 속성 *name*&#x200B;에 다음 환경 코드 중 하나를 더한 두 개의 밑줄 문자(&#39; `__`&#39;)를 추가합니다.

    * &#39;DEV&#39;
    * &#39;STAGE&#39;
    * &#39;PROD&#39;

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

예를 들어, 프로덕션 및 스테이징 서버에 대해 로그 수준을 `INFO`, 개발 서버에 대해 `DEBUG`로 설정하려면 다음을 수행합니다.

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

서버는 속성에 대해 다음 검색 순서를 사용합니다.

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` Java 시스템 등록 정보
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` Java 시스템 등록 정보

>[!NOTE]
>
>서버를 시작할 때 서버의 환경 이름을 Java System 속성으로 지정해야 합니다. 예를 들어 [!DNL catalina.bat]으로 Tomcat를 시작할 때 `CATALINA_OPTS` 환경 변수를 다음과 같이 설정합니다.
>-DENVIRONMENT_NAME=[ DEV | STAGE | PROD ]
