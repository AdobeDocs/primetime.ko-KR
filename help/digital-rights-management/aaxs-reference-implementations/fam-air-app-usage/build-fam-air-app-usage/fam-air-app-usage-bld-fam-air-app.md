---
title: Flash Access 관리자 AIR 애플리케이션 구축
description: Flash Access 관리자 AIR 애플리케이션 구축
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Flash Access 관리자 AIR 애플리케이션 구축 {#building-the-flash-access-manager-air-application}

소스 코드에서 Flash Access 관리자 AIR 파일을 작성하려면 컴퓨터에 Flex 및 AIR SDK가 설치되어 있어야 합니다. 응용 프로그램을 패키지하고 실행하려면 먼저 MXML 코드를 SWF 파일로 컴파일해야 합니다 [!DNL amxmlc] 컴파일러입니다. 다음 [!DNL amxmlc] 컴파일러는에서 찾을 수 있습니다. [!DNL bin] Flex 4 이상 SDK의 디렉터리입니다. 원하는 경우 명령줄에서 유틸리티를 더 쉽게 실행할 수 있도록 Flex SDK bin 디렉토리를 포함하도록 경로 환경 변수를 설정할 수 있습니다.

Flash Access 관리자 AIR 파일을 작성하려면 다음 절차를 따르십시오.

1. 명령 셸 또는 터미널을 열고 Flash Access 관리자 AIR 응용 프로그램의 프로젝트 폴더( [!DNL UI Tools\Flash Access Manager] 참조 구현 디렉토리)에서 참조할 수 있습니다.
1. 다음 명령을 입력합니다.

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   실행 중 [!DNL amxmlc] 생성 [!DNL FlashAccessManager.swf]: 응용 프로그램의 컴파일된 코드가 들어 있습니다.

Adobe AIR SDK에는 AIR 애플리케이션을 패키징하고 인증서를 생성하는 AIR 개발자 도구(ADT) 유틸리티가 포함되어 있습니다. AIR 응용 프로그램은 디지털 서명되어야 합니다. 제대로 서명되지 않았거나 전혀 서명되지 않은 응용 프로그램을 설치할 때 사용자에게 경고가 표시됩니다. 명령줄을 사용하여 인증서를 생성하려면 AIR 애플리케이션과 동일한 폴더에서 콘솔 창을 열고 다음을 입력합니다.

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

대체 *some_password* 원하는 암호로. 몇 초 후에 ADT는 인증서 생성 프로세스를 완료해야 하며 사용자에게 새 인증서가 있어야 합니다 [!DNL testCert.pfx] 응용 프로그램 디렉터리에 있는 파일입니다.

그런 다음 ADT를 사용하여 애플리케이션을 [!DNL .air] 다음 명령을 사용하여 파일을 생성합니다.

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

이 명령은 의 키 파일을 사용하여 응용 프로그램을 패키지하도록 ADT에 지시합니다. [!DNL testCert.pfx]. 위의 행에서 ADT를 구성하여 전체 애플리케이션을 이라는 파일로 패키징합니다 [!DNL FlashAccessManager.air]및 를 입력하여 파일을 포함합니다. [!DNL FlashAccessManager-app.xml] 및 [!DNL FlashAccessManager.swf] 및 에셋 디렉토리의 이미지를 포함합니다.

이 프로세스의 일부로 새 인증서 파일에 대해 설정한 암호를 묻는 메시지가 표시됩니다. 입력한 다음 잠시 기다린 후 [!DNL FlashAccessManager.air] 파일은 프로젝트 파일과 동일한 디렉터리에 있어야 합니다.
