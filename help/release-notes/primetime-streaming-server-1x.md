---
title: Primetime 스트리밍 서버 릴리스
description: Primetime Streaming Server 1.3 및 1.4 릴리스의 새로운 기능
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Primetime 스트리밍 서버 출시 {#primetime-streaming-server-x-releases}

Primetime Streaming Server 1.3 및 1.4 릴리스의 새로운 기능

## Primetime 스트리밍 서버 1.4(12월 릴리스)의 새로운 기능 {#what-s-new-in-primetime-streaming-server-december-release}

**오프라인 패키저**

* 이제 출력 HLS 스트림에 MPEG-2 TS에 있는 ID3 메타데이터가 포함됩니다.
* 이제 HLS 오디오 전용 스트림에 연결된 정적 이미지가 있을 수 있습니다.
* HLS AES 암호화 워크플로우에 대한 사용자 입력으로 IV 제공 지원
* 오프라인 패키저에서 IV를 생성할 때 파일에 IV 출력 지원
* Playlist Creator는 이제 다중 언어 오디오 그룹 및 다중 언어 WebVTT 자막 그룹을 미디어 스트림에 연결하는 것을 지원합니다

**원본 서버**

* HLS AES 암호화는 실시간 및 VOD 워크플로우에서 사용할 수 있습니다. Primetime Origin을 사용하면 들어오는 HLS 스트림 또는 MP4 파일에 HLS AES 암호화를 적용할 수 있습니다.
* 또한 들어오는 HDS 스트림을 HLS 스트림으로 변환하는 데 JIT HLS AES 암호화를 적용할 수 있습니다.
* 이제 Primetime Origin에서 PHLS 스트림에 대한 SWF 목록을 지원합니다. 이전에는 PHDS 스트림에서만 지원되었습니다.

**Primetime Live Packager**

* 입력 RTMP 및 MPEG-2 TS 스트림을 위한 HLS AES-128 스트림 생성 지원

PHDS/PHLS 인증서가 새로 고쳐졌습니다. 동일한 내용의 새 만료 날짜는 10/01/2016.

### **릴리스 1.4에 포함된 버그 수정** {#bug-fixes-included-in-release}

* PTPUB-282- OfflinePackager 1.3.1에서 만든 HLS 세트 수준 매니페스트에 코덱과 해상도 정보가 없습니다.
* PTPUB-353 - PlayListCreator는 설정된 수준 매니페스트에서 WebVTT 정보 추가를 지원하지 않습니다.
* PTPUB-583 - PlaylistCreator 도구가 예기치 않게 그룹 URI를 프리펜드합니다.
* PTPUB-605 Playlist Creator가 각 변형 스트림에 SUBTITLE 그룹을 나열하지 않음
* PTPUB-634 -Offline Packager가 매니페스트에 SpliceInsert를 추가합니다.
* PTPUB-635- 단일 광고 큐에 대해 삽입된 여러 SpliceOut 태그입니다.

### 릴리스 1.4 {#known-issue-in-release}의 알려진 문제

* PTPUB- 645 DKPIimple 모드는 명령줄 큐와 인스트림 큐가 모두 오프라인 패키저 구성에 제공될 때 DKPIcte35 모드가 모두 지정된 경우에도 강제 실행됩니다

## Primetime 스트리밍 서버 1.3.1(5월 릴리스)의 새로운 기능 {#what-s-new-in-primetime-streaming-server-may-release}

버전 1.3.1은 핫픽스를 참조합니다. JIT MP4 사용 사례의 주요 성능 향상 기능으로 구성되므로 다음 개선 사항을 고객에게 권장하는 업그레이드입니다.

1. 키 회전을 포함한 DRM을 사용하는 원본 기반의 MP4 JIT m3u8 생성 성능 수정
1. JIT 매니페스트 요청에서 MP4 JIT 변환을 위한 생성된 조각 URI로 쿼리 매개 변수를 복사하는 &#39;CopyQueryParamToJITFragmentURIs&#39; 구성을 추가했습니다. 샘플 사용에 대해서는 HTTP Origin Server 설명서를 참조하십시오
1. vod.xml에 구성/MP4만 구성을 통해 JIT 변환 확장 없이 MP4 파일 허용

### 릴리스 1.3.1 {#bug-fixes-included-in-release-1}에 포함된 버그 수정

* 3759167 - 패키징하는 동안 타임스탬프 예외 사항으로 인해 일부 SCTE35 신호에 의해 출력 매니페스트에 도달하지 않습니다. SCTE35 메시지의 SpliceInfoSection의 TimeSignal에서 SpliceTime에 pts_adjustment를 적용합니다.

### 릴리스 1.3.1 {#known-issues-in-release}의 알려진 문제

* 3717039 - 패키지 프로그램이 DPI 단순 모드 큐를 생성하도록 구성된 경우 스플라이스 삽입 또는 배치 기회와 같은 특정 신호 유형을 찾고 이러한 신호 유형만 간단한 모드 큐로 변환하는 것이 중요합니다. 프로그램 시작, 네트워크 시작 등과 같은 다른 유형의 신호들은 무시해야 합니다.

* 3718598 - HSM 액세스를 통해 보호된 컨텐츠를 제공하도록 Origin Server가 구성된 경우 백엔드 LunaSA 클라이언트는 HSM 모듈과 자주 통신합니다.

## Primetime 스트리밍 서버 1.3(4월 릴리스)의 새로운 기능 {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3 릴리스에서는 스트리밍 콘텐츠, 향상된 사용성 및 보안과 관련된 새로운 기능이 추가되었습니다.

**Adobe Primetime Streaming Server - 통합된 라이브 패키지 및 원본 서버 양식 제공**

Primetime Live Packager와 Primetime Origin을 함께 사용하면 하나의 구성 요소로 작업할 수 있습니다. 이 구성 요소는 Packager 또는 Origin으로 사용하거나 결합된 기능을 사용하여 라이브 스트림을 패키지하고 호스팅할 수 있습니다.

이러한 서버에 통합된 파일 인터페이스를 제공하므로 단일 시스템에서 손쉽게 실행할 수 있습니다. 별도의 패키저 또는 오리진으로 구성된 유연성을 지속적으로 제공합니다.

**베타 MPEG-DASH 지원**

Primetime 스트리밍 서버는 실시간 및 VOD 워크플로우를 위한 MPEG-DASH 패키징을 지원합니다. 라이브 패키지 구성 요소는 인제스트 RTMP 또는 MPEG-2-TS 스트림을 DASH 형식으로 변환합니다. 원본 구성 요소는 DASH 스트림을 허용합니다.

VOD 워크플로우의 경우, 오프라인 패키지 구성 요소는 MP4 및 TS 에셋을 MPEG-DASH ISOFF 형식으로 변환합니다.

**실시간 VOD 변환**

실시간 스트림 캡처 및 VOD 재생을 위한 보관을 지원하는 새로운 구성 요소 레코딩 서버를 사용할 수 있습니다. 또한 전체 이벤트 재생 및 이벤트의 일부 클립/강조 표시 생성을 지원합니다. 라이브 컨텐츠에서 오디오 전용 스트림 기록, 광고 또는 슬레이트를 제거하도록 구성할 수 있습니다. Recording Server는 Primetime Streaming Server 및 제3자 Origin과 연동됩니다.

**Primetime Live Packager의 RTMP에서 HLS로 변환**

Primetime Live Packager 구성 요소는 RTMP 스트림에서 HLS 스트림 생성을 지원합니다. 또한 Primetime DRM 및 보호된 스트리밍을 출력 HLS 스트림에 추가할 수 있습니다.

**Primetime Live Packager로 들어오는 RTMP 스트림을 위한 인증**

Primetime Live Packager로 RTMP 스트림을 보낼 때 Primetime Live Packager와 함께 신뢰할 수 있는 자격 증명으로 액세스를 구성할 수 있습니다.

이제 Live Packager로 스트림을 전송하는 동안 사용자 이름/암호를 사용하도록 인코딩을 구성할 수 있습니다.

**PlaylistCreator 도구를 사용하여 HDS 및 HLS용 최상위 매니페스트 만들기**

이제 Primetime Offline Packager와 함께 유용한 유틸리티인 PlaylistCreator.jar를 사용하여 HDS 및 HLS 에셋에 대한 최상위 매니페스트 파일을 손쉽게 생성할 수 있습니다.

**하드웨어 보안 모듈을 통합하는 추가 보안 기능**

Primetime Offline Packager는 이제 하드웨어 보안 모듈에서 Packager 자격 증명 인증서 및 일반 키에 액세스할 수 있도록 지원합니다.

하드웨어 보안 모듈은 이러한 기밀 자산에 대한 추가 보호 기능을 제공합니다.

**향상된 VOD 패키징 성능**

Primetime Offline Packager의 메자닌 에셋 패키징 시간을 개선하기 위해 몇 가지 성능 개선 사항이 포함되었습니다.

**JIT MP4 패키징 성능 향상**

대규모 VOD 에셋 라이브러리에 대한 사용자 요청을 처리하기 위해 Primetime Origin의 JIT 패키징 기능에 몇 가지 향상된 성능이 포함되어 있습니다.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### 최소 시스템 요구 사항 {#minimum-system-requirements}

**네트워크 요구 사항**

* 인코더에서 Live Packager로 MPEG-TS 스트림을 전송하려면 네트워크에서 멀티캐스트가 활성화되어 있어야 합니다. 또한 Live Packager는 멀티캐스트 네트워크가 필요 없는 인코더에서 RTMP 스트림을 허용합니다.

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제:4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장(다중 네트워크 카드 및 10Gb 지원)
* 디스크:

   * (Disk-SAS):최소 10GB(7.5K RPM 포함)
   * (디스크-SSD):400MBps 읽기/쓰기
   * (NAS) :1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java JRE 1.7(권장:Sun/Oracle 핫스팟 JVM). JMX API에 대한 JConsole 액세스에 JDK가 필요합니다.

### Primetime 스트리밍 서버 {#install-and-configure-primetime-streaming-server} 설치 및 구성

**스트리밍 서버 설치**

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java SE 및 JDK 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
2. Adobe Primetime-Streaming Server 1.4 아카이브 파일 `Primetime- StreamingServer-1-4-0-b206-12042014.zip`을 디스크에 추출합니다.

**Primetime 스트리밍 서버 시작**

스트리밍 서버를 시작하려면 스트리밍 서버의 루트 디렉토리에 있는 명령줄에서 다음 명령을 실행합니다.\
`$./pss_start.sh`

**Primetime 스트리밍 서버를 Live Packager 또는 HTTP Origin Server로 구성**

스트리밍 서버를 Live Packager 또는 Origin Server로 구성하려면 스트리밍 서버의 루트 디렉토리의 conf 디렉토리에 있는 pss.xml 구성 파일을 업데이트합니다.

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Primetime 스트리밍 서버 중지**

스트리밍 서버를 중지하려면 스트리밍 서버의 루트 디렉토리에서 다음 명령을 실행합니다.\
`$./pss_stop.sh`

**Primetime 스트리밍 서버 다시 시작**

스트리밍 서버를 다시 시작하려면 스트리밍 서버를 중지하고 시작합니다.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Primetime 스트리밍 서버 제거**

스트리밍 서버를 제거하려면 스트리밍 서버를 중지하고 Primetime 디렉토리에서 스트리밍 서버의 pss 디렉토리를 제거합니다.

## Live Packager 및 Origin Server 1.4를 사용한 작업 {#working-with-live-packager-and-origin-server}

이 조항은 Primetime 스트리밍 서버가 사용되지 않고 대신 Primetime Live Packager 및/또는 Primetime Origin Server가 배포되는 경우에 적용됩니다

### 최소 시스템 요구 사항 {#minimum-system-requirements-1}

**네트워크 요구 사항**

* 인코더에서 Live Packager로 MPEG-TS 스트림을 전송하려면 네트워크에서 멀티캐스트가 활성화되어 있어야 합니다. 또한 Live Packager는 멀티캐스트 네트워크가 필요 없는 인코더에서 RTMP 스트림을 허용합니다.

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제:4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장(다중 네트워크 카드 및 10Gb 지원)
* 디스크:

   * (Disk-SAS):최소 10GB(7.5K RPM 포함)
   * (디스크-SSD):400MBps 읽기/쓰기
   * (NAS) :1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java JRE 1.7(권장:Sun/Oracle 핫스팟 JVM). JMX API에 대한 JConsole 액세스에 JDK가 필요합니다.

위의 최소 시스템 요구 사항은 Live Packager뿐만 아니라 Origin Server에도 적용됩니다.

### Live Packager {#install-and-configure-the-live-packager} 설치 및 구성

**Live Packager 설치**

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java SE 및 JDK 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
1. Adobe Primetime - Live Packager 1.4 아카이브 파일 `Primetime-LivePackager-1-4-0-b206-12042014.zip`을 디스크에 추출합니다.

**HTTP 원본 서버 설치**

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java JRE 및 JDK 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
1. Adobe Primetime - HTTP Origin Server 1.4 아카이브 파일 `Primetime-HttpOrigin-1-4-0-b206-12042014.zip` 을 디스크에 추출합니다.

**Live Packager를** 시작하려면 Packager의 루트 디렉토리에서 다음 명령을 실행하십시오.\
`$packager_start.sh`

**HTTP 원본 서버를 시작하려면**

HTTP 원본 서버를 시작하려면 원본 서버의 루트 디렉토리에 있는 명령줄에서 다음 명령을 실행합니다.\
`$./origin_start.sh`

**Live Packager 중지**

패키저를 중지하려면 패키지 프로그램의 루트 디렉토리에서 다음 명령을 실행하십시오.\
`$packager_stop.sh`

**HTTP 원본 서버 중지**

HTTP 원본 서버를 중지하려면 원본 서버의 루트 디렉토리에서 다음 명령을 실행합니다.\
`$./origin_stop.sh`

**Live Packager를 다시 시작합니다.**

Packager를 다시 시작하려면 패키지 프로그램을 중지하고 시작하십시오.

**참고**:패키지 프로그램이 시작되면 임시 디렉토리의 조각 대상의 부트스트랩 정보를 초기화하려고 합니다. 부트스트랩 정보가 조각 대상에 있으면 패키지가 다시 시작되었음을 의미합니다. 다시 시작하는 경우 패키지는 다음 조각 경계까지 기다린 다음 패키징을 시작합니다. 패키지가 부트스트랩에 간격 항목을 삽입하여 누락된 조각이 있음을 나타냅니다.

**HTTP 원본 서버를 다시 시작합니다.**

HTTP 원본 서버를 다시 시작하려면 HTTP 원본 서버를 중지하고 시작합니다.

**Live Packager 구성**

배포 파일에는 패키지 테스트를 위해 사용할 수 있는 샘플 구성이 포함되어 있습니다.

Adobe Primetime - Live Packager 1.4 아카이브를 추출하고 디렉토리를 Packager 디렉토리로 변경하고 packager_start.sh 스크립트를 실행합니다. 샘플 구성은 멀티캐스트 주소 239.235.0.3:14000에서 수신되고 포트 8080에서 로컬 원본 서버를 실행합니다. 출력이 `packager/webroot/_default_/_default_/ directory`에 기록되도록 구성되었습니다.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**HTTP 원본 서버 구성**

여기에서 제공되는 구성 세부 사항은 Primetime HTTP Origin Server 시작하기 문서를 참조하십시오.

**Live Packager 제거**

Packager를 제거하려면 Packager를 중지하고 Primetime 디렉토리에서 Packager 디렉토리를 제거합니다.

**HTTP 원본 서버 제거**

HTTP 원본 서버를 제거하려면 HTTP 원본 서버를 중지하고 Primetime 디렉토리에 있는 HTTP 원본 서버의 httprofile 디렉토리를 제거합니다.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### 최소 시스템 요구 사항 {#minimum-system-requirements-2}

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제:4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장(다중 네트워크 카드 및 10Gb 지원)
* 디스크:

   * (Disk-SAS):최소 10GB(7.5K RPM 포함)
   * (디스크-SSD):400MBps 읽기/쓰기
   * (NAS) :1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java JRE 1.7 이상.

### 오프라인 패키지 설치 및 구성 {#install-and-configure-offline-packager}

Offline Packager를 설치하려면 다음 단계를 수행합니다.

1. [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 Java SE 소프트웨어를 다운로드하고 설치 지침을 따릅니다.
1. Adobe Primetime - Offline Packager 1.4 아카이브 파일 `Primetime- OfflinePackager-1-4-0-b206-12042014.zip` 을 디스크에 추출합니다.

[여기](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)에서 사용할 수 있는 구성 세부 사항은 Primetime Offline Packager 시작하기 문서를 참조하십시오.

## 유용한 리소스 {#helpful-resources}

* [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지에서 전체 도움말 설명서를 참조하십시오.