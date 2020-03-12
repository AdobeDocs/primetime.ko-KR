---
seo-title: 포함된 Primetime Offline Packager 사용
title: 포함된 Primetime Offline Packager 사용
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 포함된 Primetime Offline Packager 사용{#use-the-included-primetime-offline-packager}

Primetime Java Packager는 콘텐츠를 패키징하는 데 필요한 대부분의 설정과 함께 미리 구성되어 있습니다. 시작하려면 몇 가지 영역만 업데이트할 수 있습니다.

## 패키지 속성 업데이트 {#section_99904D35E99944A28FF43D924E516CC2}

현재 작업의 컨텍스트

* 구성 파일을 사용하여 컨텐츠를 패키지하기 전에 다음 패키지 속성을 업데이트하십시오.

### 사용자가 제공한 XML 구성 파일 속성

| 속성 이름 | 설명 |
|---|---|
| `policy_file` | 정책 파일 경로. Adobe는 선택할 수 있도록 미리 구성된 몇 가지 정책을 제공합니다. |
| `pkgr_pfx` | Packager 자격 증명 경로. 여기에서 직접 Adobe에서 발급한 패키지 자격 증명( [!DNL .pfx])을 제공해야 합니다. |
| `pkgr_pfx_pwd` | Packager 자격 증명 암호. 여기에서 Adobe에서 발급한 패키지 자격 증명에 암호를 제공해야 합니다. |

## 명령줄을 사용하여 패키지 {#section_DFBE462679E34D62963BE201FD3321F9}

콘텐트를 패키지하기 전에 구성 파일에 모든 필수 정보가 제공되었는지 확인하십시오.

* 구성 파일을 사용하여 컨텐츠를 패키지하려면 명령줄에서 다음 구문을 사용합니다.

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

HLS 또는 HDS 포맷으로 컨텐츠를 패키지화할 수 있는 샘플 구성 파일이 [!DNL config_hds.xml] 및 [!DNL config.hls.xml]이름이 지정됩니다.

HDS 또는 HLS 컨텐츠는 Protection Kit 디렉토리 아래의 [!DNL /output] 폴더로 출력됩니다. 이 디렉토리에 작성된 모든 객체는 HTTP 웹 서버에서 호스팅되어야 재생됩니다.
