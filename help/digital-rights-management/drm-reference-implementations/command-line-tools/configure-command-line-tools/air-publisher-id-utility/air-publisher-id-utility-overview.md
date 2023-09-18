---
title: 개요
description: 개요
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR 게시자 ID 유틸리티 {#air-publisher-id-utility}

AIR 파일을 작성하면 AIR 개발자 도구(ADT)가 자동으로 게시자 ID를 생성합니다. AIR 게시자 ID 유틸리티( [!DNL AdobePublisherIDUtility.jar])에서 AIR 애플리케이션에 대한 게시자 ID를 계산합니다.

게시자 ID는 AIR 파일을 작성하는 데 사용하는 인증서에 대해 고유합니다. 여러 AIR 애플리케이션에 대해 동일한 인증서를 재사용하는 경우 모든 AIR 애플리케이션의 게시자 ID가 동일합니다. 릴리스 1.5.2에 성공한 AIR 릴리스에서는 생성된 게시자 ID가 파일에 추가되지 않습니다. 따라서 AIR 애플리케이션 허용 목록을 사용하려는 경우 이 도구를 사용하여 게시자 ID를 결정하십시오.

>[!NOTE]
>
>AIR 허용 목록 적용에 사용되는 게시자 ID가 애플리케이션 게시자가 애플리케이션의 [!DNL application.xml] 파일.

## AIR Publisher ID 유틸리티 명령줄 사용 {#air-publisher-id-utility-command-line-usage}

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` AIR 응용 프로그램의 경로를 지정합니다. [!DNL signatures.xml] 파일, 애플리케이션에 위치 [!DNL META-INF] 디렉터리

* `signingcert` AIR 애플리케이션 서명에 사용되는 인증서를 지정합니다

>[!NOTE]
>
>Android 애플리케이션의 게시자 ID를 확인하려면 `-s` Android 애플리케이션 패키지(APK) 서명에 사용되는 인증서를 지정하는 옵션입니다. Primetime DRM은 Primetime DRM 보호 콘텐츠를 재생할 수 있는 Android 애플리케이션을 빌드하는 데 필요합니다.
