---
title: 참조 구현 라이선스 서버가 제대로 실행되는지 확인
description: 참조 구현 라이선스 서버가 제대로 실행되는지 확인
copied-description: true
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 참조 구현 라이선스 서버가 제대로 실행되는지 확인 {#determining-if-reference-implementation-license-server-runs-properly}

참조 구현 라이선스 서버가 올바르게 시작되었는지 여부를 확인하는 방법에는 몇 가지가 있습니다. 다음을 볼 수 있습니다. [!DNL catalina.log] 라이선스 서버가 자체 로그 파일에 기록하므로 로그가 충분하지 않을 수 있습니다. 참조 구현이 제대로 시작되었는지 확인하려면 아래 절차를 따르십시오.

* 다음을 확인: [!DNL AdobeFlashAccess.log] 파일. 여기서 참조 구현이 로그 정보를 기록합니다. 이 로그 파일의 위치는 [!DNL log4j.xml] 원하는 위치를 가리키도록 파일 및 를 수정할 수 있습니다. 기본적으로 로그 파일은 카탈리나를 실행하는 작업 디렉토리에 복사됩니다.

* 다음 URL로 이동합니다. [!DNL https:// flashaccess/license/v4]*서버:서버 포트*. &quot;License Server가 올바르게 설정되었습니다.&quot;라는 텍스트가 표시됩니다.

서버가 올바르게 실행되는지 테스트하는 또 다른 방법은 테스트 컨텐츠의 세그먼트를 패키징하고 샘플 비디오 플레이어를 설정한 다음 재생하는 것입니다.

다음 절차는 이 프로세스에 대해 설명합니다.

1. 로 이동 [!DNL \Reference Implementation\Command Line Tools] 폴더를 삭제합니다.

   다음을 참조하십시오 [명령줄 도구 설치](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) 명령줄 도구를 설치하는 방법에 대해 설명합니다.

1. 다음 명령을 입력하여 간단한 익명 DRM 정책을 생성합니다.

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   다음을 참조하십시오 [명령줄 사용](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) DRM 정책 관리자를 사용하여 DRM 정책을 생성하는 방법에 대해 설명합니다.

1. 설정 `encrypt.license.serverurl` 의 속성 [!DNL flashaccesstools.properties] 라이센스 서버의 URL에 대한 파일입니다.

   예를 들어, [!DNL https:// localhost:8080/]. 다음 [!DNL flashaccesstools.properties] 파일은에 있습니다. [!DNL \Reference Implementation\Command Line Tools] 폴더를 삭제합니다.

1. 다음 명령을 입력하여 컨텐츠의 세그먼트를 패키징합니다.

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

1. 생성된 두 파일을 [!DNL webapps\ROOT\Content] Tomcat 서버의 폴더입니다.
1. 로 이동 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 디렉터리로 이동하고 콘텐츠를 [!DNL webapps\ROOT\SVP\] Tomcat 서버의 폴더입니다.

1. Flash Player 버전 10.1 이상을 설치합니다.
1. 웹 브라우저를 열고 다음 URL로 이동합니다. [!DNL        https:// localhost:8080/SVP/player.html]

1. 다음 URL로 이동한 다음 **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. 비디오 재생이 실패할 경우 샘플 비디오 플레이어의 로깅 창에 오류 코드가 표시되거나 가 여기에 추가되었는지 확인합니다. [!DNL AdobeFlashAccess.log] 파일.

   이제 의 위치를 검색할 수 있습니다. [!DNL AdobeFlashAccess.log] log4j.xml 파일에 파일을 기록한 다음 수정합니다. 기본적으로 로그 파일은 카탈리나를 실행하는 작업 디렉토리에 복사됩니다.
