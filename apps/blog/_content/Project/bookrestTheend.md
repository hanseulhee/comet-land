---
title: '[BOOKREST] 마치며'
subtitle: '프로젝트를 마치고 배운 점을 작성하며 회고를 마칩니다.'
date: 2021-08-12
category: 'Project'
---

8월 13일 해커톤 제출 완료, BOOKREST의 개발이 끝이 났다. 👏🏻👏🏻👏🏻

작년에 멋쟁이 사자처럼 8기 아기사자로 들어와 이번에 9기 운영진으로서 팀 프로젝트를 진행하였다.
BOOKREST를 통해 정말 많이 배웠고 나에게 뜻깊은 시간이었다.

나름 방학 동안 많이 공부했다고 생각했는데 실전은 달랐다.
이번 BOOKREST 개발을 하면서 내가 배운 점을 정리해 놓으려 한다.

## 배운 점

### 회의

BOOKREST 회의를 하면 한 명이 서기로 적고 트렐로에 정리하는 식이었는데 시간이 지나고부터 더 많은 회의 주제들이 나오고 공유할 정보들을 트렐로에 적는 게 여러 면에서 불편했다.

그래서 우리는 NOTION에서 회의 내용을 정리했다. NOTION은 캘린더, 보드뷰와 같이 편리한 기능들이 많이 내장되어 있고 무엇보다 개발이나 회의에 관한 내용을 보기 쉽게 정리할 수 있다.

![](https://images.velog.io/images/seulhyi/post/08c02749-f231-41db-b06d-49deead5acba/image.png)

팀원이 할 일이나 개발사항을 적어놓으면 들어가서 피드백을 적어놓고 얘기할 수 있어 좋았던 것 같다.
![](https://images.velog.io/images/seulhyi/post/1c59a502-73ec-49c8-9418-70d8d035571b/image.png)

### 협업

협업에서 가장 중요한 부분은 **소통**이라고 생각한다.
Frontend와 Backend으로 나누어도 서로서로 소통이 제일 중요한 것 같다.

Backend에서 기능을 만들어도 Frontend에서 보여주는 페이지를 만들지 않고 나중에 얘기하게 된다면 수정할 것들이 더 많아지게 된다. BOOKREST 개발하기 전에 많이 회의하고 디자인, db 등 다 정했다고 생각했는데 막상 개발을 시작하니 변경되는 사항이 많았다.
BOOKREST를 개발하면서 사소한 것도 얘기하고 기록하는 게 중요하다고 느꼈다.

### Frontend

나는 Frontend를 맡았다. CSS BEM방식을 지키려고 했고 필요한 코드만 쓰려고 노력했다.

개발하면서 가장 힘들었던 부분은 디자인이었다. scroll 감지 등 javascript도 처음 해보는 것들도 많았지만 디자인을 생각하고 또 생각했던 것 같다. Figma로 팀원들과 디자인 구성을 했지만 직접 웹에 디자인해보니 생각과 다른 점들이 많았다 ..
실제로 사용자에게 보여지는 웹이기에 크기, 색깔, 구성 등 정말 많이 고민하고 수정했던 것 같다.
재밌었지만 디자인에 대해 내가 더 알았다면 더 좋은 페이지를 만들 수 있지 않았을까라는 아쉬움이 있다.

나중에는 [Semantic Web](https://www.w3.org/standards/semanticweb/) 구성을 신경 쓰면서 개발 하고 싶다. div가 더 좋은 코드라고 생각했는데 공부를 하다 보니 Semantic Web 구성이 더 의미 있는 코드라는 걸 알게 되었다.

### Backend

나는 Frontend였지만 Backend에서 배운 점도 많다.

로그인, 회원가입, CRUD 등등 Frontend와 어떻게 연결이 되는지 어떤 식으로 짜야 되는지 나도 많이 배울 수 있었고 Backend에 대해 호기심도 많이 느꼈다.

~~근데 나는 Frontend가 더 잘 맞는 것 같다 ..🤫~~

### 오류

개발을 하면서 많은 오류를 접했다.
그중에서 가장 기억에 남는 오류는 버전 오류였다.

Backend를 맡은 팀원 중 한 분이 Mac이고 Frontend는 모두 Window였다.
회원가입 기능을 Frontend와 Backend merge하는 과정에서 기능이 실행이 되지 않았다. 계속해보던 중 Mac에서는 기능이 되고 Window에서는 기능이 작동하지 않는다는 걸 알게 되었다. 🤯
알고 보니 Mac의 Python버전과 Window의 <b>Python버전</b>이 달라 Window은 실행이 안 되고 Mac은 실행이 잘됐던 거였다.

그래서 winvenv를 따로 만들어 Mac 가상환경과 3.9.6 버전으로 통일했더니 기능이 잘 작동했다.
개발하기 전에 버전 얘기를 하는 걸 생각을 못 하고 있었는데 이번 기회에 많이 배울 수 있었다.

### Git

전에는 git에 대해 자세히 알지 못했다.
개인 프로젝트를 주로 해서 git add, commit , push만 하고 다른 git 명령어들은 잘 몰랐다.

-브랜치 생성하기
git branch 브랜치명

-git 2.23.0 버전 이후
checkout이 아래 두 가지로 분리되었다.
switch: 브랜치 변경
restore: 변경사항 복원

-브랜치 이동하기
git switch 브랜치명

-브랜치 생성과 동시에 이동하기
git switch -c 브랜치명

-수정한 파일 되돌리기
git restore 파일명

~~git checkout 브랜치명
git checkout -b 브랜치명~~

-브랜치 확인하기
git branch

-클론 받은 곳에서 추가적으로 다운로드
git pull origin 브랜치명

-커밋한 내용을 업로드
git push origin 브랜치명

-브랜치 합치기
git merge 브랜치명

-remote 갱신
git remote update

-remote 브랜치 가져오기
git checkout -t origin/원격에 있는 브랜치 명

-migrate 초기화
find . -path "_/migrations/_.py" -not -name "**init**.py" -delete
find . -path "_/migrations/_.pyc" -delete

이번 BOOKREST를 통해 git이랑 정말 많이 친해졌다. 😋

### Pull Request

BOOKREST는 각자 브랜치를 파서 merge 하는 방식으로 협업을 했었는데 협업이 용이한 [Pull Request](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)로 협업을 해보고 싶다. 더 공부해서 사람들한테 공유해야겠다.

### 배포

👉🏻👉🏻 [BOOKREST](https://sharebookrest.herokuapp.com/)

### 해커톤 BEST 10 수상!

21.08.20
상상도 못했는데 BOOKREST가 BEST 10에 들었다.
심사위원분들 앞에서 BOOKREST를 보여줄 수 있었고 피드백 받으면서 부족한 점을 알 수 있었다. 정말 뜻 깊은 경험이었다.😭

![](https://images.velog.io/images/seulhyi/post/5a5b7f91-0b73-4103-a781-d04d4c45bee9/KakaoTalk_20210822_002653863.jpg)

---

## 느낀 점

BOOKREST를 통해 정말 많이 배웠고 많은 도움이 됐다.
나의 멋쟁이 사자처럼 중앙 해커톤이 BOOKREST로 마칠 수 있어서 더 의미있었고 재밌었다 !!

![](https://images.velog.io/images/seulhyi/post/dea0c7f0-5f2f-4d30-9884-9bbd39e8e237/KakaoTalk_20210702_210407306_05.jpg)

**BOOKREST 최고 !!!!**
🦁👋🏻👋🏻👋🏻
