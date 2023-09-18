---
title: 서버 속성 파일에 대한 암호 준비
description: 서버 속성 파일에 대한 암호 준비
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 서버 속성 파일에 대한 암호 준비 {#preparing-passwords-for-the-server-properties-files}

자격 증명 암호에 대한 보안을 유지하기 위해 암호를 입력하기 전에 암호화할 수 있는 도구가 제공됩니다 [!DNL flashaccess-refimpl.properties] 또는 [!DNL flashaccess-refimpl-packager.properties] 파일.

제공된 ANT 스크립트를 사용하여 도구를 실행하려면 다음을 수행하십시오.

* 다음으로 이동 *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 다음을 확인합니다. `sdkdir` 의 속성 [!DNL build-refimpl.xml] 는 Adobe 액세스 SDK가 포함된 디렉토리를 가리킵니다
* ANT를 사용하여 다음 명령을 실행합니다.

  ```
      ant -f build-refimpl.xml
  ```

* 메시지가 표시되면 자격 증명의 암호를 입력합니다

Java를 사용하여 도구를 실행하려면:

* 다음으로 이동 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 명령 프롬프트에서 다음 명령을 입력합니다.

* Windows:

  ```
  java -classpath path_to_adobe-flashaccess-sdk.jar;.  
  com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

* Linux의 경우:

  ```
      java -classpath path_to_adobe-flashaccess-sdk.jar;.  
      com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

유틸리티는 암호화된 암호를 출력하며, 이 암호는 .properties 파일에 복사해야 합니다.

>[!NOTE]
>
>참조 구현과 함께 제공된 암호 스크램블링 유틸리티를 사용하여 인코딩된 암호는 Adobe Access Server for Protected Streaming에서 작동하지 않습니다.
