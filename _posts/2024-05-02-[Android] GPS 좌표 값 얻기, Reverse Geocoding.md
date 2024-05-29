---
title : "[Android] GPS 좌표 값 얻기 + Reverse Geocoding"
date : 2024-05-02 23:06:00 +0900
categories : [Android]
tags : [android, gps, reverse geocoding] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

### [Android] GPS 좌표 값 얻기 + Reverse Geocoding

---



프로젝트를 진행하는 도중, 애뮬레이터의 현재 위치 값을 받아오는 일이 생겼다. 구글링을 통해 여러 방법을 시도해보았다. 

하지만 LocationManager.getLastKnwonLocation(...) 함수를 통해 반환 받는 값이 null인 것을 보고 이전에 설정된 좌표 값이 없다면 null이 리턴 되는 것으로 유추했고 좌표를 먼저 설정 후 받아오려고 하였으나 잘 해결되지 않아 해결 방법을 공유하려고 한다.



#### 1. 권한 설정

GPS 위치 좌표는 민감 정보에 해당하기에 먼저 권한을 주어야한다. AndroidManifest.xml 파일에 다음 두 줄을 추가하여 준다.

```xml
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```



#### 2. 라이브러리 추가

build.gradle.kts 파일의 dependencies { } 안에 다음 문장을 입력하고 상단 Sync now를 통해 라이브러리를 추가한다.

```kotlin
implementation ("com.google.android.gms:play-services-location:21.0.1")
```



#### 3. 권한 요청

위치 권한을 확인하고 허용되어 있지 않다면 권한을 다시 요청한다.

```java
if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && ActivityCompat.checkSelfPermission(this, android.Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(this, new String[]{android.Manifest.permission.ACCESS_FINE_LOCATION, android.Manifest.permission.ACCESS_COARSE_LOCATION}, 100);
        return;
}
```



#### 4. latitude, Longitude 좌표 얻어오기

```java
FusedLocationProviderClient fusedLocationProviderClient = LocationServices.getFusedLocationProviderClient(context);

fusedLocationProviderClient.getCurrentLocation(LocationRequest.PRIORITY_HIGH_ACCURACY, new CancellationToken() {
    @NonNull
    @Override
    public CancellationToken onCanceledRequested(@NonNull OnTokenCanceledListener onTokenCanceledListener) { return null; }
    @Override
    public boolean isCancellationRequested() { return false; }
}).addOnSuccessListener(location -> {
    try {
        Double lat = location.getLatitude();
        Double lon = location.getLongitude();
    } catch (Exception ignored) { }
});
```



#### 5. 추가

얻어온 좌표를 토대로 Reverse Geocoding을 수행할 수 있는데 방법은 다음과 같다

```java
Geocoder geocoder = new Geocoder(this);

List<Address> addressList = geocoder.getFromLocation(lat,lon,10);
addressList.get(0).getCountryCode();
```

##### 다른 메서드로 도시 정보 등도 얻어올 수 있다. 



#### 6. 주의 사항 

GPS 좌표를 얻어오는 중에 애뮬레이터가 실행중인 노트북의 위치가 나올 것이라 예상하였다. 하지만 계속해서 미국 캘리포니아 좌표가 반환되었고 이는 노트북의 위치가 아닌 애뮬레이터에서 설정한 위치를 그대로 받아오는 것으로 유추했다. 추후 공기계에서 테스트 시에 기능 확인이 필요할 것으로 보인다. 애뮬레이터의 위치는 옮기는 방법은 다음과 같다

| ![0](https://github.com/6-keem/BlogImageRepository/assets/113224939/38089533-2864-48fc-abdf-687da0e1f7c6) | ![1](https://github.com/6-keem/BlogImageRepository/assets/113224939/f6aca6a6-2f64-4fd4-b77b-8fff92696a9e) | ![2](https://github.com/6-keem/BlogImageRepository/assets/113224939/ee796d3a-843c-4b32-8c4a-25e5653dc0f1) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |

##### 1. 애뮬레이터 상단 버튼 클릭

##### 2. Location Tab 선택

##### 3. 원하는 지역 찾아서 Set Location 

