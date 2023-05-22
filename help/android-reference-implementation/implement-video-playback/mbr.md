---
description: TVSDK는 비트 전송률이 다른 여러 프로필이 포함된 비디오를 재생하여 사용 가능한 대역폭을 기준으로 둘 이상의 품질 수준을 제공할 수 있습니다.
title: 다중 비트 전송률
exl-id: 5f71d69e-993a-4985-accd-7ce2104f837e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 다중 비트 전송률 {#multiple-bit-rates}

TVSDK는 비트 전송률이 다른 여러 프로필이 포함된 비디오를 재생하여 사용 가능한 대역폭을 기준으로 둘 이상의 품질 수준을 제공할 수 있습니다.

MBR(다중 비트 전송률) 스트림에 대한 ABR(적응형 비트 전송률) 스위치 정책뿐만 아니라 초기, 최소 및 최대 비트 전송률을 설정할 수 있습니다. TVSDK는 지정된 구성 내에서 최상의 재생 환경을 제공하는 비트 전송률로 자동 전환합니다.

참조 구현은에서 다음 ABR 매개 변수를 구성합니다 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html).

| 매개 변수 | 설명 |
|--- |--- |
| 초기 비트 전송률: getABRInitialBitRate | 첫 번째 세그먼트에 대한 원하는 재생 비트 전송률(초당 비트 수)입니다. 재생이 시작되면 첫 번째 세그먼트에 가장 가까운 프로필(초기 비트 전송률과 같거나 큰 프로필)이 사용됩니다.  최소 비트 레이트가 정의되고 초기 비트 레이트가 최소보다 낮은 경우, TVSDK는 최소 비트 레이트 이상의 가장 낮은 비트 레이트를 갖는 프로파일을 선택한다. 마찬가지로, 초기 레이트가 최대 레이트 이상이면, TVSDK는 최대 레이트 이하에서 가장 높은 레이트를 선택한다. 초기 비트 레이트가 0이거나 정의되지 않은 경우, 초기 비트 레이트는 ABR 정책에 의해 결정된다.  초당 바이트 프로필을 나타내는 정수 값을 반환합니다. |
| 최소 비트 전송률: getABRMinBitRate | ABR이 전환할 수 있는 가장 낮은 허용 비트 전송률입니다. ABR을 전환하면 이보다 비트 전송률이 낮은 프로필은 무시됩니다. 초당 비트 수를 나타내는 정수 값을 반환합니다. |
| 최대 비트 전송률: getABRMaxBitRate | ABR이 전환할 수 있는 가장 높은 허용 비트 전송률입니다. ABR을 전환하면 이보다 비트 전송률이 높은 프로필은 무시됩니다. 초당 비트 수를 나타내는 정수 값을 반환합니다. |
| ABR 전환 정책: getABRPolicy | 가능한 경우 재생이 가장 높은 비트 전송률 프로필로 점진적으로 전환됩니다. TVSDK가 프로필 간에 전환하는 속도를 결정하는 ABR 전환에 대한 정책을 설정할 수 있습니다. 기본값은 Modern입니다. <ul><li>*보수적*: 대역폭이 현재 비트 전송률보다 50% 높으면 비트 전송률이 다음으로 높은 프로파일로 전환합니다. </li><li>*중재*: 대역폭이 현재 비트 전송률보다 20% 더 높을 때 다음으로 높은 비트 전송률 프로필로 전환합니다.</li><li>*공격적*: 대역폭이 현재 비트율보다 높을 때 가장 높은 비트율 프로파일로 즉시 전환합니다</li></ul><br/>초기 비트 전송률이 0이거나 지정되지 않고 정책이 지정된 경우, 재생은 Conservative에 대한 가장 낮은 비트 전송률 프로필, Moderate에 대한 사용 가능한 프로필의 중간 비트 전송률에 가장 가까운 프로필 및 Aggressive에 대한 가장 높은 비트 전송률 프로필로 시작됩니다.<br/><br/>이 정책은 지정된 경우 최소 및 최대 비트율의 제한 내에서 작동합니다.  ABRControlParameters 열거형에서 현재 설정을 반환합니다. <ul><li>ABR_CONSERVATIVE</li><li>ABR_MODERATE </li><li>ABR_AGGRESSIVE</li></ul><br>참조: [정책](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/ABRControlParameters.ABRPolicy.html). |

>[!NOTE]
>
>* TVSDK는 제어 매개 변수를 엄격히 준수하는 것보다 지속적인 재생 환경을 선호하므로 TVSDK 장애 조치 메커니즘이 이러한 설정을 재정의할 수 있습니다.
>* 비트 전송률이 변경되면 TVSDK가 발송됩니다 `onProfileChanged` 의 이벤트 `PlaybackEventListener`.


## 참조 구현에서 사용자 지정 ABR 컨트롤 사용 {#section_72A6E7263E1441DD8D7E0690285515E6}

ABR(적응형 비트 전송률)은 기본적으로 TVSDK에서 활성화됩니다. Primetime 설정 사용자 인터페이스를 사용하여 사용자 지정 ABR 컨트롤을 구성하여 참조 구현에서 기본 TVSDK 동작을 재정의할 수 있습니다.

설정 사용자 인터페이스를 통해 사용자 정의 ABR을 활성화하려면 다음을 수행합니다.

* Primetime 설정 대화 상자를 엽니다.
* 선택 **[!UICONTROL ABR controls]**.

   ![](assets/abr-configuration.jpg)

* 탭 [!UICONTROL Enable ON] 을 표시하도록 제어 `OFF`.

다음 `PlaybackManager` 는 다음과 같은 경우에만 ABR 매개변수를 설정합니다. [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) true(ON)를 반환합니다. false(꺼짐)를 반환하는 경우 `PlaybackManager` 는 기본 ABR 컨트롤을 사용하므로 초기, 최소 및 최대 비트 전송률은 모두 0이 되고 ABR 정책은 `ABR_MODERATE`.

## 낮은 비트 전송률에 대한 구성 {#section_5451691CBBD24542AD54A474D222CD39}

일부 낮은 비트 전송률 재생 속도의 경우 TVSDK는 기본적으로 오디오 전용 스트림으로 전환되고 재생이 고정된 것으로 표시됩니다. 오디오 전용으로 전환하는 상황이 발생하지 않도록 플레이어를 구성할 수 있습니다.

* 구현 [IPlaybackConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html) 인터페이스:

* 다음을 확인합니다. [getABRMinBitRate](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#getABRMinBitRate()) 는 오디오 전용 비트 전송률보다 높습니다(64000보다 높음).
* 다음을 확인합니다. [isABRControlEnabled](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#isABRControlEnabled()) 켜짐.
