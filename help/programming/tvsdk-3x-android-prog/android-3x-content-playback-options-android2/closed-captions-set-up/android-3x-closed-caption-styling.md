---
description: 플레이어에서 표시하는 폐쇄 캡션의 스타일을 설정하는 TextFormat 클래스를 사용하여 폐쇄 캡션 트랙의 스타일 정보를 제공할 수 있습니다.
title: 자막 스타일 제어
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# 자막 스타일 제어 {#control-closed-caption-styling}

플레이어에서 표시하는 폐쇄 캡션의 스타일을 설정하는 TextFormat 클래스를 사용하여 폐쇄 캡션 트랙의 스타일 정보를 제공할 수 있습니다.

이 클래스는 글꼴 유형, 크기, 색상 및 배경 불투명도와 같은 닫힌 캡션 스타일 정보를 캡슐화합니다.

## 선택 캡션 스타일 설정 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

TVSDK 메서드를 사용하여 자막 텍스트의 스타일을 지정할 수 있습니다.

1. 미디어 플레이어가 적어도 다음 위치에 있을 때까지 대기: `PREPARED` 상태.
1. 만들기 `TextFormatBuilder` 인스턴스.

   모든 자막 스타일 매개 변수를 지금 제공하거나 나중에 설정할 수 있습니다.

   TVSDK는 폐쇄 캡션 스타일 정보를 캡슐화합니다. `TextFormat` 인터페이스. 다음 `TextFormatBuilder` 클래스는 이 인터페이스를 구현하는 개체를 만듭니다.

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. 를 구현하는 개체에 대한 참조를 가져오려면 `TextFormat` 인터페이스, 호출 `TextFormatBuilder.toTextFormat` 공용 메서드.

   이 값은 `TextFormat` 미디어 플레이어에 적용할 수 있는 개체입니다.

   `public TextFormat toTextFormat()`


1. 필요한 경우 다음 중 하나를 수행하여 현재 자막 스타일 설정을 가져옵니다.

   * 를 사용하여 모든 스타일 설정 가져오기 `MediaPlayer.getCCStyle` 반환 값은 `TextFormat` 인터페이스.

     ```java
     /** 
     * @return the current closed captioning style.  
     * If no style was previously set, it returns a TextFormat object 
     * with default values for each attribute. 
     * @throws MediaPlayerException if media player was already released. 
     */ 
     public TextFormat getCCStyle() throws MediaPlayerException;
     ```

   * 다음을 통해 설정을 한 번에 하나씩 가져옵니다. `TextFormat` 인터페이스 getter 메서드.

     ```java
     public java.lang.String getFontColor(); 
     public java.lang.String getBackgroundColor(); 
     public java.lang.String getFillColor(); // retrieve the font fill color 
     public java.lang.String getEdgeColor(); // retrieve the font edge color 
     public TextFormat.Size getSize(); // retrieve the font size 
     public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
     public TextFormat.Font getFont(); // retrieve the font type 
     public int getFontOpacity(); 
     public int getBackgroundOpacity(); 
     public java.lang.String getBottomInset(java.lang.String bi); 
     public java.lang.String getSafeArea(java.lang.String sa);
     ```

1. 스타일 설정을 변경하려면 다음 중 하나를 수행합니다.

   * setter 메서드 사용 `MediaPlayer.setCCStyle`, 의 인스턴스 전달 `TextFormat` 인터페이스:

     ```java
     /** 
     * Sets the closed captioning style. Used to control the closed captioning font, 
     * size, color, edge and opacity.  
     * 
     * This method is safe to use even if the current media stream doesn't have closed 
     * captions. 
     * 
     * @param textFormat 
     * @throws MediaPlayerException 
     */ 
     public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
     ```

   * 사용 `TextFormatBuilder` 개별 setter 메서드를 정의하는 클래스입니다.

     다음 `TextFormat` 인터페이스는 getter 메서드만 있고 설정자는 없도록 변경할 수 없는 개체를 정의합니다. 폐쇄 캡션 스타일 매개 변수는 `TextFormatBuilder` 클래스:

     ```java
     // set font type 
     public void setFont(Font font)  
     public void setBackgroundColor(String backgroundColor) 
     public void setFillColor(String fillColor) 
     // set the font-edge color 
     public void setEdgeColor(String edgeColor)  
     // set the font size 
     public void setSize(Size size)  
     // set the font edge type 
     public void setFontEdge(FontEdge fontEdge)  
     public void setFontOpacity(int fontOpacity) 
     public void setBackgroundOpacity(int backgroundOpacity) 
     // set the font-fill opacity level 
     public void setFillOpacity(int fillOpacity)  
     public void setFontColor(String fontColor) 
     public void setBottomInset(String bi) 
     public void setSafeArea(String sa) 
     public void setTreatSpaceAsAlphaNum(bool)
     ```

     >[!IMPORTANT]
     >
     >**색상 설정:** Android TVSDK 2.X에서는 폐쇄 캡션의 색상 스타일이 개선되었습니다. 향상된 기능을 통해 RGB 색상 값을 나타내는 16진수 문자열을 사용하여 닫힌 캡션 색상을 설정할 수 있습니다. RGB 16진수 색상 표현은 Photoshop과 같은 애플리케이션에서 사용하는 친숙한 6바이트 문자열입니다.
     >
     >* FFFFFF = 검정
     >* 000000 = 흰색
     >* FF0000 = 빨간색
     >* 00FF00 = 녹색
     >* 0000FF = 파랑
     >기타 등등.
     >
     >응용 프로그램에서 색상 스타일 정보를에 전달할 때마다 `TextFormatBuilder`, 여전히 `Color` 이전과 같이 열거되지만 이제 다음을 추가해야 합니다. `getValue()` 을 추가하여 값을 문자열로 가져옵니다. 예:
     >
     >`tfb = tfb.setBackgroundColor(TextFormat.Color.RED      <b>.getValue()</b>);`

폐쇄 캡션 스타일을 설정하는 것은 비동기 작업이므로 변경 사항이 화면에 표시되는 데 최대 몇 초 정도 걸릴 수 있습니다.

## 선택 캡션 스타일 옵션 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원래 캡션의 스타일 옵션을 재정의합니다.

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
```

>[!TIP]
>
>기본값을 정의하는 옵션(예: `DEFAULT`)에서 해당 값은 캡션이 원래 지정되었을 때의 설정을 나타냅니다.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 형식 </b></th> 
   <th colname="2" class="entry"> <b>설명</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 </td> 
   <td colname="2"> <p>글꼴 유형입니다. </p> <p>에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Font </span> 열거형이며 예를 들어 serifs가 있거나 없는 단일 간격을 나타냅니다. </p> <p>팁: 디바이스에서 사용할 수 있는 실제 글꼴은 다를 수 있으며, 필요한 경우 대체 글꼴이 사용됩니다. Serifs가 있는 Monospace는 일반적으로 대체물로 사용되지만, 이 대체물은 시스템에 따라 다를 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 크기 </td> 
   <td colname="2"> <p>캡션 크기입니다. </p> <p> 에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Size </span> 열거형: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 중간 </span> - 표준 크기 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 큼 </span> - 보통 대비 약 30% 큼 </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 작음 </span> - 보통 대비 약 30% 작음 </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 기본값 </span> - 캡션의 기본 크기이며, 중간과 동일 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 가장자리 </td> 
   <td colname="2"> <p>글꼴 가장자리에 사용되는 효과(예: 높임 또는 없음). </p> <p>에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.FontEdge </span> 열거형입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 색상 </td> 
   <td colname="2"> <p>글꼴 색상입니다. </p> <p>에 의해 정의된 값으로만 설정할 수 있습니다. <span class="codeph"> TextFormat.Color </span> 열거형입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 가장자리 색상 </td> 
   <td colname="2"> <p>가장자리 효과의 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값 중 하나로 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경색 </td> 
   <td colname="2"> <p>배경 문자 셀 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값으로만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 채우기 색상 </td> 
   <td colname="2"> <p>텍스트가 있는 창 배경의 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값 중 하나로 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 불투명도 </td> 
   <td colname="2"> <p>텍스트의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전 불투명)까지의 백분율로 표시됩니다. <span class="codeph"> DEFAULT_불투명도 </span> 글꼴은 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경 불투명도 </td> 
   <td colname="2"> <p>배경 문자 셀의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전 불투명)까지의 백분율로 표시됩니다. <span class="codeph"> DEFAULT_불투명도 </span> 배경은 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 칠 불투명도 </td> 
   <td colname="2"> <p>캡션 창 배경의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전 불투명)까지의 백분율로 표시됩니다. <span class="codeph"> DEFAULT_불투명도 </span> 채우기 값은 0입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 하단 삽입 </td> 
   <td colname="2"> <p>캡션을 피하기 위한 캡션 창 아래쪽으로부터의 세로 거리입니다. </p> <p>캡션 창 높이의 백분율(예: "20%") 또는 픽셀 수(예: "20")로 표시됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 안전 지역 </td> 
   <td colname="2"> <p>화면 가장자리 주변의 0%에서 25% 사이의 영역으로서, 캡션이 표시되지 않습니다. </p> <p>기본적으로 WebVTT의 안전 영역은 0%입니다. 이 설정을 사용하면 응용 프로그램에서 해당 기본값을 재정의할 수 있습니다. 문자열 "10%,20%"와 같이 두 개의 값이 제공된 경우 첫 번째 값은 수평 안전 영역이고 두 번째 값은 수직 안전 영역이다. 문자열 "15%"와 같이 하나의 값이 제공되면 세로 및 가로 축 모두 지정된 안전 영역을 사용합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 캡션 서식 예 {#section_58E8E82494EC4683B010FFDE67485CF9}

다음은 닫힌 캡션 서식을 지정하는 방법을 보여 주는 몇 가지 예입니다.

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.DEFAULT_OPACITY, 
            TextFormat.DEFAULT_OPACITY, 
            TextFormat.DEFAULT_OPACITY).toTextFormat(); 
 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity  
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity.  
*/ 
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
