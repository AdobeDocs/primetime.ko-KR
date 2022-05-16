---
description: '환경을 반영하도록 서버 속성을 구성해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다 '
title: 서버 환경에 속성 적용
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 서버 환경에 속성 적용{#apply-properties-to-server-environments}

환경을 반영하도록 서버 속성을 구성해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

* [!DNL flashaccess-i15n.properties] - 각 [!DNL .war] 파일

* [!DNL AdobeInitial.properties] - 에 있는 샘플 [!DNL /shared] DVD의 폴더

   이 파일을 사용하여 WAR 파일에 설정된 속성을 다음과 같이 재정의할 수 있습니다.

   1. 에서 재정의 속성 값을 설정합니다. [!DNL AdobeInitial.properties]
   1. 장소 [!DNL AdobeInitial.properties] 클래스 경로 아래의 제품에서 사용할 수 있습니다.

   >[!NOTE]
   >
   >Adobe은 다음을 사용할 것을 권장합니다. [!DNL AdobeInitial.properties] 파일에서 수행한 이전 속성 구성 설정을 손실하지 않고 응용 프로그램 WAR 파일을 업데이트할 수 있으므로 [!DNL flashaccess-i15n.properties] 파일.

* Java 시스템 속성 메커니즘입니다.

이러한 특정 서버 환경에 개별 속성을 적용할 수 있습니다.

* *개발*
* *스테이징*
* *프로덕션*

이 기능을 사용하면 모든 서버 환경에 동일한 WAR 파일을 사용할 수 있습니다. 특정 환경에 속성을 적용하려면 밑줄 문자(&#39; `__`&#39;)에 다음 환경 코드 중 하나를 추가하여 속성에 추가합니다 *이름*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

예를 들어, 로그 수준을 `INFO` 및 `DEBUG` 개발 서버의 경우:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

서버는 속성에 대해 이 검색 순서를 사용합니다.

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` Java 시스템 속성
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` Java 시스템 속성

>[!NOTE]
>
>서버를 시작할 때 서버의 환경 이름을 Java 시스템 속성으로 지정해야 합니다. 예를 들어 [!DNL catalina.bat], 설정 `CATALINA_OPTS` 환경 변수는 다음과 같습니다.
>-DENVIRONMENT_NAME=[ 개발 | 단계 | PROD ]
