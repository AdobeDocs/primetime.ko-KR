---
description: 사용자가 자막 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.
seo-description: 사용자가 자막 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.
seo-title: 예 사용자가 캡션 트랙을 변경할 수 있도록 허용
title: 예 사용자가 캡션 트랙을 변경할 수 있도록 허용
uuid: 4b69d569-0d6e-4388-9fe3-488e2a4d762d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 예:사용자가 캡션 트랙{#example-allow-users-to-change-the-caption-track} 변경 허용

사용자가 자막 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.

1. 간단한 단추를 만들어 자막 트랙을 변경합니다.

   ```xml
      <Button 
     android:id="@+id/selectCC" 
     android:layout_width="wrap_content" 
     android:layout_height="wrap_content" 
     android:layout_alignParentBottom="true" 
     android:layout_alignParentRight="true" 
     android:layout_marginRight="10dp" 
     android:onClick="selectClosedCaptioningClick" 
     android:text="CC" /> 
   ```

1. 사용 가능한 닫힌 캡션 트랙 목록을 문자열 배열로 변환합니다. 자막 트랙은 TVSDK에서 데이터를 발견한 채널 등 활동이 있는 채널로 표시됩니다.

   ```java
   /** 
   * Converts the closed captions tracks to a string array. 
   * 
   * @return array of CC tracks 
   */ 
   private String[] getCCsAsArray() { 
       List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); 
       MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           List<ClosedCaptionsTrack> closedCaptionsTracks = 
             currentItem.getClosedCaptionsTracks(); 
           Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator(); 
           while (iterator.hasNext()) { 
               ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); 
               String isActive = closedCaptionsTrack.isActive() ? " (" + getString(R.string.active)+ ")" : ""; 
               closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName() + isActive); 
           } 
       } 
       return closedCaptionsTracksAsStrings.toArray(new 
       String[closedCaptionsTracksAsStrings.size()]); 
   } 
   ```

1. 사용자가 버튼을 클릭하면 모든 기본 CC 트랙이 나열된 대화 상자가 표시됩니다.

   ```java
      public void selectClosedCaptioningClick(View view) { 
       Log.i(LOG_TAG + "#selectClosedCaptions", "Displaying closed captions chooser dialog."); 
       final String items[] = getCCsAsArray(); 
       final AlertDialog.Builder ab = new AlertDialog.Builder(this); 
       ab.setTitle(R.string.PlayerControlCCDialogTitle); 
       ab.setSingleChoiceItems(items, selectedClosedCaptionsIndex, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
               // Select the new closed captioning track. 
               MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
               ClosedCaptionsTrack desiredClosedCaptionsTrack = currentItem.getClosedCaptionsTracks().get(whichButton); 
               boolean result = currentItem.selectClosedCaptionsTrack(desiredClosedCaptionsTrack); 
               if (result) { 
                   selectedClosedCaptionsIndex = whichButton; 
               } 
               // Dismiss dialog. 
               dialog.cancel(); 
           } 
       }).setNegativeButton(R.string.PlayerControlCCDialogCancel, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
           // Just cancel the dialog. 
           } 
       }); 
       ab.show(); 
   } 
   ```

