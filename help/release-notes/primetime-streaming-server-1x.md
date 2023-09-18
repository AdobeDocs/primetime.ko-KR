---
title: Primetime 스트리밍 서버 릴리스
description: Primetime 스트리밍 서버 1.3 및 1.4 릴리스의 새로운 기능.
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Primetime 스트리밍 서버 릴리스 {#primetime-streaming-server-x-releases}

Primetime 스트리밍 서버 1.3 및 1.4 릴리스의 새로운 기능.

## Primetime Streaming Server 1.4의 새로운 기능(12월 릴리스) {#what-s-new-in-primetime-streaming-server-december-release}

**오프라인 패키지**

* 이제 출력 HLS 스트림에 MPEG-2 TS에 있는 ID3 메타데이터가 포함됩니다.
* 이제 HLS 오디오 전용 스트림에 연결된 정적 이미지가 있을 수 있습니다.
* HLS AES 암호화 워크플로우에 대한 사용자 입력으로서 IV 제공 지원
* Offline Packager에서 IV가 생성될 때 파일에 IV 출력 지원
* 재생 목록 작성자는 이제 다국어 오디오 그룹 및 다국어 WebVTT 자막 그룹을 미디어 스트림에 연결할 수 있습니다

**원본 서버**

* HLS AES 암호화는 라이브 및 VOD 워크플로우에 사용할 수 있습니다. Primetime Origin Just in Time은 수신 HLS 스트림 또는 MP4 파일에 HLS AES 암호화를 적용할 수 있습니다.
* 또한 수신 HDS 스트림을 HLS 스트림으로 변환하는 데 JIT HLS AES 암호화를 적용할 수도 있습니다.
* Primetime Origin은 이제 PHLS 스트림에 대한 SWF 허용 목록을 지원합니다. 이전에는 PHDS 스트림에 대해서만 지원되었습니다

**Primetime Live Package**

* 입력 RTMP 및 MPEG-2 TS 스트림에 대한 HLS AES-128 스트림 생성 지원

PHDS/PHLS 인증서가 새로 고쳐졌습니다. 동일한 항목의 새 만료일은 2016/10/01입니다.

### **릴리스 1.4에 포함된 버그 수정** {#bug-fixes-included-in-release}

* OfflinePackager 1.3.1에서 만든 PTPUB-282- HLS 집합 수준 매니페스트에 코덱 및 해상도 정보가 없습니다.
* PTPUB-353 - PlayListCreator는 집합 수준 매니페스트에 WebVTT 정보를 추가할 수 없습니다.
* PTPUB-583 - PlaylistCreator 도구가 예기치 않게 그룹 URI의 앞에 추가됩니다.
* PTPUB-605 플레이리스트 작성자가 각 변형 스트림에 자막 그룹을 나열하지 않음
* PTPUB-634 -Offline Packager가 SpliceInsert를 매니페스트에 추가합니다.
* PTPUB-635- 단일 광고 큐용으로 삽입된 여러 SpliceOut 태그.

### 릴리스 1.4의 알려진 문제 {#known-issue-in-release}

* 명령줄 큐와 스트림 내 큐가 모두 오프라인 packager 구성에서 제공되는 경우 DPIScte35 모드가 지정되더라도 PTPUB- 645 DPISimple 모드가 강제 적용됩니다.

## Primetime Streaming Server 1.3.1의 새로운 기능(5월 릴리스) {#what-s-new-in-primetime-streaming-server-may-release}

버전 1.3.1은 핫픽스를 나타냅니다. 다음과 같은 향상된 기능을 통해 JIT MP4 사용 사례의 주요 성능 향상으로 구성되어 있으므로 고객에게 권장되는 업그레이드입니다.

1. 키 회전이 포함된 DRM을 사용하여 원본 MP4 JIT m3u8 생성을 위한 성능 수정
1. JIT 매니페스트 요청에서 MP4 JIT 변환을 위해 생성된 조각 URI로 쿼리 매개 변수를 복사하기 위한 구성 &#39;CopyQueryParamToJITFragmentURIs&#39;가 추가되었습니다. 사용 예는 HTTP 원본 서버 설명서 를 참조하십시오
1. vod.xml에 추가된 구성/MP4Only 구성을 통해 JIT 변환에 대한 확장 없이 MP4 파일 허용

### 릴리스 1.3.1에 포함된 버그 수정 {#bug-fixes-included-in-release-1}

* 3759167 - 패키징 중 타임스탬프 예외 사항으로 인해 일부 SCTE35 큐가 출력 매니페스트에 도달하는 것은 아닙니다. SCTE35 메시지에서 SpliceInfoSection의 TimeSignal에 SpliceTime에 pts_adjustment를 적용합니다.

### 릴리스 1.3.1의 알려진 문제 {#known-issues-in-release}

* 3717039 - 패키저가 DPI 단순 모드 큐를 만들도록 구성된 경우 실제로 스플라이스 삽입 또는 배치 기회와 같은 특정 신호 유형을 찾고 이러한 신호 유형만 단순 모드 큐로 변환해야 합니다. 프로그램 시작, 네트워크 시작 등과 같은 다른 유형의 신호는 무시해야 합니다.

* 3718598 - Origin Server가 HSM 액세스가 활성화된 보호된 콘텐츠를 제공하도록 구성된 경우 백엔드 LunaSA 클라이언트는 HSM 모듈과 자주 통신합니다

## Primetime Streaming Server 1.3의 새로운 기능(4월 릴리스) {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3 릴리스는 스트리밍 컨텐츠, 향상된 유용성 및 보안에 대한 몇 가지 새로운 기능을 제공합니다.

**Live Packager 및 Origin Server의 통합 형태로서의 Primetime 스트리밍 서버**

Primetime Live Packager 및 Primetime Origin이 단일 구성 요소로 작동하게 됩니다. 이 구성 요소는 패키저 또는 오리진으로 사용하거나 결합된 기능을 사용하여 라이브 스트림을 패키징하고 호스팅할 수 있습니다.

이러한 서버에 통합된 파일 인터페이스를 제공하여 단일 시스템에서 쉽게 실행할 수 있도록 합니다. 별도의 Packager 또는 Origin으로 구성할 수 있는 유연성을 계속 제공합니다.

**Beta MPEG-DASH 지원**

Primetime Streaming Server는 라이브 및 VOD 워크플로우에 대한 MPEG-DASH 패키징을 지원합니다. 라이브 패키지 구성 요소는 수집 RTMP 또는 MPEG-2-TS 스트림을 DASH 형식으로 변환합니다. 원본 구성 요소는 DASH 스트림을 허용합니다.

VOD 워크플로우의 경우 Offline Packager 구성 요소는 MP4 및 TS 자산을 MPEG-DASH ISOBFF 형식으로 변환합니다.

**라이브 VOD로 전환**

이제 라이브 스트림 캡처 및 VOD 재생 보관을 지원하는 새 구성 요소 기록 서버를 사용할 수 있습니다. 이벤트의 일부에 대한 클립/하이라이트뿐만 아니라 전체 이벤트 재생 만들기를 지원합니다. 라이브 콘텐츠에서 오디오 전용 스트림을 레코딩하고 광고 또는 슬레이트를 제거하도록 구성할 수 있습니다. 레코딩 서버는 Primetime 스트리밍 서버와 타사 오리진에서 작동합니다.

**Primetime Live Packager의 RTMP에서 HLS로 전환**

Primetime Live Packager 구성 요소는 RTMP 스트림에서 HLS 스트림 생성을 지원합니다. 또한 Primetime DRM 및 Protected Streaming을 출력 HLS 스트림에 추가할 수 있습니다.

**Primetime Live Packager로 들어오는 RTMP 스트림에 대한 인증**

이제 usermgmt.jar은 Primetime Live Packager와 함께 제공되어 Primetime Live Packager에 RTMP 스트림을 전송할 때 신뢰할 수 있는 자격 증명으로 액세스를 구성합니다

이제 Live Packager로 스트림을 전송하는 동안 사용자 이름/암호를 사용하도록 인코더를 구성할 수 있습니다.

**HDS 및 HLS용 최상위 수준 매니페스트를 만들 수 있는 PlaylistCreator 도구**

이제 Primetime Offline Packager에서 PlaylistCreator.jar 유틸리티를 사용하여 HDS 및 HLS 에셋에 대한 최상위 매니페스트 파일을 쉽게 만들 수 있습니다.

**하드웨어 보안 모듈을 통합하는 추가 보안 기능**

Primetime Offline Packager는 이제 하드웨어 보안 모듈에서 Packager 자격 증명 인증서 및 일반 키 액세스를 지원합니다.

하드웨어 보안 모듈은 이러한 기밀 자산에 대한 추가 보호 기능을 제공합니다.

**VOD 패키지 성능 향상**

Primetime Offline Packager의 메자닌 에셋에 대한 패키징 시간을 개선하기 위해 몇 가지 성능 개선 사항이 통합되었습니다

**JIT MP4 패키지 성능 향상**

대용량 VOD 자산 라이브러리에 대한 사용자 요청을 처리하기 위해 Primetime Origin의 JIT 패키징 기능에 몇 가지 성능 개선 사항이 통합되었습니다.

## Adobe Primetime 스트리밍 서버 1.4 {#adobe-primetime-streaming-server}

### 최소 시스템 요구 사항 {#minimum-system-requirements}

**네트워크 요구 사항**

* 인코더에서 Live Packager로 MPEG-TS 스트림을 전송하기 위해 네트워크를 멀티캐스트로 활성화해야 합니다. Live Packager는 또한 멀티캐스트 네트워크가 필요하지 않은 인코더에서 RTMP 스트림을 받을 수 있습니다.

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제: 4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장 (여러 네트워크 카드 및 10Gb도 지원)
* 디스크:

   * (디스크-SAS) : 최소 10GB(7.5K RPM)
   * (디스크-SSD) : 400MBps 읽기/쓰기
   * (NAS) : 1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java JRE 1.7(권장: Sun/Oracle 핫스팟 JVM) JMX API에 대한 JConsole 액세스에는 JDK가 필요합니다

### Primetime 스트리밍 서버 설치 및 구성 {#install-and-configure-primetime-streaming-server}

**스트리밍 서버 설치**

1. 에서 Java SE 및 JDK 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
2. Adobe Primetime-Streaming Server 1.4 아카이브 파일 추출, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` 디스크에 저장합니다.

**Primetime 스트리밍 서버 시작**

스트리밍 서버를 시작하려면 스트리밍 서버의 루트 디렉터리에 있는 명령줄에서 다음 명령을 실행합니다.\
`$./pss_start.sh`

**Primetime 스트리밍 서버를 Live Packager 또는 HTTP 원본 서버로 구성**

스트리밍 서버를 라이브 패키지 또는 원본 서버로 구성하려면 스트리밍 서버의 루트 디렉토리에 있는 conf 디렉토리에 있는 pss.xml 구성 파일을 업데이트합니다.

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Primetime 스트리밍 서버 중지**

스트리밍 서버를 중지하려면 스트리밍 서버의 루트 디렉터리에서 다음 명령을 실행합니다.\
`$./pss_stop.sh`

**Primetime 스트리밍 서버 다시 시작**

스트리밍 서버를 다시 시작하려면 스트리밍 서버를 중지한 후 시작합니다.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Primetime 스트리밍 서버 제거**

스트리밍 서버를 제거하려면 스트리밍 서버를 중지하고 Primetime 디렉터리에서 스트리밍 서버의 pss 디렉터리를 제거합니다

## Live Packager 및 Origin Server 1.4 작업 {#working-with-live-packager-and-origin-server}

이 섹션은 Primetime 스트리밍 서버를 사용하지 않고 대신 Primetime Live Packager 및/또는 Primetime Origin Server가 배포되는 경우에 적용됩니다

### 최소 시스템 요구 사항 {#minimum-system-requirements-1}

**네트워크 요구 사항**

* 인코더에서 Live Packager로 MPEG-TS 스트림을 전송하기 위해 네트워크를 멀티캐스트로 활성화해야 합니다. Live Packager는 또한 멀티캐스트 네트워크가 필요하지 않은 인코더에서 RTMP 스트림을 받을 수 있습니다.

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제: 4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장 (여러 네트워크 카드 및 10Gb도 지원)
* 디스크:

   * (디스크-SAS) : 최소 10GB(7.5K RPM)
   * (디스크-SSD) : 400MBps 읽기/쓰기
   * (NAS) : 1GB 전용 링크

**소프트웨어 요구 사항**

* Oracle Java JRE 1.7(권장: Sun/Oracle 핫스팟 JVM) JMX API에 대한 JConsole 액세스에는 JDK가 필요합니다

위의 최소 시스템 요구 사항은 Origin Server와 Live Packager에도 적용됩니다.

### Live Packager 설치 및 구성 {#install-and-configure-the-live-packager}

**라이브 패키지 설치**

1. 에서 Java SE 및 JDK 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
1. Adobe Primetime - Live Packager 1.4 아카이브 파일 추출 `Primetime-LivePackager-1-4-0-b206-12042014.zip` 디스크에 저장합니다.

**HTTP Origin 서버 설치**

1. 에서 Java JRE 및 JDK 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
1. Adobe Primetime - HTTP Origin Server 1.4 아카이브 파일 추출, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`을 클릭하여 디스크에 저장합니다.

**Live Packager 시작하기** packager를 시작하려면 packager의 루트 디렉토리에서 다음 명령을 실행합니다.\
`$packager_start.sh`

**HTTP 원본 서버를 시작하려면**

HTTP Origin Server를 시작하려면 Origin Server의 루트 디렉토리에 있는 명령줄에서 다음 명령을 실행합니다.\
`$./origin_start.sh`

**라이브 패키지 중단**

packager를 중지하려면 packager의 루트 디렉토리에서 다음 명령을 실행합니다.\
`$packager_stop.sh`

**HTTP 원본 서버 중지**

HTTP 원본 서버를 중지하려면 원본 서버의 루트 디렉터리에서 다음 명령을 실행합니다.\
`$./origin_stop.sh`

**Live Packager 다시 시작**

패키지를 다시 시작하려면 패키지를 중지하고 시작합니다.

**참고**: 패키저가 시작되면 임시 디렉터리의 조각 타겟에서 부트스트랩 정보를 초기화합니다. 부트스트랩 정보가 조각 타겟에서 발견되면 이는 패키저가 다시 시작되었음을 의미합니다. 다시 시작하는 경우 패키지 작성기는 다음 조각 경계까지 기다렸다가 패키징을 시작합니다. 패키저는 누락된 조각이 있음을 나타내기 위해 부트스트랩에 갭 엔트리를 삽입합니다.

**HTTP 원본 서버 다시 시작**

HTTP 원본 서버를 다시 시작하려면 HTTP 원본 서버를 중지하고 시작합니다.

**라이브 패키지 구성**

배포 파일에는 패키지 테스트에 사용할 수 있는 샘플 구성이 포함되어 있습니다.

Adobe Primetime - Live Packager 1.4 아카이브를 추출한 후 디렉토리를 packager 디렉토리로 변경하고 packager_start.sh 스크립트를 실행합니다. 샘플 구성은 멀티캐스트 주소 239.235.0.3:14000에서 수신하고 포트 8080에서 로컬 원본 서버를 실행합니다. 출력은 다음에 작성되도록 구성됩니다. `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**HTTP 원천 서버 구성**

여기에서 사용 가능한 구성 세부 사항은 Primetime HTTP Origin Server 시작 문서를 참조하십시오.

**라이브 패키지 제거**

packager를 제거하려면 packager를 중지하고 Primetime 디렉터리에서 packager 디렉터리를 제거합니다.

**HTTP 원본 서버 제거**

HTTP Origin Server를 제거하려면 HTTP Origin Server를 중지하고 Primetime 디렉토리에서 HTTP Origin Server의 httporigin 디렉토리를 제거합니다.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### 최소 시스템 요구 사항 {#minimum-system-requirements-2}

**지원되는 운영 체제**

* Linux CentOS 6.3 64비트

**하드웨어 요구 사항**

* 3.2GHz Intel® Pentium® 4 프로세서(듀얼 Intel Xeon® 이상 권장)
* 64비트 운영 체제: 4GB RAM(8GB 권장)
* 1Gb 이더넷 카드 권장 (여러 네트워크 카드 및 10Gb도 지원)
* 디스크:

   * (디스크-SAS) : 최소 10GB(7.5K RPM)
   * (디스크-SSD) : 400MBps 읽기/쓰기
   * (NAS) : 1GB 전용 링크

**소프트웨어 요구 사항**

* Java JRE 1.7 이상 oracle

### 오프라인 패키지 설치 및 구성 {#install-and-configure-offline-packager}

Offline Packager를 설치하려면 다음 단계를 수행하십시오.

1. 에서 Java SE 소프트웨어 다운로드 [Oracle 사이트](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 설치 지침을 따르십시오.
1. Adobe Primetime - Offline Packager 1.4 아카이브 파일 추출, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`을 클릭하여 디스크에 저장합니다.

사용 가능한 구성 세부 정보는 Primetime Offline Packager 시작하기 문서를 참조하십시오 [여기](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## 유용한 리소스 {#helpful-resources}

* 다음 위치에서 전체 도움말 문서 를 참조하십시오. [Adobe Primetime 학습 및 지원](https://helpx.adobe.com/support/primetime.html) 페이지를 가리키도록 업데이트하는 중입니다.
