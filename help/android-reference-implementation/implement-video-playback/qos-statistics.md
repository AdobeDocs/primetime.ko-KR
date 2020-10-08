---
description: 필요한 경우 QoSProvider에서 재생 및 디바이스 통계를 읽을 수 있도록 플레이어를 설정할 수 있습니다.
seo-description: 필요한 경우 QoSProvider에서 재생 및 디바이스 통계를 읽을 수 있도록 플레이어를 설정할 수 있습니다.
seo-title: QoS 재생 및 디바이스 통계 표시
title: QoS 재생 및 디바이스 통계 표시
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# QoS 재생 및 디바이스 통계 표시 {#display-qos-playback-and-device-statistics}

필요한 경우 QoSProvider에서 재생 및 디바이스 통계를 읽을 수 있도록 플레이어를 설정할 수 있습니다.

이 `QoSProvider` 클래스는 프레임 속도, 프로필 비트 전송률, 버퍼링에서 보낸 총 시간, 버퍼링 시도 횟수, 첫 번째 비디오 조각에서 첫 번째 바이트를 가져오는 데 걸린 시간, 첫 번째 프레임을 렌더링하는 데 걸린 시간, 현재 버퍼링된 길이, 버퍼 시간 등 다양한 통계를 제공합니다.

참조 구현은 QoS 오버레이의 표시를 활성화할 수 있는 `QoSManager` 클래스를 제공합니다. 설정 사용자 인터페이스에서 QoS 가시성을 활성화할 수도 있습니다.

![](assets/qos-configuration.jpg)

디바이스 정보를 얻고 미디어 플레이어에 연결하며 최신 QoS 정보를 업데이트하여 QoS 통계를 추적합니다. `QoSManager`

**QoS 통계 보고 활성화 또는 비활성화**

1. QosManager를 만들거나 ManagerFactory를 사용하여 QoS 보고를 활성화합니다.

   * QosManager를 만들려면
      * 이 응용 프로그램은 광고 워크플로우 기능을 사용해야 합니다

   QoSManager qosManager = 새로운 QosManagerOn();

   * ManagerFactory를 사용하여 QoS 통계 표시를 활성화하려면:

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >QoS 보고를 `false` 비활성화하도록 부울 값을 변경합니다.

2. 이벤트 리스너를 추가합니다.

   `qosManager.addEventListener(qosManagerEventListener);`

3. QoS 공급자를 만들고 플레이어 활동 컨텍스트에 연결합니다.

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >플레이어 활동이 파괴되는 경우, 미디어 플레이어에서 분리하여 QOS 공급자를 정리하려면 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) 에 전화하십시오.

**관련 API 설명서**

* [클래스 QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [클래스 QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
