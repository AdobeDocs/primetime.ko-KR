---
description: TVSDK 기능은 구성에 따라 구현되며 MediaPlayer를 통해 구현됩니다.
title: MediaPlayer에 구성 정보를 전달하여 기능 관리자 만들기
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}에 구성 정보를 전달하여 기능 관리자 만들기

TVSDK 기능은 구성에 따라 구현되며 MediaPlayer를 통해 구현됩니다.

* 구성은 ABR 컨트롤의 초기 비트 전송률 및 기본 닫힌 캡션 가시성과 같은 기능에 대한 특정 설정 목록입니다.

   기능 작동 방식을 결정하려면 기능 관리자가 구성을 받아야 합니다.

   Primetime 참조 구현에서 구성은 공유 환경 설정에 저장되지만 환경에 적합한 방식으로 구성을 저장할 수 있습니다.

* `MediaPlayer` 는 비디오 리소스를 포함하는 TVSDK 미디어 플레이어 객체입니다.

   기능 관리자는 TVSDK 이벤트 리스너를 이 플레이어 객체에 등록하고 재생 세션에서 데이터를 검색하고 재생 세션에 TVSDK 기능을 트리거합니다.

각 기능에는 해당 구성 인터페이스가 있습니다. 예를 들어 `CCManager`은 `ICCConfig`을 사용하여 구성을 검색합니다. `ICCConfig` 에는 자막 전용 관련 구성 정보를 가져오는 메서드가 포함되어 있습니다.

다음 예제에서는 `MediaPlayer`에서 닫힌 캡션 가시성, 글꼴 스타일 및 글꼴 가장자리에 대한 정보를 수신하도록 구성된 [!DNL ICCConfig.java] 파일을 보여 줍니다.

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

TVSDK 기능을 사용하는 응용 프로그램은 구성 공급자와 `MediaPlayer` 개체를 사용하여 해당 기능 관리자를 만들 수 있습니다. 예:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

기능 관리자 구성 API 문서:[Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)