---
seo-title: 서버 속성 파일
title: 서버 속성 파일
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 서버 속성 파일 {#server-properties-files}

서버에는 두 개의 구성 파일이 필요합니다. 하나는 라이센스 서버용이고 다른 하나는 패키지 서버용입니다. 두 파일을 모두 클래스 경로에 배치해야 합니다. 속성 파일에는 Adobe에서 발행한 자격 증명의 위치가 포함되어 있습니다. 이러한 자격 증명은 .pfx 파일 및 암호로 지정하거나 HSM에 저장된 자격 증명의 별칭 및 암호를 제공하여 지정할 수 있습니다.

각 매개 변수의 특정 값과 사용에 대한 자세한 내용은 속성 파일을 참조하십시오. 샘플 속성 파일은 참조 구현의 &quot;resources&quot; 디렉토리(Implementation\Server\resources 참조)에서 찾을 수 있습니다.

자격 증명의 암호를 안전하게 보호하기 위해 flashaccess-refimpl.properties 또는 flashaccess-refimpl-packager.properties 파일에 입력하기 전에 암호를 암호화하는 도구(ScrambleUtil.class)가 제공됩니다.

자격 증명의 암호를 제대로 준비하려면:

1. 로 [!DNL Reference Implementation\Server\refimpl\scrambler]이동합니다.
1. 명령 프롬프트에서 명령을 입력합니다.

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

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>앞의 예에서는 세미콜론(;)을 구분 기호로 사용합니다. Microsoft Windows 이외의 플랫폼의 경우 콜론(:)을 구분 기호로 사용합니다.

이 유틸리티는 암호화된 암호를 출력하여 [!DNL .properties] 파일에 복사해야 합니다.
