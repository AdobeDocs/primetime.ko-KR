---
description: 미디어 플레이어의 상태에 따라 합법적인 작업이 결정됩니다.
title: MediaPlayer 개체의 라이프사이클 및 상태
exl-id: 6b43f334-bd21-4d0e-a123-fd99403a6082
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# MediaPlayer 개체의 라이프사이클 및 상태 {#lifecycle-and-statuses-of-the-mediaplayer-object}

미디어 플레이어의 상태에 따라 합법적인 작업이 결정됩니다.

미디어 플레이어 상태 작업의 경우:

* 의 현재 상태를 가져올 수 있습니다. `MediaPlayer` 개체 `MediaPlayer.getStatus()`.

* 상태 목록은 [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) 열거형.

의 라이프사이클에 대한 상태 전환 다이어그램 `MediaPlayer` 인스턴스:
<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

다음 표는 미디어 플레이어의 라이프사이클과 상태에 대한 세부 정보를 제공합니다.

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 상태 </th> 
   <th colname="col2" class="entry"> 다음과 같은 경우 발생 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 유휴 상태 </td> 
   <td colname="col2"> <p>미디어 플레이어의 초기 상태입니다. 플레이어가 만들어지고 미디어 플레이어 항목 지정을 기다리고 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 초기화 중 </td> 
   <td colname="col2"> <p>애플리케이션이 호출함 <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>미디어 플레이어 항목을 로드하는 중입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 초기화됨 </td> 
   <td colname="col2"> <p>TVSDK가 미디어 플레이어 항목을 설정했습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 준비 중 </td> 
   <td colname="col2"> <p>애플리케이션이 호출함 <span class="codeph"> MediaPlayer.prepareToPlay() </span>. 미디어 플레이어가 미디어 플레이어 항목 및 연결된 리소스를 로드 중입니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 준비됨 </td> 
   <td colname="col2"> <p>TVSDK가 미디어 스트림을 준비했으며 광고 해결 및 광고 삽입(활성화된 경우)을 수행하려고 했습니다. 콘텐츠가 준비되었고 광고가 타임라인에 삽입되었거나 광고 절차가 실패했습니다. </p> <p>버퍼링 또는 재생을 시작할 수 있습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 재생 중/일시 중지됨 </td> 
   <td colname="col2"> <p>애플리케이션이 미디어를 재생하고 일시 중지하면 미디어 플레이어가 이러한 상태 사이를 이동합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 일시 중단됨 </td> 
   <td colname="col2"> <p>플레이어가 재생 중이거나 일시 중지된 상태에서 애플리케이션이 재생을 떠나거나 디바이스를 종료하거나 애플리케이션을 전환하는 경우 미디어 플레이어가 일시 중지되고 리소스가 해제됩니다. </p> <p>호출 중 <span class="codeph"> MediaPlayer.restore() </span> 플레이어가 일시 중단되기 전의 상태로 플레이어를 반환합니다. 일시 중단되었을 때 플레이어가 찾기 중일 경우 플레이어가 일시 중지된 다음 일시 중지된 경우는 예외입니다. </p> <p>중요 사항:  <p>다음 정보를 숙지하십시오. 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">다음 <span class="codeph"> MediaPlayer </span> 자동 호출 <span class="codeph"> 일시 중단 </span> 에서 사용하는 서피스 개체일 때만 <span class="codeph"> MediaPlayerView </span> 이(가) 파괴되었습니다. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">다음 <span class="codeph"> MediaPlayer </span> 자동 호출 <span class="codeph"> restore() </span> 에서 사용하는 새 표면 개체가 있는 경우에만 <span class="codeph"> MediaPlayerView </span> 이(가) 만들어졌습니다. </li> 
      </ul> </p> </p> <p>MediaPlayer가 복원될 때 항상 재생이 일시 중지되도록 하려면 응용 프로그램 호출을 수행합니다 <span class="codeph"> MediaPlayer.pause() </span> Android 활동 <span class="codeph"> onPause() </span> 메서드를 사용합니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 완료 </td> 
   <td colname="col2"> <p>플레이어가 스트림 끝에 도달하여 재생이 중지되었습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 릴리스됨 </td> 
   <td colname="col2"> <p>애플리케이션이 미디어 플레이어를 릴리스하고 연결된 리소스도 릴리스합니다. 이 인스턴스를 더 이상 사용할 수 없습니다. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 오류 </td> 
   <td colname="col2"> <p>프로세스 도중 오류가 발생했습니다. 오류는 애플리케이션이 다음에 수행할 수 있는 작업에도 영향을 줄 수 있습니다. 자세한 내용은 <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> 오류 처리 설정 </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>상태를 사용하여 다음 상태 변경을 기다리는 동안 프로세스에 대한 피드백을 제공하거나 다음 메서드를 호출하기 전에 적절한 상태를 기다리는 등 미디어 재생의 다음 단계를 수행할 수 있습니다.

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
