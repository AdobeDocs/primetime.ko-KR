---
title: 참조 구현 라이선스 서버가 제대로 실행되고 있는지 확인
description: 참조 구현 라이선스 서버가 제대로 실행되고 있는지 확인
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 참조 구현 라이선스 서버가 제대로 실행되고 있는지 확인 {#determining-if-reference-implementation-license-server-is-running-properly}

서버가 올바르게 시작되었는지 확인하는 방법에는 몇 가지가 있습니다. 보기 [!DNL catalina.log] 라이선스 서버가 자체 로그 파일에 기록하므로 로그가 충분하지 않을 수 있습니다. 참조 구현이 제대로 시작되었는지 확인하려면 아래 절차를 따르십시오.

* 다음을 확인: [!DNL AdobeFlashAccess.log] 파일. 여기서 참조 구현이 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 원하는 위치를 가리키도록 파일 및 를 수정할 수 있습니다. 기본적으로 로그 파일은 카탈리나를 실행한 작업 디렉토리로 출력됩니다.

* 다음 URL로 이동합니다. `https:///flashaccess/license/v4<your server:server port>`. &quot;License Server가 올바르게 설정되었습니다.&quot;라는 텍스트가 표시됩니다.

서버가 올바르게 실행 중인지 테스트하는 또 다른 방법은 테스트 콘텐츠를 패키징하고 샘플 비디오 플레이어를 설정한 다음 재생하는 것입니다. 다음 절차는 이 프로세스에 대해 설명합니다.

1. 다음 위치로 이동 [!DNL \Reference Implementation\Command Line Tools] 폴더를 삭제합니다. 명령줄 도구 설치에 대한 자세한 내용은 [명령줄 도구 설치](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. 다음 명령을 사용하여 간단한 익명 정책을 만듭니다.

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   정책 관리자를 사용하여 정책을 만드는 방법에 대한 자세한 내용은 다음을 참조하십시오. [명령줄 사용](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. 설정 `encrypt.license.serverurl` 의 속성 [!DNL flashaccesstools.properties] 라이센스 서버의 URL에 대한 파일입니다(예: `https:// localhost:8080/`). 다음 [!DNL flashaccesstools.properties] 파일은 아래에 있습니다. [!DNL \Reference Implementation\Command Line Tools] 폴더를 삭제합니다.

1. 다음 명령을 사용하여 콘텐츠를 패키징합니다.

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

1. Tomcat에 생성된 2개의 파일 복사 [!DNL webapps\ROOT\Content] 폴더를 삭제합니다.
1. 다음으로 이동 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` Tomcat에 내용 복사 `webapps\ROOT\SVP\` 폴더를 삭제합니다.
1. Flash Player 10.1 이상을 설치합니다.
1. 웹 브라우저를 열고 다음 URL로 이동합니다.

   `https:// localhost:8080/SVP/player.html`
1. 다음 URL로 이동한 다음 재생 버튼을 클릭합니다.

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 비디오가 재생되지 않으면 샘플 비디오 플레이어의 로깅 창 또는 `AdobeFlashAccess.log` 파일. 의 위치 `AdobeFlashAccess.log` 로그 파일은 log4j.xml 파일로 표시되며 원하는 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 카탈리나를 실행한 작업 디렉터리에 기록됩니다.
