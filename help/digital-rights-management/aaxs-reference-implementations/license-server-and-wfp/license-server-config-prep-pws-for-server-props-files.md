---
title: 서버 속성 파일에 대한 암호 준비
description: 서버 속성 파일에 대한 암호 준비
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 서버 속성 파일 {#preparing-passwords-for-the-server-properties-files} 암호 준비

자격 증명 암호를 안전하게 보호하기 위해 [!DNL flashaccess-refimpl.properties] 또는 [!DNL flashaccess-refimpl-packager.properties] 파일에 입력하기 전에 암호를 암호화하는 도구가 제공됩니다.

제공된 ANT 스크립트를 사용하여 도구를 실행하려면:

* *`<Reference Implementation Server Path>`* [!DNL \refimpl](으)로 이동

* [!DNL build-refimpl.xml]의 `sdkdir` 속성이 Adobe 액세스 SDK가 포함된 디렉토리를 가리키는지 확인합니다.
* ANT를 사용하여 다음 명령을 실행합니다.

   ```
       ant -f build-refimpl.xml
   ```

* 자격 증명 암호를 입력하라는 메시지가 표시되면

Java를 사용하여 도구를 실행하려면:

* *`<Reference Implementation Server Path>`*\ [!DNL scrambler](으)로 이동

* 명령 프롬프트에서 명령을 입력합니다.

* Windows의 경우:

   ```
   java -classpath path_to_adobe-flashaccess-sdk.jar;.  
   com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

* Linux의 경우:

   ```
       java -classpath path_to_adobe-flashaccess-sdk.jar;.  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

이 유틸리티는 암호화된 암호를 출력하여 .properties 파일에 복사해야 합니다.

>[!NOTE]
>
>참조 구현과 함께 제공된 암호 뒤틀기 유틸리티를 사용하여 인코딩된 암호는 안전한 스트리밍을 위한 Adobe Access Server에서 작동하지 않습니다.
