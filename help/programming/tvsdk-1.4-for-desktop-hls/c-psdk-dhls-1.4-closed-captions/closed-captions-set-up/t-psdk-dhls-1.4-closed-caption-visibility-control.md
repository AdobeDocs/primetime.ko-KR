---
description: 닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 켜져 있으면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하는 경우 가시성 설정은 동일하게 유지됩니다.
title: 닫힌 캡션 표시 제어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 닫힌 캡션 표시 제어{#control-closed-caption-visibility}

닫힘 캡션의 가시성을 제어할 수 있습니다. 가시성이 켜져 있으면 현재 선택한 트랙이 표시됩니다. 현재 트랙을 변경하는 경우 가시성 설정은 동일하게 유지됩니다.

>[!TIP]
>
>플레이어가 찾기 모드에 들어갈 때 닫힌 캡션 텍스트가 표시되면 찾기가 완료된 후 텍스트가 더 이상 표시되지 않습니다. 대신, 몇 초 후에 TVSDK는 종료 탐색 위치 후에 비디오에 다음 자막 텍스트를 표시합니다.

>[!NOTE]
>
>폐쇄 캡션의 가시성 값은에 정의되어 있습니다. `ClosedCaptionsVisibility`.
>
>```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```
>

1. 다음을 기다리십시오. `MediaPlayer` 적어도 PREPARED 상태를 가지고 있어야 합니다(참조). [유효한 상태를 기다립니다.](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. 닫힘 캡션에 대한 현재 가시성 설정을 가져오려면 `MediaPlayer`- 가시성 값을 반환합니다.

   ```
   public function get ccVisibility():String
   ```

1. 닫힘 캡션의 가시성을 변경하려면 setter 메서드를 사용하여 가시성 값을 다음 위치에 전달합니다. `ClosedCaptionsVisibility`.

   예:

   ```
   public function set ccVisibility(value:String):void
   ```

1. 드롭다운 목록을 정의합니다.

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. 선택 캡션 트랙의 바인딩 가능한 배열을 정의합니다.

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. 리스너를 설정합니다.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   삭제 코드에서 리스너를 제거하려면:

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. 사용자가 목록에서 선택할 때 목록을 만들고 업데이트합니다.

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```
