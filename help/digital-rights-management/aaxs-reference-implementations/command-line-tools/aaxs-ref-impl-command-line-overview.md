---
title: 콘텐츠를 패키징하고 취소 목록을 만드는 명령줄 도구
description: 콘텐츠를 패키징하고 취소 목록을 만드는 명령줄 도구
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 콘텐츠를 패키징하고 취소 목록을 만드는 명령줄 도구 {#command-line-tools-for-packaging-content-revocation-lists}

참조 구현에는 다음과 같은 명령줄 도구가 포함되어 있습니다.

* 정책 관리자: 정책을 만들고 관리하기 위한 도구입니다.
* 정책 업데이트 목록 관리자: 정책 업데이트 목록을 만들고 보기 위한 도구
* 해지 목록 관리자: 해지 목록을 만들고 보기 위한 도구
* Media Packager: 암호화된 FLV 및 F4V 파일을 만드는 도구입니다.
* AIR 게시자 ID
* UtilityLicense 생성기
* License Embedder

## 요구 사항 {#requirements}

참조 구현에서 사용할 수 있는 명령줄 도구를 사용하기 위한 요구 사항은 다음과 같습니다.

* 모든 명령줄 도구에는 Java 1.5 이상이 필요합니다.
* Adobe에서 발급한 Packager 및 라이선스 서버 자격 증명(인증서 및 암호). 비디오 파일을 암호화 및 서명하고, 정책 업데이트 및 해지 목록에 서명하고, 라이선스를 미리 생성하려면 자격 증명이 필요합니다.

>[!NOTE]
>
>Java 버그로 인해 명령줄에서 사용되는 인수(예: 파일 이름, 정책 이름 또는 설명)는 운영 체제의 기본 문자 집합에 있는 문자만 사용해야 합니다.

## 구성 파일 {#configuration-file}

일부 명령줄 도구에는 정책을 적용하고 파일을 암호화하는 데 사용할 도구에 대한 정보가 포함된 구성 파일이 필요합니다.

기본 구성 파일은 입니다. [!DNL flashaccesstools.properties]. 작업 디렉터리, 즉 도구를 실행하는 디렉터리에 있습니다(명령줄 도구 설치 참조). 각 도구에는 옵션( `-c`)를 클릭하여 기본값을 사용하지 않으려는 경우 사용할 구성 파일을 지정할 수 있습니다.

구성 파일은 Java 속성 파일 형식을 사용합니다. 속성 값에 특수 문자가 포함되어 있는 경우 다음 제한 사항에 유의하십시오.

* 추가 백슬래시로 백슬래시를 이스케이프 처리합니다. 예를 들어, [!DNL C:\credentials.pfx] 파일, 다음으로 지정 [!DNL C:\\credentials.pfx] 또는 `C:/credentials.pfx`. 네트워크 서버에 파일을 지정하려면 다음을 지정합니다 `\\\\server\\folder\\filename.pfx`.
* 구성 파일에는 라틴 1자만 포함될 수 있습니다. Latin-1이 아닌 문자를 사용해야 하는 경우 적절한 유니코드 이스케이프 시퀀스를 사용하십시오(선택 사항: [!DNL native2ascii] java와 함께 제공되는 도구).

도구를 실행하기 전에 구성 파일의 속성에 대한 값을 설정하십시오. 일부 명령줄 도구의 경우 명령줄 또는 구성 파일을 통해 일부 옵션의 값을 설정할 수 있습니다. 이러한 경우 명령줄을 통해 설정된 값이 구성 파일의 모든 값보다 우선합니다.

## 명령줄 도구 설치  {#installing-the-command-line-tools}

다음에서 필요한 파일을 복사할 수 있습니다. [!DNL \Reference Implementation\Command Line Tools] DVD의 디렉터리(기본값 포함) [!DNL flashaccesstools.properties] 구성 파일 및 [!DNL libs] 디렉토리(도구에 대한 JAR 파일이 포함).

다음 [!DNL samples] 디렉터리에는 Adobe 액세스 SDK API의 사용을 보여 주는 몇 가지 샘플 Java 소스 파일이 포함되어 있습니다. 샘플을 빌드하고 실행하려면 [!DNL build-samples.xml] 개미 대본.
