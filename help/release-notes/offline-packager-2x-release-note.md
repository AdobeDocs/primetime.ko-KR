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

---


# Primetime Offline Packager 릴리스 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능

## Primetime Offline Packager 2.3.1(2016년 10월)의 새로운 기능 {#what-s-new-in-primetime-offline-packager-oct}

이 릴리스에서는 MPEG-DASH용 온디맨드 프로파일을 사용할 수 있고 PlaylistCreator 도구에 대한 `validate` 옵션을 추가할 수 있으며 아래에 나열된 다중 DRM 시나리오에 대한 주요 수정 사항이 거의 없습니다.

| **발행물 번호** | **설명** |
|---|---|
| PTPUB 파섹 | HLS AAXS 및 Sample-AES가 패키저에서 생성된 키에 대해 작동하지 않습니다. |
| PTPUB 파섹 | 일부 특정 무선 컨텐츠에 대한 암호화 알고리즘의 오류가 수정되었습니다. |
| PTPUB 파섹 | 특정 플레이어에서 특정 미디어 유형에 대한 CENC 암호화 - Android TVSDK. |
| PTPUB 파섹 | Sample-AES 암호화는 기본적으로 AAXS DRM을 건너뜁니다. 원격 키 게재를 활성화한 상태에서 오류가 발생했습니다. |
| PTPUB 파섹 | Windows에서 key_file_path를 지정하지 않은 경우 오프라인 패키저에서 예외가 발생하지 않습니다. NPE가 대신 표시됩니다. |

Primetime Packager에 대한 최신 문서는 https://help.adobe.com/en_US/primetime/api/packagers/index.html에서 확인할 수 [있습니다](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### 버전 2.3.1의 알려진 문제 {#known-issue-in-version}

이 릴리스에는 다음과 같은 문제가 있습니다.

| **발행물 번호** | **설명** |
|---|---|
| PTPUB 파섹 | PlaylistCreator는 AAXS DRM에 대해 생성된 최종 세트 수준 .mpd 파일에서 .pssh 파일에 대한 올바른 URL을 제공하지 않습니다. |
| PTPUB 파섹 | PlaylistCreator는 in_path 매개 변수를 통해 빈 경로가 제공되면 오류를 발생시켜야 합니다. |
| PTPUB 파섹 | DASH의 경우, Offline Packager는 매개 변수 `log_vi` &amp;가 `iv_out_path` 지정된 경우 생성된 IV를 디스크에 쓰지 않습니다. |
| PTPUB 파섹 | 구성 파일을 패키징에 사용할 때 매개 변수를 사용하면 제공된 입력에서 따옴표가 제거되지 `key_url` 않습니다. |

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

1. Oracle 사이트에서 Java SE 소프트웨어를 [다운로드하고](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따릅니다.
1. 디스크에 명명된 Adobe Primetime Offline Packager 2.3.1 아카이브 파일을 `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 추출합니다.

### Offline Packager 2.3.1 구성 {#configuring-the-offline-packager}

구성 지침은 Primetime Offline Packager 시작 안내서(https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)을 [참조하십시오.](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1(2015년 7월)의 새로운 기능 {#what-s-new-in-primetime-offline-packager-july}

PlayReady BuyDRM(DASH용) 지원 자세한 내용은 여기에서 [사용 가능한 도움말 문서를 참조하십시오](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

오프라인 패키저에도 다음과 같은 향상된 기능이 추가되었습니다.

PTPUB 파섹

## Primetime Offline Packager 2.0(2015년 6월)의 새로운 기능 {#what-s-new-in-primetime-offline-packager-june}

DASH 출력 지우기 지원이 추가되었습니다. 자세한 내용은 [여기에서](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 제품 설명서를 참조하십시오.

이 릴리스에서도 다음 문제가 해결되었습니다.

* 이제 PTPUB 파섹-783 OffLINE PackAGER에서 빈 WebVTT 파섹 파일을 처리할 수 있습니다.
* PTPUB 파섹 781 특정 트랜스코딩된 MP4 에셋이 오프라인 패키징과 함께 패키징되어 MBR 출력을 생성하는 경우 Chrome에서 HLS의 가공물이 출력됩니다.

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

### Offline Packager 2.1 설치 {#installing-offline-packager}

1. Oracle 사이트에서 Java SE 소프트웨어를 [다운로드하고](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따릅니다.
1. 디스크를 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`추출합니다.

### Offline Packager 2.1 구성 {#configuring-the-offline-packager-1}

https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html에서 제공하는 구성 세부 사항은 Primetime Offline Packager 시작 문서를 [참조하십시오.](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 유용한 리소스 {#helpful-resources}

* Adobe Primetime 학습 및 지원 [페이지에서 전체 도움말 문서를](https://helpx.adobe.com/support/primetime.html) 참조하십시오.