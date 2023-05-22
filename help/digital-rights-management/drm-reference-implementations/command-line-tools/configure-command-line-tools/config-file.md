---
title: 명령줄 도구 구성 파일 정보
description: 명령줄 도구 구성 파일 정보
copied-description: true
exl-id: 0ec4917e-7c70-4b84-86ac-c34c8a522018
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 명령줄 도구 구성 파일 정보{#about-command-line-tools-configuration-files}

명령줄 도구는 [!DNL flashaccesstools.properties] 를 입력합니다. 하지만 `-c` 명령줄 도구를 실행하여 다른 기본 위치를 지정할 때 옵션 사용 [!DNL flashaccesstools.properties]. 다음을 사용할 수도 있습니다. `-c` 다른 구성 파일을 지정합니다.

명령줄 도구 구성 파일은 *Java 속성 파일* 형식: 다음 규칙이 적용됩니다.

* 추가 백슬래시로 백슬래시를 이스케이프 처리합니다.

   예를 들어 Windows 컴퓨터에서 [!DNL C:\credentials.pfx] 파일, 다음으로 입력해야 합니다. [!DNL C:\\credentials.pfx] 또는 `C:/credentials.pfx`. Windows 네트워크 서버에 파일을 지정하려면 다음을 입력해야 합니다 `\\\\server\\folder\\filename.pfx`
* 항목만 포함 *라틴-1* 자.

   비-를 사용하려면&#x200B;*라틴-1* 문자를 사용하는 경우 적절한 유니코드 이스케이프 시퀀스를 사용해야 합니다. 다음을 선택적으로 적용할 수 있습니다. [!DNL native2ascii] 구성 파일 항목에 대한 도구(Java에 포함됨)입니다.
