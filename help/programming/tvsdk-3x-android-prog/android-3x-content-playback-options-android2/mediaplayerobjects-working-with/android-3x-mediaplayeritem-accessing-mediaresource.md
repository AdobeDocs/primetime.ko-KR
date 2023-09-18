---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.
title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource가 나타내는 콘텐츠 스트림에 대한 정보를 얻을 수 있습니다.

| 방법 | 설명 |
|--- |--- |
| **태그 추가** |  |
| 목록`<String>` getAdTags() | 광고 배치 프로세스에 사용되는 광고 태그 목록을 제공합니다. |
| **라이브 스트림** |  |
| 부울 isLive(); | 스트림이 라이브이면 True이고, VOD이면 False입니다. |
| **DRM 보호** |  |
| 부울 isProtected(); | 스트림이 DRM으로 보호되면 True입니다. |
| 목록`<DRMMetadataInfo>` getDRMMetadataInfos(); | 매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. |
| **폐쇄 캡션** |  |
| 부울 hasClosedCaptions(); | 자막 트랙을 사용할 수 있는 경우 True입니다. |
| 목록`<ClosedCaptionsTrack>` getClosedCationsTracks(); | 사용 가능한 자막 트랙 목록을 제공합니다. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | SelectClosedCaptionsTrack 을 사용하여 선택한 현재 닫힌 캡션 트랙을 검색합니다. |
| selectClosedCaptionsTrack( ClosedCaptionsTrack closedCaptionsTrack) | 자막 트랙을 현재 자막 트랙으로 설정합니다. |
| **대체 오디오 트랙** |  |
| 부울 hasAlternateAudio(); | 스트림에 대체 오디오 트랙이 있는 경우 True입니다. 참고: 기본(기본) 오디오 트랙도 대체 오디오 트랙 목록의 일부입니다.  Android용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록의 항목 중 하나로 간주합니다. 이러한 이유로 MediaPlayerItem.hasAlternateAudio가 false를 반환하는 유일한 경우는 스트림에 오디오가 전혀 없는 경우입니다. 컨텐츠에 하나의 오디오 트랙만 있는 경우 이 메서드는 true를 반환하고,  `MediaPlayerItem.getAudioTracks`  단일 요소(기본 오디오 트랙)가 있는 목록을 반환합니다. |
| 목록`<AudioTrack>` getAudioTracks(); | 사용 가능한 대체 오디오 트랙 목록을 제공합니다. |
| AudioTrack getSelectedAudioTrack(); | selectAudioTrack 을 사용하여 선택한 오디오 트랙을 검색합니다. |
| selectAudioTrack ( AudioTrack audioTrack ) | 오디오 트랙을 현재 오디오 트랙으로 선택합니다. |
| **시간 메타데이터** |  |
| 부울 hasTimedMetadata(); | 스트림에 시간 메타데이터가 연결된 경우 True입니다. |
| 목록`<TimedMetadata>` getTimedMetadata(); | 스트림과 연결된 시간이 지정된 메타데이터 개체의 목록을 제공합니다. |
| **여러 프로필(비트 전송률)** |
| 부울 isDynamic(); | 스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. |
| 목록`<Profile>` getProfiles(); | 연결된 비트 전송률 프로필 목록을 제공합니다. 각 프로필에 대해 비트 전송률과 프로필의 높이 및 너비를 검색할 수 있습니다. |
| 프로필 getSelectedProfile() | 현재 선택한 프로필을 검색합니다. |
| **트릭 플레이** |  |
| 부울 isTrickPlaySupported(); | 플레이어가 빨리 감기, 되감기 및 재개를 지원하는 경우 True입니다. |
| 목록`< Float>` getAvailablePlaybackRates() | 트릭 재생 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. |
| getSelectedPlaybackRate() 부동 | 현재 선택한 재생 속도를 검색합니다. |
| MediaPlayerItemConfig getConfig() | 이 항목과 연결된 MediaPlayerItemConfig 인스턴스를 반환합니다. |
| **미디어 리소스** |  |
| MediaResource getResource(); | 이 항목과 연결된 미디어 리소스를 반환합니다. |
| int getResourceId() | 이 항목과 연결된 미디어 식별자를 반환합니다. 이 ID는 MediaPlayerItemLoader.load 를 사용하여 항목을 로드할 때 설정됩니다. |
