---
seo-title: 서버 속성 파일에 대한 암호 준비
title: 서버 속성 파일에 대한 암호 준비
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 서버 속성 파일에 대한 암호 준비 {#preparing-passwords-for-the-server-properties-files}

자격 증명의 암호를 보안을 유지하기 위해 [!DNL flashaccess-refimpl.properties] 또는 [!DNL flashaccess-refimpl-packager.properties] 파일에 입력하기 전에 암호를 암호화하는 도구가 제공됩니다.

제공된 ANT 스크립트를 사용하여 도구를 실행하려면

* 이동 *`<Reference Implementation Server Path>`*[!DNL \refimpl]

* Adobe `sdkdir` Access SDK가 들어 있는 디렉토리 [!DNL build-refimpl.xml] 위치 확인
* ANT를 사용하여 다음 명령을 실행합니다.

   ```
       ant -f build-refimpl.xml
   ```

* 메시지가 표시되면 자격 증명의 암호를 입력합니다

Java를 사용하여 도구를 실행하려면

* 이동 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 명령 프롬프트에서 명령을 입력합니다.

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

이 유틸리티는 암호화된 암호를 출력하여 .properties 파일에 복사해야 합니다.

>[!NOTE]
>
>참조 구현과 함께 제공된 암호 스크래핑 유틸리티를 사용하여 인코딩된 암호는 보호된 스트리밍을 위한 Adobe Access Server에서 작동하지 않습니다.
