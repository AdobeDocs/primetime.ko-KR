---
description: 'null'
seo-description: 'null'
seo-title: 명령줄 도구 구성 파일 정보
title: 명령줄 도구 구성 파일 정보
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# 명령줄 도구 구성 파일 정보{#about-command-line-tools-configuration-files}

명령줄 도구는 도구를 실행하는 [!DNL flashaccesstools.properties] 디렉토리에서 찾습니다. 그러나 명령줄 도구를 실행할 때 이 `-c` 옵션을 사용하여 기본 위치에 다른 위치를 지정할 수 [!DNL flashaccesstools.properties]있습니다. 를 `-c` 사용하여 다른 구성 파일을 지정할 수도 있습니다.

명령줄 도구 구성 파일은 다음 규칙이 적용되는 *Java 속성 파일* 형식을 사용합니다.

* 백슬래시를 추가로 사용합니다.

   예를 들어 Windows 시스템에서 [!DNL C:\credentials.pfx] 파일을 지정하려면 [!DNL C:\\credentials.pfx] 또는 `C:/credentials.pfx`으로 입력해야 합니다. Windows 네트워크 서버에서 파일을 지정하려면 `\\\\server\\folder\\filename.pfx`
* 라틴 *1* 문자만 포함

   라틴&#x200B;*1* 문자가 아닌 문자를 사용하려면 적절한 유니코드 이스케이프 시퀀스를 사용해야 합니다. 선택적으로 구성 파일 항목에 도구(Java에 포함)를 적용할 수 있습니다. [!DNL native2ascii]
