---
title: 참조 구현 라이센스 서버가 제대로 실행되고 있는지 확인
description: 참조 구현 라이센스 서버가 제대로 실행되고 있는지 확인
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 참조 구현 라이선스 서버가 올바르게 실행되고 있는지 확인 중 {#determining-if-reference-implementation-license-server-is-running-properly}

서버가 올바르게 시작되었는지 확인하는 방법에는 여러 가지가 있습니다. 라이센스 서버가 자체 로그 파일에 기록되므로 [!DNL catalina.log] 로그를 보는 것으로는 충분하지 않을 수 있습니다. 참조 구현이 제대로 시작되었는지 확인하려면 아래 절차를 따르십시오.

* [!DNL AdobeFlashAccess.log] 파일을 확인합니다. 여기서 참조 구현은 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 파일로 표시되며 원하는 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 카탈로그를 실행한 작업 디렉토리로 출력됩니다.

* 다음 URL로 이동합니다.`https:///flashaccess/license/v4<your server:server port>`. &quot;라이센스 서버가 올바르게 설정됨&quot;이라는 텍스트가 표시됩니다.

서버가 올바르게 실행되고 있는지 여부를 테스트하는 또 다른 방법은 테스트 컨텐츠를 패키지하여 샘플 비디오 플레이어를 설정한 다음 재생하는 것입니다. 다음 절차에서는 이 프로세스에 대해 설명합니다.

1. [!DNL \Reference Implementation\Command Line Tools] 폴더로 이동합니다. 명령줄 도구 설치에 대한 자세한 내용은 [명령줄 도구 설치](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools)를 참조하십시오.

1. 다음 명령을 사용하여 간단한 익명 정책을 만듭니다.

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   정책 관리자를 사용하여 정책을 만드는 방법에 대한 자세한 내용은 [명령줄 사용](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md)을 참조하십시오.

1. [!DNL flashaccesstools.properties] 파일의 `encrypt.license.serverurl` 속성을 라이센스 서버의 URL로 설정합니다(예: `https:// localhost:8080/`). [!DNL flashaccesstools.properties] 파일은 [!DNL \Reference Implementation\Command Line Tools] 폴더 아래에 있습니다.

1. 다음 명령을 사용하여 컨텐츠를 패키지합니다.

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. 생성된 2개의 파일을 Tomcat [!DNL webapps\ROOT\Content] 폴더에 복사합니다.
1. `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release`으로 이동하여 `webapps\ROOT\SVP\` 폴더에 콘텐트를 복사합니다.
1. Flash Player 10.1 이상을 설치합니다.
1. 웹 브라우저를 열고 다음 URL로 이동합니다.

   `https:// localhost:8080/SVP/player.html`
1. 다음 URL로 이동한 다음 [재생] 단추를 클릭합니다.

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 비디오가 재생되지 않으면 샘플 비디오 플레이어의 로깅 창이나 `AdobeFlashAccess.log` 파일에서 오류 코드가 기록되었는지 확인합니다. `AdobeFlashAccess.log` 로그 파일의 위치는 log4j.xml 파일로 표시되며 원하는 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 카탈로그를 실행한 작업 디렉토리에 기록됩니다.
