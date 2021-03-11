---
title: 사용 모델 데모 사용
description: 사용 모델 데모 사용
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 사용 모델 데모 사용{#enable-the-usage-model-demo}

1. 패키징 시 사용자 지정 속성 `RI_UsageModelDemo=true`을 지정합니다.

   Media Packager 명령줄 도구를 사용하여 내용을 패키지하는 경우 다음을 입력합니다.

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>패키징 시 선택적 데모 모드를 활성화하지 않는 경우 라이선스 서버는 첫 번째 유효한 DRM 정책을 기반으로 라이센스를 발행합니다.

