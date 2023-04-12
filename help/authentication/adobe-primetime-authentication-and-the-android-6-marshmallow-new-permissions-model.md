---
title: Adobe Primetime 인증 및 Android 6 "Marshallow" 새 권한 모델
description: Adobe Primetime 인증 및 Android 6 "Marshallow" 새 권한 모델
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Adobe Primetime 인증 및 Android 6 &quot;Marshallow&quot; 새 권한 모델 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>이 페이지의 컨텐츠는 정보용으로만 제공됩니다. 이 API를 사용하려면 Adobe의 현재 라이선스가 필요합니다. 무단 사용이 허용되지 않습니다.

</br>

새로운 Android 6 Marshmallow 릴리스에서는 기존 Adobe Primetime 인증 SDK 버전 1.8 이상을 사용하는 앱의 동작에 영향을 줄 수 있는 권한 모델에 대한 일부 업데이트를 도입합니다. 

새로운 기능으로 새로운 Android OS가 제공합니다 [설치 시 및 런타임 시 앱이 필요로 하는 권한을 세밀하게 제어할 수 있습니다](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>아래 설명된 변경 사항은 다음과 같습니다 **Android 6.0용으로 특별히 개발된 애플리케이션에만 영향을 줍니다.** (targetSdkVersion=23). Android 6.0으로 업그레이드할 때 사용자의 장치에 이미 설치된 이전 응용 프로그램에는 영향을 주지 않습니다. 


특히, [API 수준 23](http://developer.android.com/sdk/api_diff/23/changes.html) 및 Adobe Primetime 인증 SDK를 사용하는 개발자는 사용자 지정 코드를 작성해야 합니다(아래의 코드 조각 참조) [허용/거부 권한 대화 상자를 트리거하려면](https://developer.android.com/training/permissions/requesting.html). 

다음은 장치 외부 저장소에 대한 쓰기 액세스를 요청하는 데 사용되는 코드 발췌문입니다.

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**사용자의 관점에서**&#x200B;설치 시 파일에 대한 읽기/쓰기 권한을 확인하는 창이 사용자에게 표시됩니다(아래 그림 2 참조). 이렇게 하면 다음 두 결과 중 하나가 생성됩니다.

1. 사용자가 **확인** 권한, 일반 인증 흐름이 유지되고 토큰이 글로벌 저장소에 저장됩니다. 토큰이 유효하면 사용자가 앱 및 Adobe Primetime 인증을 사용하는 앱 간에 인증됩니다.
1. 사용자가 **거부** 사용 권한, 저장소에서 쓰기 작업은 실패하고 사용자가 앱을 종료할 때만 인증됩니다. 일부 응용 프로그램은 전경과 배경 간을 전환할 때 다시 초기화되므로 이 작업을 수행할 때 사용자가 로그아웃됩니다. 토큰은 저장되지 않으며 사용자는 앱을 사용할 때마다 인증해야 합니다. 


>[!TIP]
>
>저장소 복원 기능을 도입하는 기능은 현재 Adobe Primetime 인증 SDK 1.9용 개발 중입니다. 새 SDK는 다음에 타깃팅됩니다 **10월 마지막 주에 릴리스**. 일반 저장소를 사용할 수 없을 때마다 애플리케이션이 애플리케이션의 샌드박스 스토리지에 쓰기 작업을 폴백합니다. API 레벨 23에서 개발된 애플리케이션의 경우 사용자가 글로벌 스토리지에서 읽기/쓰기 권한을 허용하지 않는 경우를 다룹니다. 토큰은 앱별로 개별적으로 저장되므로 Adobe Primetime 인증을 사용하는 앱 간 단일 사인온이 비활성화됩니다.


![](assets/android-permissions-request.png)

*그림: 타깃팅 API 수준 23을 작성한 앱에 대한 권한 요청 대화 상자*

>[!IMPORTANT]
>
> Adobe 조언 **인증 프로세스에서 최상의 사용자 경험을 보장하기 위해 API 수준 22(targetSdkVersion=22) 이상을 사용하여 앱을 개발하는 파트너가 있습니다**. 
