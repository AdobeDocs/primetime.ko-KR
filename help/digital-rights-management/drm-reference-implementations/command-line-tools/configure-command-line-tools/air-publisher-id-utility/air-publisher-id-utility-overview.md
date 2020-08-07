---
seo-title: 개요
title: 개요
uuid: f45c6b58-53c5-41e0-be3d-590231dd214a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# AIR 게시자 ID 유틸리티 {#air-publisher-id-utility}

AIR 파일을 빌드하면 ADT(AIR Developer Tool)가 자동으로 Publisher ID를 생성합니다. AIR 게시자 ID 유틸리티( [!DNL AdobePublisherIDUtility.jar])는 AIR 응용 프로그램의 게시자 ID를 계산합니다.

게시자 ID는 AIR 파일을 작성하는 데 사용하는 인증서에 고유합니다. 여러 AIR 응용 프로그램에 대해 동일한 인증서를 재사용하는 경우 모든 AIR 응용 프로그램의 Publisher ID가 동일합니다. 릴리스 1.5.2가 성공하면 생성된 게시자 ID가 파일에 추가되지 않습니다. 따라서 AIR 응용 프로그램 허용 목록을 사용하려는 경우 이 도구를 사용하여 게시자 ID를 결정합니다.

>[!NOTE]
>
>AIR 허용 목록 실행에 사용되는 게시자 ID는 응용 프로그램 게시자가 응용 프로그램의 [!DNL application.xml] 파일에서 지정하는 게시자 ID와 다릅니다.

## AIR 게시자 ID 유틸리티 명령줄 사용 {#air-publisher-id-utility-command-line-usage}

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

* 
   * `signaturefile`* 응용 프로그램 디렉토리에 있는 AIR 응용 프로그램 [!DNL signatures.xml] 파일의 경로를 [!DNL META-INF] 지정합니다.

* `signingcert` AIR 응용 프로그램 서명에 사용되는 인증서를 지정합니다.

>[!NOTE]
>
>Android 응용 프로그램의 게시자 ID를 결정하려면 `-s` 옵션을 사용하여 APK(Android 응용 프로그램 패키지)에 서명하는 데 사용되는 인증서를 지정해야 합니다. Primetime DRM은 Primetime DRM으로 보호된 콘텐츠를 재생할 수 있는 Android 애플리케이션을 구축하는 데 필요합니다.