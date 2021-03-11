---
title: 명령줄 도구 구성 파일 정보
description: 명령줄 도구 구성 파일 정보
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 명령줄 도구 구성 파일 정보{#about-command-line-tools-configuration-files}

명령줄 도구는 도구를 실행하는 디렉토리에서 [!DNL flashaccesstools.properties]을 찾습니다. 그러나 명령줄 도구를 실행할 때 `-c` 옵션을 사용하여 기본 [!DNL flashaccesstools.properties]의 다른 위치를 지정할 수 있습니다. `-c`을 사용하여 다른 구성 파일을 지정할 수도 있습니다.

명령줄 도구 구성 파일은 다음 규칙이 적용되는 *Java 속성 파일* 형식을 사용합니다.

* 백슬래시를 추가 백슬래시로 이스케이프 처리합니다.

   예를 들어 Windows 컴퓨터에서 [!DNL C:\credentials.pfx] 파일을 지정하려면 [!DNL C:\\credentials.pfx] 또는 `C:/credentials.pfx`로 입력해야 합니다. Windows 네트워크 서버에서 파일을 지정하려면 `\\\\server\\folder\\filename.pfx`을 입력해야 합니다.
* *Latin-1*&#x200B;자만 포함

   비&#x200B;*Latin-1* 문자를 사용하려면 적절한 유니코드 이스케이프 시퀀스를 사용해야 합니다. 선택적으로 [!DNL native2ascii] 도구(Java에 포함)를 구성 파일 항목에 적용할 수 있습니다.
