---
title: '[BOOKREST] Kakao Maps API'
subtitle: '카카오 맵 api 사용한 경험을 공유합니다.'
date: 2021-07-27
category: 'Project'
---

BOOKREST는 온라인 / 오프라인 서비스다.
온라인으로 본인이 대여할 책을 예약하고 성공회대 BOOKREST로 와서 대여하는 방식이다.

따라서 오프라인 BOOKREST 위치를 알려주기 위해 오시는 길 페이지를 개발하기로 했다.

## Kakao Maps API

오시는 길 페이지에 Kakao map을 이용하였다.
map api는 아직까지 해본 적이 없어서 이번 기회에 배워보고 싶었다.

kakao 공식문서를 우선 찾아보았다.
👉🏻 https://apis.map.kakao.com/web/guide/#start

공식문서를 보면 자세히 설명되어있고 로드맵 등 다양한 기능들을 제공하고 있어 쉽게 이용할 수 있다.

## 개발

먼저 키 발급이 필요하다.

[카카오 개발자사이트](https://developers.kakao.com)에 접속하여 개발자 등록 및 앱 생성을 한다.

다음으로 앱 선택 > 플랫폼 > Web 플랫폼 등록 > 사이트 도메인 등록하면 된다.

사이트 도메인 등록: 웹 플랫폼을 선택하고, 사이트 도메인 을 등록한다.
(BOOKREST는 아직 따로 도메인이 없어 http://127.0.0.1:8000 로 등록하였다.)

그 후 페이지 상단의 JavaScript 키를 지도 API의 appkey로 사용한다.

여기까지 완료가 되었다면 이제 코드를 이용해 만들기만 하면 된다.

<b>html</b>

```html
<!-- <div>태그로 지도를 사용할 영역을 만들어준다. -->
<div class="map"></div>
```

<b>css</b>

```css
.map {
  width: 100%;
  height: 350px;
}
```

<b>Javascript API</b>

```javascript
<script
  type="text/javascript"
  src="//dapi.kakao.com/v2/maps/sdk.js?appkey=발급받은 APP KEY를 넣으시면 됩니다."
></script>
```

Javascript API는 반드시 실행 코드보다 먼저 선언되어야 한다.
지도 API의 appkey를 복사해 코드에 넣어주면 API를 받아온 것이다.

<b>Javascript</b>

```javascript
const container = document.querySelector('.map');
const options = {
  center: new kakao.maps.LatLng(37.48779388711603, 126.82514044863785), // 지도의 중심좌표
  level: 3, //지도의 레벨(확대, 축소 정도)
};
const map = new kakao.maps.Map(container, options);
```

지도의 중심좌표는 구글에 본인이 넣고자하는 장소를 검색해 우클릭을 하면 위치가 나온다.

![images_seulhyi_post_2aaaf3da-96e6-465f-8be4-64a33fcb27be_image](https://user-images.githubusercontent.com/63100352/175518153-7b7cd0be-7b8b-4e3c-8383-90b95282bcf2.png)

이를 이용해 중심좌표를 정할 수 있다.

## 실행

![images_seulhyi_post_b4035597-9cb7-4069-b455-c458a84c3b6d_image](https://user-images.githubusercontent.com/63100352/175518162-ae80792a-1f5a-43a2-84f4-2cade11c1c17.png)

중심좌표를 성공회대학교로 두어 실행을 하면 이와같이 뜬다.

> 근데 이걸론 좀 아쉽다 ... 마커를 찍어볼까 ?!

## 마커

마커란 지도에 올라가는 핀 모양의 이미지를 뜻한다.

```Javascript
// 마커가 표시될 위치입니다
const markerPosition = new kakao.maps.LatLng(37.48829223509457, 126.82500137418384);

// 마커를 생성합니다
const marker = new kakao.maps.Marker({
position: markerPosition
});

// 마커가 지도 위에 표시되도록 설정합니다
marker.setMap(map);
```

마커가 표시될 위치도 이전과 같이 세부적인 장소를 검색 후 위치를 넣어주면 된다.
나는 임시로 성공회대학교 구두인관으로 설정해두었다.

## 결과

![images_seulhyi_post_f8e6f5ed-a775-4aed-96fd-783f76a5e3ff_image](https://user-images.githubusercontent.com/63100352/175518156-59c42288-66e7-4cbd-8d34-1bfc913bcbf3.png)

성공회대학교가 중심으로 찍히고 성공회대학교 구두인관에 마커가 생긴 모습을 볼 수 있다.

확대 축소기능은 기본이고 이외에 로드맵, 길찾기, 지도 검색 등 다양한 기능이 있어 시간이 남는다면 적용해보려고 한다.
