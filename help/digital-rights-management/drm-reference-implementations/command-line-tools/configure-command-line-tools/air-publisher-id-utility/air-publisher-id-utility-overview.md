---
title: 개요
description: 개요
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR Publisher ID 유틸리티 {#air-publisher-id-utility}

AIR 파일을 만들면 AIR 개발자 도구(ADT)가 자동으로 게시자 ID를 생성합니다. AIR 게시자 ID 유틸리티( [!DNL AdobePublisherIDUtility.jar])은 AIR 애플리케이션의 게시자 ID를 계산합니다.

게시자 ID는 AIR 파일을 만드는 데 사용하는 인증서에 고유합니다. 여러 AIR 애플리케이션에 대해 동일한 인증서를 재사용하는 경우 모든 AIR 애플리케이션의 게시자 ID는 동일합니다. 릴리스 1.5.2를 성공하는 AIR 릴리스에서는 생성된 게시자 ID를 파일에 추가하지 않습니다. 따라서 AIR 애플리케이션 허용 목록을 사용할 계획이라면 이 도구를 사용하여 게시자 ID를 결정합니다.

>[!NOTE]
>
>AIR 허용 목록 실행에 사용되는 게시자 ID는 애플리케이션 게시자가 애플리케이션의 [!DNL application.xml] 파일.

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

* `signaturefile` AIR 응용 프로그램의 경로를 지정합니다. [!DNL signatures.xml] 응용 프로그램에 있는 파일 [!DNL META-INF] directory

* `signingcert` AIR 응용 프로그램에 서명하는 데 사용되는 인증서를 지정합니다

>[!NOTE]
>
>Android 애플리케이션의 게시자 ID를 확인하려면 `-s` APK(Android 애플리케이션 패키지)에 서명하는 데 사용되는 인증서를 지정하는 옵션입니다. Primetime DRM은 Primetime DRM으로 보호된 콘텐츠를 재생할 수 있는 Android 애플리케이션을 빌드하려면 필요합니다.
