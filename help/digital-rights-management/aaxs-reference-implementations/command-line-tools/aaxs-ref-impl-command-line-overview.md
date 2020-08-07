---
seo-title: '컨텐츠 패키징 및 취소 목록 생성을 위한 명령줄 툴 '
title: '컨텐츠 패키징 및 취소 목록 생성을 위한 명령줄 툴 '
uuid: 2c740521-2004-4320-88e1-118b84e80e31
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 컨텐츠 패키징 및 취소 목록 생성을 위한 명령줄 툴 {#command-line-tools-for-packaging-content-revocation-lists}

참조 구현에는 다음과 같은 명령줄 도구가 포함됩니다.

* 정책 관리자:정책 만들기 및 관리 도구
* 정책 업데이트 목록 관리자:정책 업데이트 목록을 만들고 보기 위한 도구
* 해지 목록 관리자:해지 목록을 만들고 보기 위한 도구
* Media Packager:암호화된 FLV 및 F4V 파일을 만드는 툴
* AIR 게시자 ID
* 유틸리티 라이센스 생성기
* 라이선스 임베드

## 요구 사항 {#requirements}

참조 구현에서 사용할 수 있는 명령줄 도구를 사용하기 위한 요구 사항은 다음과 같습니다.

* 모든 명령줄 도구는 Java 1.5 이상이 필요합니다.
* Adobe에 의해 발급되는 패키지 및 라이센스 서버 자격 증명(인증서 및 암호). 비디오 파일을 암호화 및 서명하고, 정책 업데이트 및 해지 목록에 서명하고, 라이선스를 미리 생성하려면 자격 증명이 필요합니다.

>[!NOTE]
>
>Java 버그로 인해 명령줄에서 사용되는 인수(파일 이름, 정책 이름 또는 설명 등)는 운영 체제의 기본 문자 집합의 문자만 사용해야 합니다.

## 구성 파일 {#configuration-file}

여러 명령줄 도구에는 정책 적용 및 파일 암호화에 사용할 도구에 대한 정보가 포함된 구성 파일이 필요합니다.

기본 구성 파일은 입니다 [!DNL flashaccesstools.properties]. 작업 디렉토리에 있습니다.즉, 도구를 실행하는 디렉토리입니다(명령줄 도구 설치 참조). 또한 각 도구에는 기본값을 사용하지 않으려는 경우 사용할 구성 파일을 가리킬 수 있는 옵션( `-c`)이 포함되어 있습니다.

구성 파일은 Java 속성 파일 형식을 사용합니다. 속성 값에 특수 문자가 포함되어 있으면 다음 제한 사항을 염두에 두십시오.

* 백슬래시를 추가로 사용합니다. 예를 들어 파일을 지정하려면 [!DNL C:\credentials.pfx] 또는 [!DNL C:\\credentials.pfx] 으로 지정합니다 `C:/credentials.pfx`. 네트워크 서버에서 파일을 지정하려면 을 지정합니다 `\\\\server\\folder\\filename.pfx`.
* 구성 파일은 라틴 문자 1자만 포함할 수 있습니다. 라틴 1이 아닌 문자를 사용해야 하는 경우에는 적절한 유니코드 이스케이프 시퀀스를 사용하십시오(Java와 함께 제공되는 [!DNL native2ascii] 도구 선택 사항).

도구를 실행하기 전에 구성 파일의 속성 값을 설정합니다. 일부 명령줄 도구의 경우 명령줄 또는 구성 파일을 통해 일부 옵션에 대한 값을 설정할 수 있습니다. 이러한 경우 명령줄을 통해 설정된 값이 구성 파일의 모든 값보다 우선합니다.

## 명령줄 도구 설치  {#installing-the-command-line-tools}

DVD의 [!DNL \Reference Implementation\Command Line Tools] 디렉토리에서 필요한 파일을 복사할 수 있습니다. 이 디렉토리에는 기본 [!DNL flashaccesstools.properties] [!DNL libs] 구성 파일이 포함되어 있고 도구용 JAR 파일이 들어 있습니다.

이 디렉토리에는 Adobe 액세스 SDK API의 사용을 시연하는 여러 샘플 Java 소스 파일이 포함되어 있습니다. [!DNL samples] 샘플을 만들고 실행하려면 Ant 스크립트를 [!DNL build-samples.xml] 사용하십시오.