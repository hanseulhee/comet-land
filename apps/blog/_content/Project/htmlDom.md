---
title: '[BOOKREST] HTML DOM Change Animation'
subtitle: 'HTML DOM Change Animation에 관해 공유합니다.'
date: 2021-08-04
category: 'Project'
---

![](https://images.velog.io/images/seulhyi/post/256e4cca-3388-4170-96cc-67e5e6d91e52/image.png)

BOOKREST Notice 페이지 (서비스 소개, 규정, 오시는 길, 문의하기 페이지가 모여있는 곳)을 만들던 도중

> 새로고침이 아닌 Animation으로 페이지를 나타내자!

라는 생각이 들었다.

animation으로 페이지 이동을 하려면 html에서는 animation을 줄 페이지들을 한 템플릿 안에서 만들어야 한다.

## 개발

<b>html</b>

```html
<div class="noticeTool__category">
  <div class="noticeTool__category__title">BOOKREST 이용안내</div>
  <div class="noticeTool__category__link">
    <a class="js-introduceA js-noticeTool__category__link">BOOKREST란</a>
    <a class="js-ruleA js-noticeTool__category__link">규정</a>
    <a class="js-faqA js-noticeTool__category__link">자주 묻는 질문</a>
    <a class="js-bookrestMapA js-noticeTool__category__link">오시는 길</a>
  </div>
</div>
```

먼저, a링크를 달아서 내용 폼에 관련한 각각의 제목을 적어준다.
자세한 개발 사항은 a링크 BOOKREST란? , 규정 두 가지로 얘기하도록 하겠다.

class 명은 BEM방식으로 지으려고 노력했다.
👉🏻 [CSS BEM 참고](https://nykim.work/15)

<b>a class="js-introduceA"를 누르면 나오는 폼</b>

```HTML
 <div class="noticeTool__summaryTool">
   <!-- js-introduce 여기가 포인트 -->
      <div class="noticeTool__summaryTool__box js-introduce noticeShowing">
        <div class="noticeTool__summaryTool__box__title">
          <h1>BOOKREST란?</h1>
        </div>
        <div class="noticeTool__summaryTool__box__summary">
          BOOKREST는 전공 서적을 대여해주는 서비스입니다. 학기마다 전공 책을
          새로 구매하시나요? 구매하셨다면 가격이 부담스럽지 않으셨나요?
          머라머라머라
        </div>
      </div>
    </div>
```

<b>a class="js-ruleA" 를 누르면 나오는 폼</b>

```HTML
    <div class="noticeTool__summaryTool">
      <!-- js-rule 여기가 포인트 -->
      <div class="noticeTool__summaryTool__box js-rule">
        <div class="noticeTool__summaryTool__box__title">
          <h1>Rule</h1>
        </div>
        <div class="noticeTool__summaryTool__box__summary">
          <b>Book</b>
          책의 종류와 재고는 BOOKREST 사이트에서 확인해주시면 됩니다. 직접
          오셔서 대여하려 하시면 이미 예약된 책들도 있어 어려우실 수 있습니다.
          BOOKREST 사이트에서 미리 예약하시면 더 빠르고 쉽게 대여하실 수
          있습니다.
          머라머라머라
        </div>
      </div>
    </div>
```

위의 두 폼 모두 한 템플릿에서 쓰인 코드다.
class명, css는 모두 똑같고 BEM방식으로 js-introduce, js-rule이라 써준다.

---

<b>이제 Javascript에서 각각의 a링크를 클릭하면 그에 맞는 폼이 나오도록 만들면 된다.</b>

<b>Javascript</b>

```javascript
// 각각 내용이 있는 폼
const introduce = document.querySelector('.js-introduce');
const rule = document.querySelector('.js-rule');

// a링크
const introduceA = document.querySelector('.js-introduceA');
const ruleA = document.querySelector('.js-ruleA');

// css 애니메이션
const NOTICESHOWING_CN = 'noticeShowing';
```

각각의 변수를 선언해준다. noticeShowing에 관한 코드는 아래 있다.

<b>css</b>

```css
.noticeShowing {
  opacity: 1;
  z-index: 10;
  transform: scale(1);
}
```

noticeShowing은 introduce폼과 rule폼을 보였다 사라졌다 하는 <b>animation을 주는 역할</b>을 한다.

근데 모든 폼이 opacity가 0이면 아무것도 안 보이니 <b>introduce폼이 기본으로 설정</b>해두었다.
따라서 위에 html을 보면 introduce폼 class에 noticeShowing이 적어져 있다.

<b>Javascript</b>

```javascript
const elementList = [introduce, rule];
const elementLinkList = [introduceA, ruleA];
let currentIndex = 0;
let beforeIndex = 0;
```

elementList 변수는 introduce와 rule 객체(DOM)가 있는 배열이다.
elementLinkList는 각각의 DOM으로 갈 수 있는 링크 태그로 이루어진 배열이다.
currentIndex는 현재 보이는 배열의 인덱스, beforeIndex는 전에 보였던 배열의 인덱스다.

<b>Javascript</b>

```javascript
const noticeInit = () => {
  elementLinkList.map((link, index) => {
    link.addEventListener('click', () => {
      addClassNameToCurrentElement(index);
    });
  });
};

noticeInit();
```

noticeInit 함수는 제일 먼저 실행되며 elementLinkList 각 요소의 EventListener를 부착한다.
이때 [map 메소드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)의 인덱스 값을 addClassNameToCurrentElement의 인자로 사용한다.

<b>Javascript</b>

```javascript
const addClassNameToCurrentElement = index => {
  elementList[beforeIndex].classList.remove(NOTICESHOWING_CN);
  elementList[index].classList.add(NOTICESHOWING_CN);
  beforeIndex = index;
};
```

link 요소가 click되면 addClassNameToCurrentElement 함수에 index 값을 인자로 실행한다.

elementList 배열의 beforeIndex번째 객체의 classList에 NOTICESHOWING_CN을 지워주고, elementList 배열의 index번째 객체의 classList에 NOTICESHOWING_CN을 더해준다.

`beforeIndex = index;` beforeIndex에 인덱스 값을 할당해 주었다.
click 되면 beforeIndex번째의 NOTICESHOWING_CN를 지우면 전에 있는 건 안보이고 현재 누른 것만 보이게 되기 때문에 다음에 눌렀을 때를 위해서 beforeIndex 변수에 지금 누른 값인 index를 할당하였다.

## 결과

![](https://images.velog.io/images/seulhyi/post/256e4cca-3388-4170-96cc-67e5e6d91e52/image.png)

![](https://images.velog.io/images/seulhyi/post/6992cd5b-ef54-46c9-95cf-df0061c97cf4/image.png)

url을 보면 같은 한 페이지임을 알 수 있다.
새로고침이 아닌 오른쪽 틀이 animation으로 나오게 된다.

## refactoring 전 ..

```javascript
const noticeAnimateIntroduce = () => {
  introduce.classList.add(NOTICESHOWING_CN);
  rule.classList.remove(NOTICESHOWING_CN);
  bookrestMap.classList.remove(NOTICESHOWING_CN);
  inquiry.classList.remove(NOTICESHOWING_CN);
};

const noticeAnimateRule = () => {
  rule.classList.add(NOTICESHOWING_CN);
  introduce.classList.remove(NOTICESHOWING_CN);
  bookrestMap.classList.remove(NOTICESHOWING_CN);
  inquiry.classList.remove(NOTICESHOWING_CN);
};

const noticeInit = () => {
  introduceA.addEventListener('click', noticeAnimateIntroduce);
  ruleA.addEventListener('click', noticeAnimateRule);
  bookrestMapA.addEventListener('click', noticeAnimateBookrestMap);
  inquiryA.addEventListener('click', noticeAnimateInquiry);
};

noticeInit();
```

refactoring 전에는 배열이랑 인덱스를 사용하지 않고 각 요소마다 함수를 만들었다.
하면서도 비효율적이라고 느껴졌다.

만약 더 많은 페이지가 추가된다고 하면 함수를 몇십 개 더 만들어야 하는 거다.
그래서 배열과 인덱스를 활용하였다.

<b>refactoring 후 elementList와 elementLinkList의 배열에 넣어주기만 하면 된다.</b>

```javascript
const elementList = [introduce, rule];
```

```javascript
const elementLinkList = [introduceA, ruleA];
```
