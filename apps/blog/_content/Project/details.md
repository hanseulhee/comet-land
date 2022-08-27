---
title: '[BOOKREST] <details>'
subtitle: 'details 태그에 관해 공유합니다.'
date: 2021-07-27
category: 'Project'
---

![캡처dfdf](https://user-images.githubusercontent.com/63100352/175520730-91cded30-dcea-4fee-891d-1b7e930b26e1.png)

몇 주 전에 알게 된 html의 새로운 태그가 있다.

<b>바로 details 태그 !!</b>

details 태그는 "열림" 상태일 때만 내부 정보를 보여주는 정보 공개 위젯을 생성한다.

> 이게 무슨 일인가 ..🙄 이런 기능은 Javascripts로 구현하는 줄만 알았는데 html에 태그를 써주기만 하면 된다.

이러한 details 요소의 콘텐츠는 open 속성이 설정되기 전까지는 화면에 보이지 않는다.

summary 요소는 details 요소에서 화면에 보일 제목을 명시할 때 사용한다.
이 summary를 마우스로 클릭함으로써 details 요소를 보이도록 할 수도 있고 숨길 수도 있다. (ex: toggle)

## 개발

BOOKREST에 문의하기(inquiry) 페이지를 개발해야 하는데 어떻게 디자인할지 고민이었다.

이때 전에 details 태그를 본 게 기억나 이번에 적용해보기로 했다.

<b>자주 묻는 질문이라는 제목 아래에 details 태그를 사용했다.</b>

<b>html</b>

```html
<details>
  <summary>한 사람당 책 몇 권까지 대여 가능한가요?</summary>
  <div class="details__content">5권까지 대여 가능합니다.</div>
</details>
```

details 태그 안에 summary 태그를 넣어 제목을 만들어주고 그 아래에 답변을 적었다.
css를 적용하기 위해 답변에 class를 만들어 줬다.

<b>css</b>

```css
details[open] ~ \* {
  animation: sweep 0.5s ease-in-out;
}

@keyframes sweep {
  from {
    opacity: 0;
    margin-top: -10px;
  }
  to {
    opacity: 1;
    margin-top: 0;
  }
}
```

animation을 이용해 details 태그가 open되었을 때 효과를 넣어주었다.

## 결과

<b>open 전</b>
![images_seulhyi_post_c76d2deb-33a9-4181-a470-19706db2c45f_image](https://user-images.githubusercontent.com/63100352/175520766-e9b53f27-a53a-4b43-a9b0-dd0bb89a3547.png)

<b>open 후</b>
![images_seulhyi_post_56c71324-317c-42d2-9e2d-68e03ce55058_image](https://user-images.githubusercontent.com/63100352/175520837-95469ade-8103-49eb-98dc-a6179e4d4df3.png)
summary에 적은 내용이 제목으로 들어갔고 open되었을 때 summary 태그 아래에 적은 내용이 나온다.
