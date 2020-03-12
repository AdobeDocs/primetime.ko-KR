---
description: 이 절차는 사용자가 닫힌 캡션 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.
seo-description: 이 절차는 사용자가 닫힌 캡션 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.
seo-title: 사용자가 캡션 추적 변경 허용
title: 사용자가 캡션 추적 변경 허용
uuid: 5a6d33f2-cece-48f6-8a68-fe76d9d2a950
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 사용자가 캡션 추적 변경 허용 {#allow-users-to-change-the-caption-track}

이 절차는 사용자가 닫힌 캡션 트랙을 선택할 수 있는 단추를 만드는 방법의 예입니다.

1. 단추를 만들어 닫힌 캡션 트랙을 변경합니다.

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

1. 사용 가능한 닫힌 캡션 트랙 목록을 문자열 배열로 변환합니다.

   자막은 활동이 있는 추적, 즉 TVSDK에서 데이터를 검색한 채널이 그에 따라 표시됩니다.

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
               String isActive = closedCaptionsTrack.isActive() ? " (" +  
                 getString(R.string.active)+ ")" : ""; 
               closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName() +  
                 isActive); 
           } 
       } 
       return closedCaptionsTracksAsStrings. 
         toArray(new String[closedCaptionsTracksAsStrings.size()]); 
   } 
   ```

1. 사용자가 단추를 클릭하면 모든 기본 닫힌 캡션 트랙을 나열하는 대화 상자가 표시됩니다.

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
               ClosedCaptionsTrack desiredClosedCaptionsTrack =  
                 currentItem.getClosedCaptionsTracks().get(whichButton); 
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
