---
title : "[Linux] Ubuntu 한글 설정"
date : 2024-07-08 22:31:00 +0900
categories : [linux, 설정]
tags : [linux] #소문자만 가능
toc: true
toc_sticky: true
published : true
---
# [Linux] Ubuntu 한글 설정

크롤러를 만드는 중 gui가 필요하여 xrdp를 설치하여 접속하였다. 브라우저에서 검색을 하려고 하니 영어 밖에 입력이 되지 않고, 한글은 모두 깨져서 ㅁ으로 표시되는 일이 발생했다. 이 내용을 바탕으로 검색하여보니 많은 해결법들이 있었지만 나에게는 적용되지 않아 골머리를 앓았다. 

다음은 내가 해결한 방법이다.

먼저 설정에서 ibus-setup (ibus-preference)를 켜준다

<img width="1710" alt="3" src="https://github.com/6-keem/BlogImageRepository/assets/113224939/c1badf5c-d63d-4eb3-9698-b0d746ea4176">

설치 후 처음 실행한 것이라면 English 밖에 없을 것이다. ADD를 눌러 Korean을 검색한다.


<img width="1710" alt="1" src="https://github.com/6-keem/BlogImageRepository/assets/113224939/85d30642-04b0-4852-8371-60fec24d58dd">

korean을 클릭하면 나오는 Hangul이라는 input method를 선택하면 된다.
※ 다른 블로그에는 다른 입력 레이아웃도 나오는데 나는 Hangul 밖에 나오지 않았다.

<img width="1710" alt="2" src="https://github.com/6-keem/BlogImageRepository/assets/113224939/26daa143-a17e-4f35-abb3-150dd8ca39f8">

설치가 완료되면 Start in hangul mode 를 선택해주고 원하는 toggle key를 Add를 통해 설정하면 완료된다.
마지막으로 첫 페이지에 나온 English를 삭제 하여준다.

### 🚨 작동되지 않는 경우

나는 위와 같은 과정을 모두 수행하였는데 토글 키를 아무리 눌러도 한/영 전환이 되지 않았다.
Ibus-setup이 실행중일 때는 상단에 태극문양 버튼을 통해 전환이 가능했지만, close를 하면 사라져 ibus가 계속 실행되지 않는 것으로 문제를 유추해 볼 수 있었다.

#### 1. 환경변수 추가
> vi ~/.bashrc

```bash
export GTK_IM_MODULE=ibus 
export XMODIFIERS=@im=ibus 
export QT_IM_MODULE=ibus
```

#### 2. ibus가 백그라운드에서 실행되도록
> ibus-daemon -drxR
