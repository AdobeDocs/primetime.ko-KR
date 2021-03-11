---
description: ClosedCaptionStyles 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다. 플레이어에 표시되는 닫힌 캡션의 스타일을 설정합니다.
title: 자막 스타일 제어
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# 닫힌 캡션 스타일 제어{#control-closed-caption-styling}

ClosedCaptionStyles 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다. 플레이어에 표시되는 닫힌 캡션의 스타일을 설정합니다.

이 클래스는 글꼴 유형, 크기, 색상 및 배경 불투명도와 같은 닫힌 캡션 스타일 정보를 캡슐화합니다. 연결된 헬퍼 클래스 `ClosedCaptionStylesBuilder`에서는 자막 스타일 설정을 사용하여 작업을 쉽게 할 수 있습니다.

## 닫힌 캡션 스타일 {#section_DAE84659D1964DB1B518F91B59AF29D9} 설정

TVSDK 메서드를 사용하여 자막 텍스트의 스타일을 지정할 수 있습니다.

1. MediaPlayer가 PREMITED 상태 이상을 가질 때까지 기다립니다([유효한 상태](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md) 대기 참조).
1. 스타일 설정을 변경하려면 다음 중 하나를 수행합니다.

   * `ClosedCaptionStylesBuilder` 도우미 클래스를 사용합니다(백그라운드에서 `ClosedCaptionStyles`에서 작동).
   * `ClosedCaptionStyles` 클래스를 직접 사용합니다.

>[!NOTE]
>
>닫힌 캡션 스타일을 설정하는 것은 비동기 작업이므로 변경 사항이 화면에 표시되는 데 최대 몇 초가 걸릴 수 있습니다.

## 닫힌 캡션 스타일 옵션 {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

`ClosedCaptionStyles` 클래스를 사용하여 닫힌 캡션 트랙에 대한 스타일 정보를 제공할 수 있습니다. 플레이어에 표시되는 닫힌 캡션의 스타일을 설정합니다.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
```

>[!TIP]
>
>기본값(예: `DEFAULT`)을 정의하는 옵션에서 해당 값은 캡션이 원래 지정된 시점을 나타냅니다.

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
   <td colname="2"> <p>글꼴 유형입니다. </p> <p><span class="codeph"> ClosedCaptionStyles.FONT </span> 배열로 정의된 값으로만 설정할 수 있으며 일련 번호를 포함하거나 포함하지 않고 고정 폭(예: )을 나타냅니다. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>팁: 장치에서 사용할 수 있는 실제 글꼴은 다양하며 필요한 경우 대체 글꼴을 사용합니다. 이 대체는 시스템별로 사용할 수 있지만 일반적으로 직렬이 있는 고정 공간은 대체용으로 사용됩니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 크기 </td> 
   <td colname="2"> <p>캡션의 크기입니다. </p> <p> <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span> 배열로 정의된 값만 설정할 수 있습니다. 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 중간  </span> - 표준 크기 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE  </span> - 중간 크기보다 약 30% 큼 </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 중소기업  </span> - 중간 크기보다 약 30% 작음 </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT  </span> - 캡션의 기본 크기입니다.미디어와 동일 </li> 
     </ul> </p> <p>팁: <span class="codeph"> DefaultMediaPlayer.ccStyles </span> 함수의 크기 매개 변수를 변경하여 WebVTT 캡션의 글꼴 크기를 변경할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 가장자리 </td> 
   <td colname="2"> <p>글꼴 가장자리에 사용되는 효과(예: 높이거나 없음). </p> <p><span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span> 배열로 정의된 값만 설정할 수 있습니다. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 색상 </td> 
   <td colname="2"> <p>글꼴 색상입니다. </p> <p><span class="codeph"> ClosedCaptionStyles.COLOR </span> 배열로 정의된 값만 설정할 수 있습니다. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 가장자리 색상 </td> 
   <td colname="2"> <p>가장자리 효과의 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값으로 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경색 </td> 
   <td colname="2"> <p>배경 문자 셀 색상입니다. </p> <p>글꼴 색상에 사용할 수 있는 값만 설정할 수 있습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 칠 색상 </td> 
   <td colname="2"> <p>텍스트가 있는 창의 배경색입니다. </p> <p>글꼴 색상에 사용할 수 있는 값으로 설정할 수 있습니다. </p> <p>중요: WebVTT는 이 기능을 사용하지 않으므로 WebVTT 캡션에는 적용되지 않습니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 글꼴 불투명도 </td> 
   <td colname="2"> <p>텍스트의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 글꼴의 DEFAULT_OPACITY </span> 는 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 배경 불투명도 </td> 
   <td colname="2"> <p>배경 문자 셀의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 배경에  </span> 대한 DEFAULT_OPACITY는 100입니다. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 칠 불투명도 </td> 
   <td colname="2"> <p>캡션 창의 배경의 불투명도입니다. </p> <p>0(완전 투명)에서 100(완전히 불투명)까지의 백분율로 표현됩니다. <span class="codeph"> 채우기에  </span> 대한 DEFAULT_OPACITY는 0입니다. </p> </td> 
  </tr> 
 </tbody> 
</table>

## 예:캡션 서식 {#section_63E33840B7A14D26990046E2ACF2ECA1}

닫힌 캡션 서식을 지정할 수 있습니다.

## 예 1:형식 값을 명시적으로 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4} 지정합니다.

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## 예 2:매개 변수 {#section_147036D7C31C4010A5A7DF49997014A9}에 형식 값을 지정합니다.

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
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
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
