---
title: '비동기 어떻게 만들까?'
subtitle: '비동기 구현 방법에 대해 공유합니다.'
date: 2022-09-13
category: 'JavaScript'
---

본 게시물은 `비동기 구현 방법`에 대해 알아본 내용을 공유합니다.

## 비동기

비동기란 어떠한 요청을 보내면 그 요청이 끝날 때까지 기다리지 않고 다음 동작을 먼저 수행하는 것을 의미합니다.

더 자세한 내용은 이전 글 <a href="https://www.seulheehan.com/synchronous">'동기 비동기 파헤치기'</a>에서 보실 수 있습니다.

## Callback

Callback 함수란 다른 함수의 인자로써 사용되는 함수, 어떠한 이벤트에 의해 호출되는 함수를 뜻합니다.

```JavaScript
function checkTime(time, lunch, dinner){
    time <= 17 ? lunch() : dinner();
}

function lunchGreeting(){
    console.log("점심 맛있게 드세요!");
}

function dinnerGreeting() {
    console.log("저녁 맛있게 드세요!");
}

checkTime(13, lunchGreeting, dinnerGreeting);
```

예를 들어 위의 코드에서는 lunchGreeting 함수와 dinnerGreeting 함수가 Callback 함수입니다.

checkTime 함수가 먼저 호출되고 lunchGreeting 함수 또는 dinnerGreeting 함수가 나중에 호출되기 때문입니다.

Callback 함수를 어렵게 생각할 필요 없이 다양하게 쓰이는 표현 방식이라 생각하면 이해하기 쉬울 것 같습니다.

### 왜 Callback을 사용할까?

Callback 함수는 가독성이나 코드 재사용성 면에서 활용할 수 있기도 하며 JavaScript에서 비동기적 프로그래밍을 할 수 있기 때문입니다.

그러나 비동기 호출이 자주 일어나는 경우 `Callback 지옥`이 발생할 수 있습니다.

Callback 지옥이란 Callback 함수를 많이 사용해 코드의 들여쓰기 수준이 감당하기 힘들어질 정도로 깊어지는 현상을 뜻합니다.

```JavaScript
test1(function(value1){
    test2(function(value2){
        test3(function(value3){
            test4(function(value4){
                test5(function(value5){
                    test6(function(value6){
                        // ...
                    })
                })
            })
        })
    })
})
```

Callback 지옥은 위와 같이 가독성이 떨어지고 로직을 변경하기에 어려움이 있습니다.

이런 점을 `보완하여 비동기 처리를 할 수 있는 것이 Promise`입니다.

## Promise

Promise는 Callback 함수를 보완해 나온 비동기 처리에 활용되는 객체입니다. (ES6)

### Promise 사용법

```JavaScript
const test = new Promise((resolve, reject) => {
    // ...
})
```

`new Promise()`로 Promise 객체를 새로 만들고 첫 번째 인자로 resolve, 두 번째 인자로 reject를 받습니다.

여기서 resolve는 비동기가 성공했을 경우, reject는 비동기가 실패했을 경우를 뜻합니다.

이후 Promise가 끝나고 난 뒤 후속 작업을 할 때 then 메소드와 catch 메소드를 사용합니다.

- then 메소드

해당 Promise가 성공했을 때의 동작을 지정합니다.

- catch 메소드

해당 Promise가 실패했을 때의 동작을 지정합니다.

```JavaScript
const test = new Promise((resolve, reject) => {
    resolve()
});
test
  .then(() => {
    console.log("성공했어요!");
  })
  .catch(() => {
    console.log("실패했어요!");
  });
```

위의 코드는 바로 resolve가 호출되었기 때문에 실행 결과가 성공했어요! 라 나오고 해당 부분을 reject()로 바꾸면 실패했어요! 라고 나오게 됩니다.

요약하자면 `Promise를 생성하는 순간 비동기 작업이 시작`되고 비동기 작업을 `성공`으로 간주하고 싶을 땐 `resolve` 함수를 호출, `실패`라 간주하고 싶을 때는 `reject` 함수를 호출합니다.

해당 비동기 작업이 `성공`했을 경우 후속 작업을 지정할 때는 `then`, `실패`했을 경우 후속 작업은 `catch`로 지정할 수 있습니다.

### Promise의 3가지 상태

Promise를 사용할 때 꼭 알아야 하는 것은 `Promise의 상태`입니다. 같은 말로 `Promise의 처리 과정`이라고 할 수 있습니다.

Promise는 생성하고 종료될 때까지 3가지의 상태를 갖는데 아래와 같습니다.

- Pending (대기)

비동기 처리가 아직 완료되지 않은 상태를 뜻합니다.

Promise를 생성하면 Pending (대기) 상태가 됩니다.

즉 new Promise로 Promise가 생성되는 직후부터 resolve나 reject가 호출되기 전까지의 순간을 Pending 상태라 할 수 있습니다.

- Fulfilled (이행)

비동기 처리가 완료되어 Promise가 결괏값을 반환해준 상태를 뜻합니다.

다른 말로 완료된 상태라고도 합니다.

- Rejected (실패)

비동기 처리가 실패하거나 오류가 발생한 상태를 뜻합니다.

![promises](https://user-images.githubusercontent.com/63100352/190096805-1a837d8f-502e-48ee-8144-82c824df6673.png)

[이미지 출처](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

## Async Await

Async Await는 JavaScript 비동기 처리 패턴 중 최근에 나온 문법입니다. (ES8)

Async Await를 사용하면 더욱 직관적인 코드가 될 수 있습니다.

### Async Await 사용법

function 앞에 async 키워드를 붙여 선언하고 비동기로 처리되는 부분 앞에 await 키워드를 붙이면 됩니다.

```JavaScript
async function hi () {
  // ...
};

const hi = async () => {
  // ...
};
```

await 키워드는 `async 키워드가 있는 함수 내부에서만 사용`이 가능하며 비동기 함수가 리턴하는 `Promise로부터 결괏값을 반환`합니다.

```JavaScript
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  const result = await resolveAfter2Seconds();
  console.log(result);
}

asyncCall();
```

**ES2022** 추가된 스펙을 말씀드리자면

```JavaScript
(async function () {
  await test();
})();
```

기존에는 익명함수를 만들어 했어야 하는데 이제는 Top Level에서도 가능합니다.

```JavaScript
await test();
```

**예외 처리**

Async Await에서 예외를 처리할 때는 `try catch`를 사용합니다.

Promise에서 catch 메소드를 사용했던 것처럼 async에서는 catch{}를 사용합니다.

```JavaScript
async function test() {
    try{
      const response = await fetch('url');
        // ...
    } catch (error) {
        // ...
    }
}
```

이를 통해 다양한 오류까지 찾아낼 수 있습니다. 발견된 오류는 error 객체에 담기게 됩니다.

## 마무리

JavaScript의 비동기 처리에 사용되는 Callback, Promise, Async Await에 대해 알아봤습니다.

설명하는 과정에서 혹시나 잘못된 부분이 있을 시 피드백 부탁드립니다. 🙇🏻‍♂️

글 읽어주셔서 감사합니다!
