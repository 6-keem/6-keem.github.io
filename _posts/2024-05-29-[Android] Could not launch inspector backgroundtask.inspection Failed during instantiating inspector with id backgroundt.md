---
title : "[Android] Could not launch inspector backgroundtask.inspection: Failed during instantiating inspector with id backgroundtask.inspection 오류"
date : 2024-05-29 14:02:00 +0900
categories : [Android]
tags : [android, room database] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

## [Anroid] Could not launch inspector backgroundtask.inspection: Failed during instantiating inspector with id backgroundtask.inspection 오류



Room Database 사용 중 Database를 내용을 보기 위해 App Inspection을 열었지만 해당 오류가 발생했다. 



##### 해결 방법 : build.gradle.kts (Module : app) 파일에서 targetSdk 버전을 낮춰주면 해결된다.

```kotlin
android {
    namespace = "패키지 명"
    compileSdk = 34

    defaultConfig {
        applicationId = "패키지 명"
        minSdk = 21
        targetSdk = 33 // 34 -> 33으로 
        versionCode = 1
        versionName = "1.0"

    }
...
```



