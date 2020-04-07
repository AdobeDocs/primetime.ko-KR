---
seo-title: 사용 모델 데모 활성화
title: 사용 모델 데모 활성화
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 6e949c2f88deef88f0d0ac95b18c006da1c89d2f

---


# 사용 모델 데모 활성화{#enable-the-usage-model-demo}

1. 패키징 `RI_UsageModelDemo=true` 시 사용자 지정 속성을 지정합니다.

   Media Packager 명령줄 도구를 사용하여 컨텐츠를 패키지하는 경우 다음을 입력합니다.

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>패키징 시 선택적 데모 모드를 활성화하지 않는 경우 라이선스 서버는 첫 번째 유효한 DRM 정책을 기반으로 라이센스를 발행합니다.

