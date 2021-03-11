---
title: 포함된 Primetime Offline Packager 사용
description: 포함된 Primetime Offline Packager 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 포함된 Primetime Offline Packager{#use-the-included-primetime-offline-packager} 사용

Primetime Java Packager는 콘텐츠를 패키징하는 데 필요한 대부분의 설정으로 사전 구성되어 있습니다. 시작하려면 몇 개의 영역만 업데이트할 수 있습니다.

## 업데이트 패키지 속성 {#section_99904D35E99944A28FF43D924E516CC2}

현재 작업의 컨텍스트

* 구성 파일을 사용하여 컨텐츠를 패키지하기 전에 다음 패키지 속성을 업데이트하십시오.

### 사용자가 제공한 XML 구성 파일 속성

| 속성 이름 | 설명 |
|---|---|
| `policy_file` | 정책 파일 경로입니다. Adobe은 선택할 수 있도록 미리 구성된 몇 가지 정책을 제공한다. |
| `pkgr_pfx` | 패키저 자격 증명 경로. 여기에서 Adobe에서 발행한 패키지 자격 증명( [!DNL .pfx])을 제공해야 합니다. |
| `pkgr_pfx_pwd` | Packager 자격 증명 암호. 여기에서 Adobe에서 발급한 패키지 자격 증명에 암호를 제공해야 합니다. |

## 명령줄 {#section_DFBE462679E34D62963BE201FD3321F9}을(를) 사용하여 패키지

콘텐트를 패키징하기 전에 구성 파일에 제공된 모든 필수 정보가 있는지 확인하십시오.

* 구성 파일을 사용하여 컨텐츠를 패키지하려면 명령줄에 다음 구문을 사용합니다.

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

내용을 HLS 또는 HDS 형식으로 패키징하는 샘플 구성 파일이 제공됩니다(이름이 [!DNL config_hds.xml] 및 [!DNL config.hls.xml]).

HDS 또는 HLS 컨텐츠는 Protection Kit 디렉토리 아래의 [!DNL /output] 폴더로 출력됩니다. 이 디렉토리에 쓰여진 모든 가공물은 HTTP 웹 서버에서 호스팅되어야 재생됩니다.
