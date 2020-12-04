---
title: Primetime Offline Packager 2.x 릴리스
seo-title: Primetime Offline Packager 2.x 릴리스
description: Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능
seo-description: Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---


# Primetime Offline Packager 릴리스 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능

## Primetime Offline Packager 2.3.1(2016년 10월) {#what-s-new-in-primetime-offline-packager-oct}의 새로운 기능

이번 릴리스는 MPEG-DASH용 온디맨드 프로파일을 활성화하고, PlaylistCreator 도구에 대한 `validate` 옵션에 대한 지원을 추가하며, 아래에 나열된 멀티 DRM 시나리오에 대한 주요 수정 사항은 거의 없습니다.

| **발행물 번호** | **설명** |
|---|---|
| PTPUB-985 | HLS AAXS 및 Sample-AES가 패키저에서 생성된 키에는 작동하지 않습니다. |
| PTPUB-973 | 일부 특정 무선 컨텐츠에 대한 암호화 알고리즘의 오류가 수정되었습니다. |
| PTPUB-964 | 특정 플레이어(Android TVSDK)에서 특정 미디어 유형에 대해 CENC 암호화가 손상되었습니다. |
| PTPUB-954 | 샘플 AES 암호화는 기본적으로 AAXS DRM을 건너뜁니다. 원격 키 게시가 활성화된 경우 오류가 발생했습니다. |
| PTPUB-951 | Windows에서 key_file_path를 지정하지 않은 경우 오프라인 패키저는 예외를 throw하지 않습니다. 대신 NPE를 던집니다. |

Primetime Packager의 최신 문서는 [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html)에서 확인할 수 있습니다.

### 버전 2.3.1 {#known-issue-in-version}에서 알려진 문제

이 릴리스에는 다음과 같은 문제가 있습니다.

| **발행물 번호** | **설명** |
|---|---|
| PTPUB-1005 | PlaylistCreator는 AAXS DRM에 대해 생성된 최종 세트 수준 .mpd 파일에서 .pssh 파일에 대한 올바른 URL을 제공하지 않습니다. |
| PTPUB-1001 | PlaylistCreator는 in_path 매개 변수를 통해 빈 경로를 제공하는 경우 오류를 발생시켜야 합니다. |
| PTPUB-990 | DASH의 경우 `log_vi` 및 `iv_out_path` 매개 변수가 지정된 경우 Offline Packager는 생성된 IV를 디스크에 쓰지 않습니다. |
| PTPUB-980 | 구성 파일을 패키징에 사용하는 경우 매개 변수 `key_url`을(를) 사용하면 제공된 입력에서 따옴표가 제거되지 않습니다. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### 최소 시스템 요구 사항 {#minimum-system-requirements}

지원되는 운영 체제

* Linux CentOS 6.3 64비트

하드웨어 요구 사항

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)

* 64비트 운영 체제:4GB RAM(8GB 권장)

* 하드 디스크

(Disk-SAS):최소 10GB(7.5K RPM 포함)

(디스크-SSD):400MBps 읽기/쓰기 속도

(NAS):1GB 전용 링크

소프트웨어 요구 사항

* Oracle Java SE 1.8 이상

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java SE 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
1. `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip`이라는 이름의 Adobe Primetime Offline Packager 2.3.1 아카이브 파일을 디스크에 추출합니다.

### Offline Packager 2.3.1 구성 {#configuring-the-offline-packager}

구성 지침은 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)의 Primetime Offline Packager 시작하기 안내서에서 확인할 수 있습니다.

## Primetime Offline Packager 2.1(2015년 7월) {#what-s-new-in-primetime-offline-packager-july}의 새로운 기능

PlayReady BuyDRM(DASH용) 지원 자세한 내용은 도움말 문서 [에서 사용 가능한 ](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)를 참조하십시오.

오프라인 패키저에도 다음과 같은 향상된 기능이 추가되었습니다.

PTPUB-780 EXT-X-START 태그에 대한 지원 추가

## Primetime Offline Packager 2.0(2015년 6월) {#what-s-new-in-primetime-offline-packager-june}의 새로운 기능

지우기 DASH 출력 지원이 추가되었습니다. 자세한 내용은 제품 설명서 [여기](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)를 참조하십시오.

이 릴리스에서도 다음 문제가 해결되었습니다.

* 이제 PTPUB-783 Offline Packager에서 빈 WebVTT 파일을 처리할 수 있습니다.
* PTPUB- 781 트랜스코딩된 특정 MP4 에셋이 오프라인 패키지로 패키징되어 MBR 출력을 생성하는 경우 크롬의 HLS 출력 시 가공물이 출력됩니다.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### 최소 시스템 요구 사항 {#minimum-system-requirements-1}

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)

* 64비트 운영 체제:4GB RAM(8GB 권장)

* 1Gb 이더넷 카드 권장(다중 네트워크 카드 및 10Gb 지원)

* 하드 디스크

   * (Disk-SAS):최소 10GB(7.5K RPM 포함)
   * (디스크-SSD):400MBps 읽기/쓰기 속도
   * (NAS):1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java SE 1.8 이상

### Offline Packager 2.1 {#installing-offline-packager} 설치

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java SE 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
1. `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`을(를) 디스크에 추출합니다.

### Offline Packager 2.1 {#configuring-the-offline-packager-1} 구성

[https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)에서 제공되는 구성 세부 사항은 Primetime Offline Packager 시작 문서를 참조하십시오.

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 문서를 참조하십시오.