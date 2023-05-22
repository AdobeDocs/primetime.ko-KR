---
description: TextFormat 클래스를 사용하여 자막 트랙의 스타일 정보를 제공할 수 있습니다. 플레이어에서 표시하는 모든 폐쇄 캡션의 스타일을 설정합니다.
title: 자막 스타일 제어
exl-id: 0083c141-9c03-46a2-902b-6e7eebaadea4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 자막 스타일 제어 {#control-closed-caption-styling-overview}

TextFormat 클래스를 사용하여 자막 트랙의 스타일 정보를 제공할 수 있습니다. 플레이어에서 표시하는 모든 폐쇄 캡션의 스타일을 설정합니다.

이 클래스는 글꼴 유형, 크기, 색상 및 배경 불투명도와 같은 자막 스타일 정보를 캡슐화합니다. 연결된 도우미 클래스, `TextFormatBuilder`를 사용하면 자막 스타일 설정으로 쉽게 작업할 수 있습니다.

## 선택 캡션 스타일 설정 {#set-closed-caption-styles}

TVSDK 메서드를 사용하여 자막 텍스트의 스타일을 지정할 수 있습니다.

1. 미디어 플레이어가 적어도 준비됨 상태가 될 때까지 기다립니다.
1. 만들기 `TextFormatBuilder` 인스턴스.

   모든 자막 스타일 매개 변수를 지금 제공하거나 나중에 설정할 수 있습니다.

   TVSDK는 폐쇄 캡션 스타일 정보를 캡슐화합니다. `TextFormat` 인터페이스. 다음 `TextFormatBuilder` 클래스는 이 인터페이스를 구현하는 개체를 만듭니다.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. 를 구현하는 개체에 대한 참조를 가져오려면 `TextFormat` 인터페이스, 호출 `TextFormatBuilder.toTextFormat` 공용 메서드.

   이 값은 `TextFormat` 미디어 플레이어에 적용할 수 있는 개체입니다.

   ```java
   public TextFormat toTextFormat()
   ```

1. 필요한 경우 다음 중 하나를 수행하여 현재 자막 스타일 설정을 가져옵니다.

   * 를 사용하여 모든 스타일 설정 가져오기 `MediaPlayer.getCCStyle`.

      반환 값은 `TextFormat` 인터페이스.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * 다음을 통해 설정을 한 번에 하나씩 가져옵니다. `TextFormat` 인터페이스 getter 메서드.

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. 스타일 설정을 변경하려면 다음 중 하나를 수행합니다.

   >[!NOTE]
   >
   >WebVTT 캡션의 크기는 변경할 수 없습니다.

   * setter 메서드 사용 `MediaPlayer.setCCStyle`, 의 인스턴스 전달 `TextFormat` 인터페이스:

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * 사용 `TextFormatBuilder` 개별 setter 메서드를 정의하는 클래스입니다.

      다음 `TextFormat` 인터페이스는 getter 메서드만 있고 설정자는 없도록 변경할 수 없는 개체를 정의합니다. 폐쇄 캡션 스타일 매개 변수는 `TextFormatBuilder` 클래스:

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

폐쇄 캡션 스타일을 설정하는 것은 비동기 작업이므로 변경 사항이 화면에 표시되는 데 최대 몇 초 정도 걸릴 수 있습니다.

## 선택 캡션 스타일 옵션 {#closed-caption-styling-options}

여러 캡션 스타일 옵션을 지정할 수 있으며 이러한 옵션은 원래 캡션의 스타일 옵션을 재정의합니다

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>기본값(예: DEFAULT)을 정의하는 옵션에서 해당 값은 캡션이 처음 지정되었을 때의 설정을 나타냅니다.

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
 </tbody> 
</table>

## 캡션 서식 예 {#examples-caption-formatting}

폐쇄 캡션 서식을 지정할 수 있습니다.

**예제 1: 형식 값을 명시적으로 지정**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**예제 2: 매개 변수에 형식 값 지정**

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
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
