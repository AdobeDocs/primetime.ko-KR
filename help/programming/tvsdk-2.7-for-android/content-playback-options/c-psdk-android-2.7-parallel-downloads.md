---
description: 비디오 및 오디오를 시리즈가 아니라 동시에 다운로드할 경우 시작 지연이 줄어듭니다.
title: 병렬 다운로드
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 병렬 다운로드 {#parallel-downloads}

비디오 및 오디오를 시리즈가 아니라 동시에 다운로드할 경우 시작 지연이 줄어듭니다.

병렬 다운로드를 통해 VOD(Video-On-Demand) 파일을 재생할 수 있고, 서버의 사용 가능한 대역폭 사용을 최적화하며, 버퍼 언더런 상태에 도달할 수 있는 가능성을 낮추며 다운로드 및 재생 간의 지연을 최소화합니다.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

병렬 다운로드가 없으면 TVSDK가 비디오 세그먼트에 대한 요청을 발행하고 비디오 세그먼트가 로드된 후 하나 또는 두 개의 오디오 세그먼트를 요청합니다. 병렬 다운로드 시 오디오 및 비디오 세그먼트가 순차적이 아니라 동시에 다운로드됩니다. 또한 두 개의 연결과 두 개의 HTTP 요청이 동시에 있으므로 데이터가 화면에 더 빠르게 도달합니다.

>[!NOTE]
>
>이 기능은 오디오 및 비디오가 다른 파일(무함유 컨텐츠)로 인코딩된 컨텐츠에만 적용되며 항상 혼합되어 있는 MP4 컨텐츠에는 적용되지 않습니다. HLS 컨텐츠는 종종 혼합되지 않습니다(특히 대체 오디오가 있는 경우).

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP 연결은 다음 단계에서 지연될 수 있습니다.

* 서버에 TCP/IP 연결을 설정할 때

   클라이언트와 서버가 통신하기로 동의했지만 아직 HTTP 통신이 발생하지 않았습니다. 이러한 유형의 지연은 클라이언트와 서버 사이의 인프라에 따라 다릅니다. 이 프로세스에서는 클라이언트와 서버 사이의 인터넷을 통해 경로를 검색하고 라우터와 방화벽과 같은 모든 디바이스가 데이터 전송에 동의하는지 확인합니다.
* TCP/IP 연결을 통해 세그먼트 또는 매니페스트에 대한 HTTP 요청을 보낼 때.

   서버는 요청을 받고 처리하고 데이터를 다시 클라이언트로 보내기 시작합니다. 지연 수준은 서버에서 소프트웨어의 로드 및 복잡성과 클라이언트가 요청을 보낼 때 업로드 연결 속도에 따라 다릅니다.

