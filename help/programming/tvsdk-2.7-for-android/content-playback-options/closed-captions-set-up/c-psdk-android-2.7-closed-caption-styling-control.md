---
description: 플레이어에 표시되는 자막 스타일을 설정하는 TextFormat 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다.
seo-description: 플레이어에 표시되는 자막 스타일을 설정하는 TextFormat 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다.
seo-title: 자막 스타일 제어
title: 자막 스타일 제어
uuid: fa4f637f-f13c-465d-8eee-5e66a6dd9db2
translation-type: tm+mt
source-git-commit: 4ccc99f1ad6536ceb5e09c898dba3f71fa2de3f3
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# 자막 스타일 제어 {#control-closed-caption-styling}

플레이어에 표시되는 자막 스타일을 설정하는 TextFormat 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다.

이 클래스는 글꼴 유형, 크기, 색상 및 배경 불투명도와 같은 닫힌 캡션 스타일 정보를 캡슐화합니다.

## 자막 스타일 설정 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

TVSDK 방법을 사용하여 자막 텍스트의 스타일을 지정할 수 있습니다.

1. 미디어 플레이어가 적어도 `PREPARED` 상태가 될 때까지 기다립니다.
1. 인스턴스를 `TextFormatBuilder` 만듭니다.

   이제 모든 자막 스타일 지정 매개 변수를 제공하거나 나중에 설정할 수 있습니다.

   TVSDK는 `TextFormat` 인터페이스에 자막 스타일 정보를 캡슐화합니다. 이 `TextFormatBuilder` 인터페이스를 구현하는 객체를 만듭니다.

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

1. 인터페이스를 구현하는 개체에 대한 참조를 얻으려면 `TextFormat` public 메서드를 `TextFormatBuilder.toTextFormat` 호출합니다.

   >[!NOTE]
   >
   >미디어 플레이어에 적용할 수 있는 `TextFormat` 개체를 반환합니다.

   ```java
   public TextFormat toTextFormat()
   ```

1. 원하는 경우 다음 중 하나를 수행하여 현재 자막 스타일 설정을 가져옵니다.

   * 반환 값이 인터페이스의 인스턴스이므로 모든 스타일 설정 `MediaPlayer.getCCStyle` 을 `TextFormat` 가져옵니다.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * 인터페이스 getter 메서드를 통해 한 번에 하나씩 설정을 `TextFormat` 가져옵니다.

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

   * setter 메서드를 사용하여 인터페이스 인스턴스 `MediaPlayer.setCCStyle`를 `TextFormat` 전달합니다.

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

   * 개별 setter 메서드를 정의하는 `TextFormatBuilder` 클래스를 사용하십시오.

      인터페이스는 변경할 수 없는 객체를 정의하므로 getter 메서드만 있고 setter는 없습니다. `TextFormat` 닫힌 캡션 스타일 매개 변수는 `TextFormatBuilder` 클래스와 함께 설정할 수만 있습니다.

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
      >**색상 설정:** Android TV SDK 2.X에서는 자막 색상 스타일링을 향상시켰습니다. 향상된 기능을 통해 RGB 색상 값을 나타내는 16진수 문자열을 사용하여 닫힌 캡션 색상을 설정할 수 있습니다. RGB 16진수 색상 표현은 Photoshop과 같은 애플리케이션에서 사용하는 익숙한 6바이트 문자열입니다.
      >
      >    * FFFF = 검정
      >    * 000000 = 흰색
      >    * FF0000 = 빨간색
      >    * 00FF00 = 녹색
      >    * 0000FF = 파란색

      >
      >다양한 기능을 사용할 수 있습니다.
      >
      >응용 프로그램에서 색상 스타일 정보를 전달할 때마다 전과 같이 열거형 `TextFormatBuilder`을 사용하지만 이제 값을 문자열로 가져오려면 색상 `Color` `getValue()` 에 추가해야 합니다. 예:
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```




자막 스타일을 설정하는 것은 비동기 작업이므로 변경 사항이 화면에 나타나는 데 최대 몇 초가 걸릴 수 있습니다.

## 닫힌 캡션 스타일 옵션 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원본 캡션의 스타일 옵션을 덮어씁니다.

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
>기본값(예: `DEFAULT`)을 정의하는 옵션에서 해당 값은 캡션이 처음 지정된 시점을 나타냅니다.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 형식 </th> 
   <th colname="2" class="entry"> 설명 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 </td> 
   <td colname="2"> <p>글꼴 유형입니다. </p> <p>TextFormat.Font 열거형으로 정의된 값 <span class="codeph"> </span> 으로 설정할 수 있으며 serifs를 포함하거나 포함하지 않는 고정 간격(예: </p> <p>팁: 장치에서 사용할 수 있는 실제 글꼴은 다를 수 있으며 필요한 경우 대체 글꼴을 사용합니다. 이 대체는 시스템별로 지정할 수 있지만, serifs가 있는 고정 공간은 일반적으로 대용으로 사용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 크기 </td> 
   <td colname="2"> <p>캡션의 크기입니다. </p> <p> TextFormat.Size 열거형으로 정의된 값만 설정할 수 <span class="codeph"> </span> 있습니다. 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM </span> - 표준 크기 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE </span> - 중간 크기보다 약 30% 더 크게 </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL </span> - 중간 크기보다 약 30% 작음 </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT </span> - 캡션의 기본 크기입니다.미디어와 동일 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 가장자리 </td> 
   <td colname="2"> <p>글꼴 가장자리에 사용된 효과(예: 높이거나 없음). </p> <p>TextFormat.FontEdge 열거형으로 정의된 값만 설정할 <span class="codeph"> 수 </span> 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 색상 </td> 
   <td colname="2"> <p>글꼴 색상 </p> <p>TextFormat.Color 열거형으로 정의된 값만 설정할 수 <span class="codeph"> </span> 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 가장자리 색상 </td> 
   <td colname="2"> <p>가장자리 효과의 색상 </p> <p>글꼴 색상에 사용할 수 있는 값으로 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경색 </td> 
   <td colname="2"> <p>배경 문자 색상. </p> <p>글꼴 색상에 사용할 수 있는 값만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 채우기 색상 </td> 
   <td colname="2"> <p>텍스트가 있는 창의 배경색입니다. </p> <p>글꼴 색상에 사용할 수 있는 값으로 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 불투명도 </td> 
   <td colname="2"> <p>텍스트의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 글꼴의 DEFAULT_OPACITY </span> 는 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경 불투명도 </td> 
   <td colname="2"> <p>배경 문자 셀의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 배경에 대한 DEFAULT_OPACITY </span> 는 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 칠 불투명도 </td> 
   <td colname="2"> <p>캡션 창의 배경 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 채우기에 대한 DEFAULT_OPACITY </span> 는 0입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 아래쪽 인세트 </td> 
   <td colname="2"> <p>캡션을 피하려면 캡션 창 아래쪽에서 세로 거리입니다. </p> <p>캡션 창 높이(예: "20%") 또는 픽셀 수(예: "20")로 표현됩니다. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 안전 영역 </td> 
   <td colname="2"> <p>0%에서 25% 사이의 화면 가장자리 주변에 캡션이 표시되지 않는 영역입니다. </p> <p>기본적으로 WebVTT의 안전 영역은 0%입니다. 이 설정을 사용하면 응용 프로그램이 해당 기본값을 무시할 수 있습니다. 예를 들어 "10%,20%" 문자열을 제공하는 경우 첫 번째 값은 수평 보호 영역이고 두 번째 값은 수직 안전 영역입니다. 예를 들어 문자열 "15%"와 같은 하나의 값이 제공되면 세로 축과 가로 축에서 모두 지정된 안전 영역을 사용합니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 캡션 서식 예제 {#section_58E8E82494EC4683B010FFDE67485CF9}

다음은 닫힌 캡션 서식을 지정하는 방법을 보여주는 몇 가지 예입니다.

**예 1:형식 값을 명시적으로 지정합니다.**

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

**예 2:매개 변수의 형식 값 지정**

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
