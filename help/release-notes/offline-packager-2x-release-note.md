---
title: Primetime Offline Packager 2.x 릴리스
description: Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Primetime Offline Packager 릴리스 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1 및 2.3.1 릴리스의 새로운 기능

## Primetime Offline Packager 2.3.1(2016년 10월)의 새로운 기능  {#what-s-new-in-primetime-offline-packager-oct}

이 릴리스를 통해 MPEG-DASH용 온디맨드 프로필 이 활성화되고 `validate` PlaylistCreator 도구 옵션이며, 아래에 나열된 다중 DRM 시나리오에 대한 키 수정 사항이 거의 없습니다.

| **문제 번호** | **설명** |
|---|---|
| PTPUB-985 | HLS AAXS 및 Sample-AES는 packager 생성 키에 대해 작동하지 않습니다 |
| PTPUB-973 | 일부 특정 Widevine 콘텐츠에 대한 암호화 알고리즘 오류를 수정했습니다. |
| PTPUB-964 | 특정 플레이어의 특정 미디어 유형에 대해 끊어진 CENC 암호화 - Android TVSDK. |
| PTPUB-954 | Sample-AES 암호화는 기본적으로 원격 키 전달이 활성화된 상태에서 발생하는 AAXS DRM을 우회합니다. |
| PTPUB-951 | key_file_path가 Widevine에 지정되지 않은 경우 Offline packager에서 예외가 발생하지 않습니다. 대신 NPE를 사용합니다. |

Primetime Packagers의 최신 설명서는 다음 위치에서 확인할 수 있습니다. [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### 버전 2.3.1의 알려진 문제 {#known-issue-in-version}

이 릴리스에는 다음과 같은 문제가 있습니다.

| **문제 번호** | **설명** |
|---|---|
| PTPUB- | PlaylistCreator는 AAXS DRM에 대해 생성된 최종 설정 수준 .mpd 파일의 .pssh 파일에 올바른 URL을 제공하지 않습니다. |
| PTPUB- | in_path 매개 변수를 통해 빈 경로를 제공하면 PlaylistCreator에서 오류가 발생합니다. |
| PTPUB-990 | DASH의 경우 Offline Packager는 매개 변수가 있는 경우 디스크에 packager 생성 IV를 쓰지 않습니다. `log_vi` 및 `iv_out_path` 을(를) 지정합니다. |
| PTPUB-980 | 구성 파일을 패키지화하는 데 사용하는 경우 매개 변수를 사용합니다. `key_url` 입력한 항목에서 따옴표를 제거하지 않습니다. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### 최소 시스템 요구 사항 {#minimum-system-requirements}

지원되는 운영 체제

* Linux CentOS 6.3 64비트

하드웨어 요구 사항

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)

* 64비트 운영 체제: 4GB RAM(8GB 권장)

* 하드 디스크

(디스크-SAS): 최소 10GB(7.5K RPM)

(디스크-SSD): 400MBps 읽기/쓰기 속도

(NAS): 1GB 전용 링크

소프트웨어 요구 사항

* Oracle Java SE 1.8 이상

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. 에서 Java SE 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
1. 이름이 인 Adobe Primetime Offline Packager 2.3.1 아카이브 파일 추출 `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 디스크에 저장합니다.

### Offline Packager 2.3.1 구성 {#configuring-the-offline-packager}

구성 지침은 Primetime Offline Packager 시작 안내서의 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1(2015년 7월)의 새로운 기능 {#what-s-new-in-primetime-offline-packager-july}

PlayReady BuyDRM(DASH용)에 대한 지원 자세한 내용은 도움말 설명서를 참조하십시오. [사용 가능한 위치](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

오프라인 패키저도 다음과 같이 개선되었습니다.

PTPUB-780 EXT-X-START 태그에 대한 지원 추가됨

## Primetime Offline Packager 2.0의 새로운 기능 (2015년 6월) {#what-s-new-in-primetime-offline-packager-june}

DASH 출력 지우기 지원이 추가되었습니다. 제품 설명서 참조 [여기](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 을 참조하십시오.

다음 문제도 이 릴리스에서 해결되었습니다.

* PTPUB-783 Offline Packager는 이제 빈 WebVTT 파일을 처리할 수 있습니다.
* MBR 출력을 생성하기 위해 트랜스코딩된 특정 MP4 자산이 오프라인 패키저와 함께 패키징될 때 Chrome에서 HLS 출력의 PTPUB- 781 아티팩트.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### 최소 시스템 요구 사항 {#minimum-system-requirements-1}

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)

* 64비트 운영 체제: 4GB RAM(8GB 권장)

* 1Gb 이더넷 카드 권장 (여러 네트워크 카드 및 10Gb도 지원)

* 하드 디스크

   * (디스크-SAS): 최소 10GB(7.5K RPM)
   * (디스크-SSD): 400MBps 읽기/쓰기 속도
   * (NAS): 1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java SE 1.8 이상

### Offline Packager 2.1 설치 {#installing-offline-packager}

1. 에서 Java SE 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
1. 추출 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`을 클릭하여 디스크에 저장합니다.

### Offline Packager 2.1 구성 {#configuring-the-offline-packager-1}

여기에서 사용 가능한 구성 세부 정보는 Primetime Offline Packager 시작 문서를 참조하십시오. [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
