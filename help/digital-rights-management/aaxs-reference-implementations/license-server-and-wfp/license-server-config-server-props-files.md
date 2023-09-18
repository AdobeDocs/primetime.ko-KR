---
title: 서버 속성 파일
description: 서버 속성 파일
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# 서버 속성 파일 {#server-properties-files}

서버에는 두 개의 구성 파일이 필요합니다. 하나는 라이센스 서버용이고 다른 하나는 패키지 장치용입니다. 두 파일 모두 클래스 경로에 배치해야 합니다. 속성 파일에는 Adobe에서 발급한 자격 증명의 위치가 포함됩니다. 이러한 자격 증명은 .pfx 파일 및 암호로 지정하거나 HSM에 저장된 자격 증명에 대한 별칭 및 암호를 제공하여 지정할 수 있습니다.

각 매개 변수의 특정 값 및 사용에 대한 자세한 내용은 속성 파일을 참조하십시오. 샘플 속성 파일은 참조 구현의 &quot;resources&quot; 디렉터리에 있습니다(참조 구현\서버\resources).

자격 증명의 암호 보안을 위해 flashaccess-refimpl.properties 또는 flashaccess-refimpl-packager.properties 파일에 암호를 입력하기 전에 암호화할 수 있는 도구(ScrambleUtil.class)가 제공됩니다.

자격 증명의 암호를 올바르게 준비하려면 다음을 수행하십시오.

1. 다음으로 이동 [!DNL Reference Implementation\Server\refimpl\scrambler].
1. 명령 프롬프트에서 다음 명령을 입력합니다.

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>앞의 예제에서는 세미콜론(;)을 구분 기호로 사용합니다. Microsoft Windows 이외의 플랫폼의 경우 구분 기호로 콜론(:)을 사용합니다.

유틸리티는 암호화된 암호를 출력하며 이 암호는 [!DNL .properties] 파일.
