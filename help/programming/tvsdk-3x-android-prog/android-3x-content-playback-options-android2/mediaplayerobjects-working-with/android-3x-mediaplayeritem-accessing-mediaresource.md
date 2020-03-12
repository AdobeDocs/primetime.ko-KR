---
description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-description: MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.
seo-title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
title: MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# MediaResource 정보에 액세스하기 위한 MediaPlayerItem 메서드 {#mediaplayeritem-methods-for-accessing-mediaresource-information}

MediaPlayerItem 클래스의 메서드를 사용하면 로드된 MediaResource로 표시되는 컨텐츠 스트림에 대한 정보를 얻을 수 있습니다.

| 메서드 | 설명 |
|--- |--- |
| **광고 태그** |  |
| List`<String>` getAdTags() | 광고 배치 프로세스에 사용되는 광고 태그 목록을 제공합니다. |
| **라이브 스트림** |  |
| boolean isLive(); | 스트림이 라이브인 경우 True;VOD인 경우 false입니다. |
| **DRM 보호** |  |
| boolean isProtected(); | 스트림이 DRM으로 보호되는 경우 true입니다. |
| getDRMMetadataInfos`<DRMMetadataInfo>` (); 목록 | 매니페스트에서 검색된 모든 DRM 메타데이터 개체를 나열합니다. |
| **자막** |  |
| boolean hasClosedCaptions(); | 자막 트랙을 사용할 수 있으면 true입니다. |
| List`<ClosedCaptionsTrack>` getClosedActionsTracks(); | 사용 가능한 자막 트랙 목록을 제공합니다. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | SelectClosedCaptionsTrack을 사용하여 선택한 현재 닫힌 캡션 트랙을 검색합니다. |
| selectClosedCaptionsTrack(ClosedCaptionsTrack closedCaptionsTrack) | 자막 트랙을 현재 자막 트랙으로 설정합니다. |
| **대체 오디오 트랙** |  |
| boolean hasAlternateAudio(); | 스트림에 대체 오디오 트랙이 있으면 true입니다. 참고: 기본(기본) 오디오 트랙은 대체 오디오 트랙 목록에도 포함되어 있습니다.  Android용 TVSDK는 기본 오디오 트랙을 대체 오디오 트랙 목록에 있는 항목 중 하나로 간주합니다. 이로 인해 MediaPlayerItem.hasAlternateAudio가 false를 반환하는 유일한 경우는 스트림에 오디오가 전혀 없을 때입니다. 내용에 오디오 트랙이 하나만 있으면 이 메서드는 true를 반환하고 단일 요소(기본 오디오 트랙)가 있는 목록을 `MediaPlayerItem.getAudioTracks` 반환합니다. |
| getAudioTracks`<AudioTrack>` (); 목록 | 사용 가능한 대체 오디오 트랙 목록을 제공합니다. |
| AudioTrack getSelectedAudioTrack(); | selectAudioTrack으로 선택한 오디오 트랙을 검색합니다. |
| selectAudioTrack( AudioTrack audioTrack ) | 현재 오디오 트랙으로 사용할 오디오 트랙을 선택합니다. |
| **시간 지정 메타데이터** |  |
| boolean hasTimedMetadata(); | 스트림에 시간 지정 메타데이터가 연결되어 있으면 true입니다. |
| List`<TimedMetadata>` getTimedMetadata(); | 스트림과 연관된 시간 메타데이터 개체의 목록을 제공합니다. |
| **다양한 프로파일(비트 전송률)** |
| boolean isDynamic(); | 스트림이 MBR(다중 비트 전송률) 스트림이면 true입니다. |
| 목록`<Profile>` getProfiles(); | 연결된 비트 전송률 프로파일 목록을 제공합니다. 각 프로필에 대해 해당 비트율, 프로파일의 높이와 너비를 검색할 수 있습니다. |
| 프로필 getSelectedProfile() | 현재 선택한 프로파일을 검색합니다. |
| **트릭 플레이** |  |
| boolean isTrickPlaySupported(); | 플레이어가 빨리 감기, 되감기 및 다시 시작을 지원하는 경우 true입니다. |
| List`< Float>` getAvailablePlaybackRates() | 트릭 플레이 기능의 컨텍스트에서 사용 가능한 재생 속도 목록을 제공합니다. |
| 부동 getSelectedPlaybackRate() | 현재 선택한 재생 속도를 검색합니다. |
| MediaPlayerItemConfig getConfig() | 이 항목과 연결된 MediaPlayerItemConfig 인스턴스를 반환합니다. |
| **미디어 리소스** |  |
| MediaResource getResource(); | 이 항목과 연결된 미디어 리소스를 반환합니다. |
| int getResourceId() | 이 항목과 연결된 미디어 식별자를 반환합니다. 이 ID는 항목이 MediaPlayerItemLoader.load를 사용하여 로드될 때 설정됩니다. |