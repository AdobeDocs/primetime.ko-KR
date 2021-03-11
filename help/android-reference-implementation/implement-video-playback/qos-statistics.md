---
description: 필요한 경우 QoSProvider에서 재생 및 디바이스 통계를 읽을 수 있도록 플레이어를 설정할 수 있습니다.
title: QoS 재생 및 디바이스 통계 표시
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# QoS 재생 및 디바이스 통계 표시 {#display-qos-playback-and-device-statistics}

필요한 경우 QoSProvider에서 재생 및 디바이스 통계를 읽을 수 있도록 플레이어를 설정할 수 있습니다.

`QoSProvider` 클래스는 프레임 속도, 프로필 비트 전송률, 버퍼링에서 보낸 총 시간, 버퍼링 시도 횟수, 첫 번째 비디오 조각에서 첫 번째 바이트를 가져오는 데 걸린 시간, 첫 번째 프레임을 렌더링하는 데 걸린 시간, 현재 버퍼링된 길이 및 버퍼 시간을 비롯한 다양한 통계를 제공합니다.

참조 구현은 QoS 오버레이의 표시를 활성화할 수 있는 `QoSManager` 클래스를 제공합니다. 설정 사용자 인터페이스에서 QoS 가시성을 활성화할 수도 있습니다.

![](assets/qos-configuration.jpg)

`QoSManager`은 디바이스 정보를 가져오고 미디어 플레이어에 연결하며 최신 QoS 정보로 업데이트하여 QoS 통계를 추적합니다.

**QoS 통계 보고 활성화 또는 비활성화**

1. ManagerFactory를 사용하여 QosManager를 만들거나 QoS 보고를 활성화합니다.

   * QosManager를 만들려면:
      * 이 응용 프로그램은 광고 워크플로우 기능을 사용해야 합니다.

   QoSManager qosManager = new QosManagerOn();

   * ManagerFactory를 사용하여 QoS 통계를 표시하려면 다음을 수행하십시오.

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >부울 값을 `false`으로 변경하면 QoS 보고가 비활성화됩니다.

2. 이벤트 리스너 추가:

   `qosManager.addEventListener(qosManagerEventListener);`

3. QoS 공급자를 만들고 플레이어 활동 컨텍스트에 연결합니다.

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >플레이어 활동이 파괴되는 경우 미디어 플레이어에서 분리하여 QOS 공급자를 정리하려면 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider())를 호출해야 합니다.

**관련 API 설명서**

* [QosManager 클래스](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [QosManagerOn 클래스](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
