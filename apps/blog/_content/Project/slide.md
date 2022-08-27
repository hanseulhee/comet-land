---
title: '[BOOKREST] Slide'
subtitle: '슬라이드 개발기를 공유합니다.'
date: 2021-08-03
category: 'Project'
---

BOOKREST main 페이지에 들어갈 slide를 javascript로 개발했다.

slide를 통해 BOOKREST가 어떤 서비스인지 바로 알 수 있도록 하기위해 이미지를 Figma로 제작하였다.

포토샵을 해본 적이 별로 없어서 지인의 도움을 받아 만들어 볼 수 있었다.

## Slide 사진

![](https://images.velog.io/images/seulhyi/post/a9e5fdbb-4707-4f93-947e-2b59d8c9bd98/BOOKREST_slider1.png)![](https://images.velog.io/images/seulhyi/post/e00163c6-db36-469e-9405-4876e4d6d08e/BOOKREST_slider4.png)![](https://images.velog.io/images/seulhyi/post/e18038f7-c201-479b-9dac-d1a695820296/BOOKREST_slider2.png)![](https://images.velog.io/images/seulhyi/post/84d22e06-6ef5-4c01-b805-ae6c50729da2/BOOKREST_slider3.png)

---

## 개발

<b>html</b>

```html
<!-- slide의 큰 틀 -->
<div class="container">
  <!-- slide의 틀 -->
  <div class="container__slider js-container__slider">
    <div class="blank"></div>
    <!-- slide에 들어갈 이미지 -->
    <img class="container__slider__img js-container__slider__img" src="{% static 'img/main.png'%}" />
    <img class="container__slider__img js-container__slider__img" src="{% static 'img/main2.png'%}" />
    <img class="container__slider__img js-container__slider__img" src="{% static 'img/main3.png'%}" />
    <img class="container__slider__img js-container__slider__img" src="{% static 'img/main4.png'%}" />
    <div class="blank"></div>
  </div>
</div>
```

slide 틀을 만들고 slide에 들어갈 이미지를 넣었다.
전에는 class 명을 짓기 귀찮아서 대충 짓곤 했는데 개발을 하다 보니 이 요소가 어떤 클래스고 어떤 div에 감싸져있는지 수정할 때마다 신경 써야 하는 점이 번거로웠다.

그래서 class 명을 <b>BEM방식</b>으로 지을려고 노력하고 있다.
실제 현업이나 팀플을 할 때에도 내가 만든 코드를 보고 무슨 코드인지 누가 봐도 다 알도록 해야 한다.
처음엔 번거로울지 몰라도 하다 보면 BEM방식이 오히려 쉽다.
👉 [CSS BEM 참고](https://nykim.work/15)

<b>css</b>

```css
.container {
  position: relative;
  display: flex;
  justify-content: center;
  margin-bottom: 80vh;
}

.container__slider {
  position: absolute;
  display: flex;
  justify-content: center;
  width: 80vw;
  height: 69vh;
  box-sizing: border-box;
  margin-top: 15px;
}

.js-container__slider__img {
  position: absolute;
  width: 80vw;
  height: 69vh;
  border-radius: 3px;
  object-fit: cover;
  box-shadow: 9px 9px 0 #bdccd4;

  transition: all 0.4s ease-in-out;
  cursor: pointer;
  z-index: 0;
  opacity: 0;
}

.slider_showing {
  z-index: 1;
  opacity: 1;
  transition: all 1s;
}
```

다른 개발을 하면서 css position을 이해하는 게 어려웠었는데 slide를 개발하면서 position을 전보다는 이해할 수 있었다.

👉 [CSS Position](https://developer.mozilla.org/ko/docs/Web/CSS/position)

<b>Javascript</b>

```javascript
const container__slider = document.querySelector('.js-container__slider');
const firstSlide = document.querySelector('.js-container__slider__img');

const SHOWING_CN = 'slider_showing';
const IMG_NUM = 4;
```

먼저 slide 틀과 slide 이미지들을 querySelector로 가져왔고, animation 역할을 할 slider_showing과 slide에 들어갈 사진 수를 변수로 만들어 주었다.

<b>Javascript</b>

```javascript
const handleSlideClick = () => {
  changeSlide();
};

const slideInit = () => {
  changeSlide();
  setInterval(changeSlide, 5900);

  // container__slider를 클릭했을 때 handleSlideClick 함수를 실행해라
  container__slider.addEventListener('click', handleSlideClick);
};

slideInit();
```

init 함수를 slideInit이라 지은 이유는 slide.js 제외한 다른 javascript가 연결된 상태에서 두 js 모두 init이라고 쓰면 js가 제대로 실행이 안된다.

그래서 나는 javascript를 할 때마다 js의 기능을 써주고 Init을 붙인다.

## setInterval

setInterval이란 일정한 시간 간격으로 작업을 수행하기 위해 사용하는 함수다.
나는 클릭 이외에도 시간이 지나면 슬라이드가 자동으로 넘어가도록 하기 위해 setInterval 함수를 이용했다.

<b>Javascript</b>

```javascript
const changeSlide = () => {
  const currentSlide = container__slider.querySelector(`.${SHOWING_CN}`);

  if (currentSlide !== null) {
    currentSlide.classList.remove(SHOWING_CN);
    const nextSlide = currentSlide.nextElementSibling;

    if (nextSlide.className !== 'blank') {
      nextSlide.classList.add(SHOWING_CN);
    } else {
      firstSlide.classList.add(SHOWING_CN);
    }
  } else {
    firstSlide.classList.add(SHOWING_CN);
  }
};
```

currentSlide 변수를 보면

```javascript
`.${SHOWING_CN}`;
```

이라는 특이한 코드가 보인다.

감싸져있는 것을 <b>백틱 (``)</b>이라고 하는데
백틱은 <b>문자열 표기법</b>이다.

따라서 ${} 사이에 변수나 연산 등을 삽입 후 백틱으로 감싸면 문자열로 자동 변환된다.

> 즉, 컨테이너 슬라이더 객체(DOM) 안에서 "slider_showing" 클래스를 가진 애를 currentSlide 변수에 넣는 것이다.

<b>nextElementSibling</b>
if문 안에 nextSlide 변수를 보면 nextElementSibling method가 있다,
nextElementSibling은 해당 요소 바로 다음 요소를 가져오는 역할을 한다.

👉 [Element.nextElementSibling](https://developer.mozilla.org/en-US/docs/Web/API/Element/nextElementSibling)

이를 통해 slide가 계속 돌아갈 수 있게 하였다.

## 결과

![](https://images.velog.io/images/seulhyi/post/7ee34702-2e48-4644-bd43-14b344a007d7/image.png)

![](https://images.velog.io/images/seulhyi/post/413026a3-5dbc-4da1-a3ca-8e0069a3b055/image.png)

정해진 시간이 지나거나 사용자가 클릭했을 때 slide가 넘어간다.
