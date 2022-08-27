---
title: '[BOOKREST] 회원가입 Vanilla JS'
subtitle: '회원가입 개발기를 공유합니다.'
date: 2021-07-27
category: 'Project'
---

## 이용약관

전에는 항상 입력받는 폼만 만들었었는데 실제 서비스라 생각해보니 이용약관이 있는 게 더 좋을 것 같다는 생각이 들었다.

이용약관을 구글링하면 내용이 다 나와 있었다.
BOOKREST로 바꾸어 사용하였다.

<b>html</b>

```html
<div class="signupBoxTool__signupBox__terms__title">
  <h3>개인정보 수집 및 이용</h3>
</div>
<div class="signupBoxTool__signupBox__terms__summary">
  <dl>
    <dt>시행일자: 2021년 08월 14일</dt>
    <br />
    <dd>
      BOOKREST(이하 "회사" 또는 "BOOKREST"이라고 함)은 통신비밀보호법, 전기통신사업법, 정보통신망 이용촉진 및 정보보호
      등에 관한 법률 등 정보통신서비스제공자가 준수하여야 할 관련 법령상의 개인정보보호 규정을 준수하며, 관련 법령에
      의거한 개인정보취급방침을 정하여 이용자 권익 보호에 최선을 다하고 있습니다.<br /><br />

      본 개인정보취급방침은 다음과 같은 내용을 담고 있습니다.<br /><br />
    </dd>
  </dl>
</div>
```

<b>css</b>

```css
.signupBoxTool__signupBox__terms__summary {
  height: 150px;
  overflow: auto;
  padding: 7px;
  margin-bottom: 0;
}
```

html dl태그는 설명 목록을 나타낸다.
dl은 dt로 표기한 용어와 dd 요소로 표기한 설명 그룹의 목록을 감싸서 설명 목록을 생성해 이용약관을 쓸 때 이를 이용하였다.

css를 이용해 틀을 잡아주어 안에서 스크롤 되게 만들었다.

![](https://images.velog.io/images/seulhyi/post/d7edf614-0c8d-49df-9a27-8cbe586039e5/image.png)

이렇게 완성이 되었다.

## 이용약관 JavaScript

```javascript
const termsCheckbox = event => {
  event.preventDefault();
  const agreement1 = document.querySelector('.js-agreement1');
  const agreement2 = document.querySelector('.js-agreement2');

  if (!agreement1.checked) {
    window.alert('이용약관 이용동의는 필수입니다.');
  } else if (!agreement2.checked) {
    window.alert('개인정보의 수집 및 이용동의는 필수입니다.');
  } else {
    signupAnimate();
  }
};
```

동의, 동의 안 함 버튼을 두었고 먼저, 첫 번째 이용약관 (agreement1)을 체크 안 했다면 alert로 경고 메시지가 뜨도록 설정하였고 두 번째 이용약관(agreement2)도 마찬가지로 alert를 설정하였다.
![](https://images.velog.io/images/seulhyi/post/c261afa5-247d-4456-b320-73becc01e908/image.png)

<b>Javascript</b>

```javascript
const onNoregisterClick = event => {
  event.preventDefault();
  if (window.confirm('회원가입을 취소하고 BOOKREST 첫 화면으로 돌아가시겠습니까?')) {
    location.replace('/');
  }
};
```

동의 안 함 버튼을 눌렀을 시에는 회원가입을 못 하도록 설정하였다.
replace() 메소드는 Location현재 리소스를 제공된 URL의 리소스로 바꾸는 기능을 한다.

replace()는 현재 페이지를 새로운 페이지로 덮어씌우기 때문에 이전 페이지로 이동이 불가능하다.

![](https://images.velog.io/images/seulhyi/post/2c9214f3-6549-452e-9667-9a114f20a39c/image.png)

**이렇게 해서 모든 이용약관을 동의 후 동의 버튼을 누르면 정보입력 폼이 나오게 된다.**

---

## 정보입력

회원가입에서 받을 정보

1. 이름
2. 학부 / 전공
3. 학번
4. 이메일
5. 비밀번호
6. 전화번호

> 그냥 입력폼만 있는 건 BOOKREST랑 안어울려 .. 양식을 두자 !

## 정보입력 양식

1. 이름이 2자 이상
2. 학번은 9자리 (우리 학교 기준)
3. 이메일 정규표현식에 맞아야 함
4. 비밀번호는 6자리 이상
5. BOOKREST 이용 규정에 동의하는 checkbox에 체크해야 함

### 그 외

학부 / 전공은 select 태그로 총 네 개의 학부 중 하나를 선택하도록 (우리 학교 기준)
전화번호는 그냥 입력받을지 막대기(-) 할지 아직 고민중이다.

<b>html</b>

```html
<div class="signupBoxTool__signupBox__form-control">
  <div class="signupBoxTool__signupBox__form-control__title">
    <span>이름</span>
  </div>
  <input type="text" class="name input" placeholder="Enter username" />
  <small>Error message</small>
</div>
```

input 태그로 입력을 받는 곳을 두고 아래에 error message가 들어갈 곳을 만들어 준다.

<b>css</b>

```css
.signupBoxTool__signupBox__form-control small {
  font-size: 11px;
  font-weight: 500;
  bottom: 0;
  left: 0;
  visibility: hidden;
}

.signupBoxTool__signupBox__form-control.error small {
  visibility: visible;
}
```

visible - 요소가 보이고, hidden - 요소가 숨겨진다 (그려지지 않음).
css를 이렇게 설정해두고 Javascript로 코드만 짜면 된다.

<b>Javascript</b>

```javascript
const loadName = () => {
  if (name.value.length === 0) {
    errorRed(name, `사용자 이름은 2자 이상이어야 합니다`);
  } else if (name.value.length >= 2) {
    successLight(name);
  } else {
    errorRed(name, `사용자 이름은 2자 이상이어야 합니다`);
  }
};

const signInit = () => {
  name.addEventListener('input', loadName);
  email.addEventListener('input', checkEmail);
  password.addEventListener('input', checkPassword);
  studentID.addEventListener('input', checkstudentID);
  checkbox.addEventListener('change', handleCheckboxForm);

  signupForm.addEventListener('submit', e => {
    e.preventDefault();
    checkPassword(password, 1, 6);
    loadName();
    checkEmail(email);
    checkstudentID(studentID);
    handleCheckboxForm();
  });
};

signInit();
```

~~양식이 많아 이름만 기록해야겠다..~~
먼저 등록 버튼을 누를시 (submit) 아래 함수들이 실행되게 설정하였고 또한 input 창에 내용을 적을 때 위와 같은 함수가 실행되도록 하였다.

loadName 함수는 사용자가 입력한 길이가 0일 경우 아래와 같은 error메시지가 뜨도록 하였다.
``은 "백틱(backtick)" 이라고 하는데 자세한 내용은 [여기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)를 참고하면 좋을 것 같다.

사용자가 입력한 길이가 2 이상일 경우 successLight라는 함수를 실행하는데 successLight 함수는 아래와 같이 error를 classList에서 빼주는 기능이다. 즉 양식에 맞아 에러 메시지가 안 뜨도록 한 것이다.

<b>Javascript</b>

```javascript
const successLight = input => {
  const formControl = input.parentElement;
  formControl.classList.remove('error');
};
```

```javascript
const checkEmail = () => {
  const emailRule =
    /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
  if (emailRule.test(email.value.trim())) {
    successLight(email);
  } else {
    errorRed(email, `이메일이 유효하지 않습니다`);
  }
};
```

이메일 정규표현식은 구글링해보면 쉽게 나온다.

---

## 결과

에러 메시지가 안 떴을 때

![](https://images.velog.io/images/seulhyi/post/bc35258d-baf8-4331-9c32-ee99ba1df455/image.png)

아무것도 안 쓰고 등록 버튼을 눌렀을 때

![](https://images.velog.io/images/seulhyi/post/efafd5e3-5e93-4cd2-a5cb-a08dc4327f21/image.png)

실행해보면 input창에 정보양식에 맞게 입력하면 해당 오류 메시지가 사라진다.
