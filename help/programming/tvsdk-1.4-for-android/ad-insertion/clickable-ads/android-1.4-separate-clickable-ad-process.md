---
description: 플레이어의 UI 로직과 광고 클릭을 관리하는 프로세스를 구분해야 합니다. 한 가지 방법은 활동에 대해 여러 조각을 구현하는 것입니다.
title: 클릭 가능한 광고 프로세스 구분
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 클릭 가능한 광고 프로세스 구분{#separate-the-clickable-ad-process}

플레이어의 UI 로직과 광고 클릭을 관리하는 프로세스를 구분해야 합니다. 한 가지 방법은 활동에 대해 여러 조각을 구현하는 것입니다.

1. 하나의 조각을 구현하여 `MediaPlayer`을(를) 포함하고 비디오 재생을 담당하는 조각을 구현합니다.

   이 조각은 `notifyClick`을(를) 호출해야 합니다.

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. 다른 조각을 구현하여 광고를 클릭할 수 있음을 나타내는 UI 요소를 표시하고, 해당 UI 요소를 모니터링하고, 사용자 클릭 수를 `MediaPlayer`이 포함된 단편에 알립니다.

   이 조각은 조각 통신에 대한 인터페이스를 선언해야 합니다. 조각은 onAttach 라이프사이클 메서드 중 인터페이스 구현을 캡처하고 인터페이스 메서드를 호출하여 활동과 통신할 수 있습니다.

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
   
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container, Bundle 
                                savedInstanceState) { 
   
           // the custom fragment is defined by a custom button 
           viewGroup =  
             (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad, container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
   
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);  
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
               + " must implement OnAdUserInteraction"); 
           }  
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```

