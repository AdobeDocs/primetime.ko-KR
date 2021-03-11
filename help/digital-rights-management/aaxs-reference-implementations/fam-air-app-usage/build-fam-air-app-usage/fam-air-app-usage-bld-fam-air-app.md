---
title: Flash Access 관리자 AIR 응용 프로그램 만들기
description: Flash Access 관리자 AIR 응용 프로그램 만들기
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Flash Access 관리자 AIR 응용 프로그램 만들기 {#building-the-flash-access-manager-air-application}

소스 코드에서 Flash Access Manager AIR 파일을 빌드하려면 컴퓨터에 Flex 및 AIR SDK가 설치되어 있어야 합니다. 응용 프로그램을 패키지하여 실행하려면 먼저 [!DNL amxmlc] 컴파일러를 사용하여 MXML 코드를 SWF 파일에 컴파일해야 합니다. [!DNL amxmlc] 컴파일러는 Flex 4 이상 SDK의 [!DNL bin] 디렉토리에 있습니다. 원하는 경우 명령줄에서 유틸리티를 쉽게 실행하려면 경로 환경 변수를 Flex SDK bin 디렉토리를 포함하도록 설정할 수 있습니다.

Flash Access 관리자 AIR 파일을 빌드하려면 다음 절차를 따르십시오.

1. 명령 셸 또는 터미널을 열고 Flash Access Manager AIR 응용 프로그램의 프로젝트 폴더( 참조 구현 디렉토리의 [!DNL UI Tools\Flash Access Manager])로 이동합니다.
1. 다음 명령을 입력합니다.

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   [!DNL amxmlc]을(를) 실행하면 응용 프로그램의 컴파일된 코드가 포함된 [!DNL FlashAccessManager.swf]이 생성됩니다.

Adobe AIR SDK에는 AIR 애플리케이션을 패키지하고 인증서를 생성하는 ADT(AIR Developer Tool) 유틸리티가 포함되어 있습니다. AIR 애플리케이션은 디지털 방식으로 서명해야 합니다.제대로 서명되지 않았거나 전혀 서명되지 않은 응용 프로그램을 설치하면 사용자에게 경고가 표시됩니다. 명령줄을 사용하여 인증서를 생성하려면 AIR 응용 프로그램과 동일한 폴더의 콘솔 창을 열고 다음을 입력합니다.

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

*some_password*&#x200B;을 원하는 암호로 대체합니다. 몇 초 후 ADT는 인증서 생성 프로세스를 완료해야 하며 응용 프로그램 디렉토리에 새 [!DNL testCert.pfx] 파일이 있어야 합니다.

그런 다음 ADT를 사용하여 다음 명령을 사용하여 응용 프로그램을 [!DNL .air] 파일로 패키지합니다.

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

이 명령은 ADT에 [!DNL testCert.pfx]의 키 파일을 사용하여 응용 프로그램을 패키징하도록 지시합니다. 위 줄에서 전체 응용 프로그램을 [!DNL FlashAccessManager.air] 파일로 패키지하고 [!DNL FlashAccessManager-app.xml] 및 [!DNL FlashAccessManager.swf] 파일과 에셋 디렉토리의 이미지를 포함하도록 ADT를 구성합니다.

이 프로세스의 일부로 새 인증서 파일에 대해 설정한 암호를 입력하라는 메시지가 표시됩니다. 입력한 후 잠시 기다린 다음 프로젝트 파일과 동일한 디렉토리에 [!DNL FlashAccessManager.air] 파일이 나타납니다.
