---
description: 비디오와 오디오를 시리즈가 아닌 병렬로 다운로드하면 시작 지연이 줄어듭니다.
title: 병렬 다운로드
exl-id: 6c93154b-8de4-448b-bc33-776fcc1f6243
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 병렬 다운로드 {#parallel-downloads}

비디오와 오디오를 시리즈가 아닌 병렬로 다운로드하면 시작 지연이 줄어듭니다.

병렬 다운로드를 사용하면 VOD(Video-on-Demand) 파일을 재생할 수 있고, 서버에서 사용 가능한 대역폭 사용을 최적화하고, 버퍼 언더런 상황에 도달할 확률을 낮추고, 다운로드와 재생 사이의 지연을 최소화합니다.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

병렬 다운로드가 없으면 TVSDK에서 비디오 세그먼트에 대한 요청을 발행하고 비디오 세그먼트가 로드된 후 하나 또는 두 개의 오디오 세그먼트를 요청합니다. 병렬 다운로드를 사용하면 오디오 및 비디오 세그먼트가 순차적으로 다운로드되지 않고 동시에 다운로드됩니다. 또한 세그먼트당 두 개의 연결과 두 개의 HTTP 요청이 동시에 존재하므로 데이터가 화면에 더 빠르게 도달합니다.

>[!NOTE]
>
>이 기능은 오디오와 비디오가 서로 다른 파일로 인코딩된 콘텐츠(믹싱되지 않은 콘텐츠)에만 적용되고, 항상 믹싱되는 MP4 콘텐츠에는 적용되지 않습니다. HLS 콘텐츠는 특히 대체 오디오의 경우 종종 믹싱이 해제됩니다.

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP 연결은 다음 단계에서 지연이 발생할 수 있습니다.

* 서버에 TCP/IP 연결 설정 시

   클라이언트와 서버가 통신하기로 동의했지만 아직 HTTP 통신이 발생하지 않았습니다. 이러한 지연 유형은 클라이언트와 서버 사이의 인프라에 따라 다릅니다. 이 프로세스에서는 클라이언트와 서버 간 인터넷을 통해 경로를 찾고 라우터와 방화벽 등 경로에 있는 모든 장치가 데이터 전송에 동의하는지 확인해야 합니다.
* TCP/IP 연결을 통해 세그먼트 또는 매니페스트에 대한 HTTP 요청을 보낼 때.

   서버가 요청을 수신하고 처리하고 데이터를 다시 클라이언트로 보내기 시작합니다. 지연의 정도는 서버의 소프트웨어 부하 및 복잡성에 따라 다르며, 클라이언트가 요청을 전송할 때의 업로드 연결 속도에 따라 다소 달라집니다.
