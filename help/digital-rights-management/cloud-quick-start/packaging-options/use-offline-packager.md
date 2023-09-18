---
title: 포함된 Primetime 오프라인 패키지 사용
description: 포함된 Primetime 오프라인 패키지 사용
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 포함된 Primetime 오프라인 패키지 사용{#use-the-included-primetime-offline-packager}

Primetime Java Packager는 콘텐츠를 패키징하는 데 필요한 대부분의 설정이 사전 구성된 상태로 제공됩니다. 시작하려면 업데이트해야 할 영역이 몇 개 없습니다.

## 패키지 속성 업데이트 {#section_99904D35E99944A28FF43D924E516CC2}

현재 작업에 대한 컨텍스트

* 구성 파일을 사용하여 콘텐츠를 패키징하기 전에 다음 packager 속성을 업데이트합니다.

### 사용자 제공 XML 구성 파일 속성

| 속성 이름 | 설명 |
|---|---|
| `policy_file` | 정책 파일 경로. Adobe은 선택할 수 있도록 사전 구성된 여러 정책을 제공해야 합니다. |
| `pkgr_pfx` | Packager 자격 증명 경로. Adobe 발급 패키지 자격 증명( )을 제공해야 합니다. [!DNL .pfx])을 참조하십시오. |
| `pkgr_pfx_pwd` | 패키지 자격 증명 암호입니다. 여기에서 Adobe 발급 패키지 자격 증명에 대한 암호를 제공해야 합니다. |

## 명령줄을 사용한 패키지 {#section_DFBE462679E34D62963BE201FD3321F9}

콘텐츠를 패키징하기 전에 구성 파일에 필요한 정보를 모두 입력했는지 확인하십시오.

* 구성 파일로 콘텐츠를 패키지하려면 명령줄에서 다음 구문을 사용합니다.

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

컨텐츠를 HLS 또는 HDS 형식으로 패키지하는 샘플 구성 파일이 제공됩니다. [!DNL config_hds.xml] 및 [!DNL config.hls.xml].

HDS 또는 HLS 컨텐츠는 [!DNL /output] Protection Kit 디렉터리 아래에 있는 폴더입니다. 이 디렉터리에 기록된 모든 아티팩트가 재생되려면 HTTP 웹 서버에서 호스팅되어야 합니다.
