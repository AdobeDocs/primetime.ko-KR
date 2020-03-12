---
description: 미디어 플레이어의 상태는 올바른 작업을 결정합니다.
seo-description: 미디어 플레이어의 상태는 올바른 작업을 결정합니다.
seo-title: MediaPlayer 객체의 라이프사이클 및 상태
title: MediaPlayer 객체의 라이프사이클 및 상태
uuid: a0eb27c8-180b-4c56-926f-59fa3bcef032
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# MediaPlayer 객체의 라이프사이클 및 상태 {#lifecycle-and-statuses-of-the-mediaplayer-object}

미디어 플레이어의 상태는 올바른 작업을 결정합니다.

미디어 플레이어 상태 작업:

* 로 `MediaPlayer` 객체의 현재 상태를 검색할 수 `MediaPlayer.getStatus()`있습니다.

* 상태 목록은 MediaPlayerStatus [열거형에 정의되어](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) 있습니다.

인스턴스 라이프사이클에 대한 상태 전환 다이어그램: `MediaPlayer`
<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

다음 표에서는 미디어 플레이어의 라이프사이클 및 상태에 대한 세부 사항을 제공합니다.

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 상태 </th> 
   <th colname="col2" class="entry"> 다음 경우에 발생합니다. </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 유휴 </td> 
   <td colname="col2"> <p>미디어 플레이어의 초기 상태입니다. 플레이어가 생성되어 미디어 플레이어 항목을 지정하기를 기다리고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 초기화 중 </td> 
   <td colname="col2"> <p>응용 프로그램에서 <span class="codeph"> MediaPlayer.replaceCurrentItem()을 </span>호출합니다. </p> <p>미디어 플레이어 항목을 로드하는 중입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 초기화됨 </td> 
   <td colname="col2"> <p>TVSDK가 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 준비 </td> 
   <td colname="col2"> <p>응용 프로그램에서 <span class="codeph"> MediaPlayer.prepareToPlay()를 </span>호출합니다. 미디어 플레이어가 미디어 플레이어 항목 및 관련 리소스를 로드하고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 준비 완료 </td> 
   <td colname="col2"> <p>TVSDK가 미디어 스트림을 준비했고 광고 확인 및 광고 삽입(활성화된 경우)을 수행하려고 했습니다. 컨텐츠가 준비되고 광고가 타임라인에 삽입되었거나 광고 절차가 실패했습니다. </p> <p>버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 재생/일시 중지됨 </td> 
   <td colname="col2"> <p>응용 프로그램이 미디어를 재생하고 일시 중지하면 미디어 플레이어가 이러한 상태 사이를 이동합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 일시 중단 </td> 
   <td colname="col2"> <p>응용 프로그램이 재생을 중단하고 장치를 종료하거나, 플레이어가 재생 또는 일시 정지하는 동안 응용 프로그램을 전환하는 경우 미디어 플레이어가 일시 중단되고 리소스가 해제됩니다. </p> <p>MediaPlayer <span class="codeph"> .restore()를 </span> 호출하면 플레이어가 일시 중단되기 전의 상태로 플레이어가 반환됩니다. 일시 중지를 호출할 때 플레이어가 SEARCHING인 경우는 예외입니다. 플레이어는 일시 중지되고 일시 중단됩니다. </p> <p>중요:  <p>다음 정보를 기억하십시오. 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">MediaPlayer <span class="codeph"> 는 MediaPlayerView에서 사용되는 표면 개체가 </span> 멸실된 경우에만 일시 중단을 <span class="codeph"> 자동으로 </span> 호출합니다 <span class="codeph"> </span> . </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">MediaPlayer <span class="codeph"> 는 MediaPlayerView에서 사용하는 새 표면 개체를 만들 </span> 때만 <span class="codeph"> restore()를 </span> 자동으로 <span class="codeph"> 호출합니다 </span> . </li> 
      </ul> </p> </p> <p>MediaPlayer가 복원될 때 항상 재생을 일시 중지하려면 Android Activity의 onPause() <span class="codeph"> 메서드에서 응용 프로그램에서 MediaPlayer. </span> pause() <span class="codeph"> </span> 를 호출하도록 하십시오. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 완료 </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달했으며 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 릴리스됨 </td> 
   <td colname="col2"> <p>애플리케이션이 미디어 플레이어를 릴리스하여 관련 리소스도 릴리스했습니다. 더 이상 이 인스턴스를 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 오류 </td> 
   <td colname="col2"> <p>프로세스 중에 오류가 발생했습니다. 오류가 발생하면 다음에 응용 프로그램이 수행할 수 있는 작업에도 영향을 줄 수 있습니다. 자세한 내용은 <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> 오류 처리 설정을 </a>참조하십시오. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 다음 상태 변경을 기다리는 동안 프로세스에 대한 피드백을 제공하거나 다음 방법을 호출하기 전에 적절한 상태를 기다리는 등의 다음 단계를 수행하여 미디어를 재생할 수 있습니다.

예:

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```

