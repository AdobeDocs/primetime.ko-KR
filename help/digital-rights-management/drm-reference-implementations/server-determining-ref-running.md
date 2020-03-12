---
description: 'null'
seo-description: 'null'
seo-title: 참조 구현 라이센스 서버가 제대로 실행되는지 확인
title: 참조 구현 라이센스 서버가 제대로 실행되는지 확인
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 참조 구현 라이센스 서버가 제대로 실행되는지 확인 {#determining-if-reference-implementation-license-server-runs-properly}

참조 구현 라이센스 서버가 올바르게 시작되었는지 확인하는 방법에는 여러 가지가 있습니다. 라이센스 서버가 자체 로그 파일에 로그하기 때문에 로그를 볼 수 [!DNL catalina.log] 없습니다. 참조 구현이 제대로 시작되었는지 확인하려면 아래 단계를 따르십시오.

* 파일을 [!DNL AdobeFlashAccess.log] 확인합니다. 여기서 참조 구현은 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 파일에 의해 지정되며 원하는 위치를 가리키도록 수정할 수 있습니다. 기본적으로 로그 파일은 카탈로그를 실행하는 작업 디렉토리에 복사됩니다.

* 다음 URL로 이동합니다.서버: [!DNL https:// flashaccess/license/v4]*서버 포트&#x200B;*. &quot;라이센스 서버가 올바르게 설정되었습니다&quot;라는 텍스트가 표시됩니다.

서버가 제대로 실행되는지 여부를 테스트하는 또 다른 방법은 테스트 컨텐츠의 세그먼트를 패키지하고 샘플 비디오 플레이어를 설정한 다음 재생하는 것입니다.

다음 절차에서는 이 프로세스에 대해 설명합니다.

1. 폴더로 [!DNL \Reference Implementation\Command Line Tools] 이동합니다.

   명령줄 [도구 설치 방법에 대한 자세한 내용은 명령줄 도구](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) 설치를 참조하십시오.

1. 간단한 익명 DRM 정책을 만들려면 다음 명령을 입력합니다.

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   DRM [정책 관리자를 사용하여 DRM 정책을 만드는 방법에 대한 명령줄 사용을](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) 참조하십시오.

1. 파일의 `encrypt.license.serverurl` 속성을 [!DNL flashaccesstools.properties] 라이센스 서버의 URL로 설정합니다.

   예를 들면 다음과 같습니다 [!DNL https:// localhost:8080/]. 이 [!DNL flashaccesstools.properties] 파일은 [!DNL \Reference Implementation\Command Line Tools] 폴더에 있습니다.

1. 다음 명령을 입력하여 컨텐츠의 세그먼트를 패키지합니다.

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. 생성된 두 파일을 Tomcat 서버의 [!DNL webapps\ROOT\Content] 폴더에 복사합니다.
1. 디렉토리로 이동하여 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] Tomcat 서버의 [!DNL webapps\ROOT\SVP\] 폴더에 내용을 복사합니다.

1. Flash Player 버전 10.1 이상을 설치합니다.
1. 웹 브라우저를 열고 다음 URL로 이동합니다. [!DNL        https:// localhost:8080/SVP/player.html]

1. 다음 URL로 이동한 다음 **[!UICONTROL Play]**&#x200B;을 클릭합니다. [!DNL https:// localhost:8080/Content/]*`your_encrypted_FLV`* 5.

1. 비디오가 재생되지 않으면 샘플 비디오 플레이어의 로깅 창에 오류 코드가 표시되거나 [!DNL AdobeFlashAccess.log] 파일에 추가되어 있는지 확인합니다.

   이제 log4j.xml 파일에서 [!DNL AdobeFlashAccess.log] 로그 파일의 위치를 검색한 다음 수정할 수 있습니다. 기본적으로 로그 파일은 카탈로그를 실행하는 작업 디렉토리로 복사됩니다.

