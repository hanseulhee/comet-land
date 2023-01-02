---
title: 'Github Actions 파헤치기'
subtitle: 'Github Actions에 대해 공유합니다.'
date: 2022-12-02
category: 'Frontend'
---

본 게시물은 `Github Actions`에 대해 알아본 내용을 공유합니다.

## Github Actions이란?

[공식문서](https://docs.github.com/en/actions)에 따르면 Github Actions는 아래를 의미합니다.

> GitHub Actions는 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 지속적인 통합 및 지속적인 배포(CI/CD) 플랫폼입니다. 리포지토리에 대한 모든 풀 요청을 빌드 및 테스트하는 워크플로를 생성하거나 병합된 풀 요청을 프로덕션으로 배포할 수 있습니다.

Github Actions이란 2018년도에 만들어진 Github 저장소를 기반으로 소프트웨어 개발 Workflow를 자동화 할 수 있는 도구입니다.

Github 내부에서 프로젝트를 빌드, 테스트, 릴리즈 또는 배포를 지원하는 기능으로서 `Github에서 제공하는 CI/CD 도구`라고 생각하면 됩니다.

Github Actions는 repository에서 어떠한 이벤트가 발생할 때 workflow를 실행할 수 있도록 해주는데 그와 관련한 여섯 가지 키워드를 아래에서 보실 수 있습니다.

## Github Actions 주요개념

Github Actions는 크게 이 여섯 가지만 알면 됩니다.

- Workflow

workflow란 프로젝트를 빌드, 테스트, 패키지, 릴리즈 또는 배포하기 위한 `전체적인 프로세스`입니다.

자신만의 동작을 정의한 workflow file을 만들어 전달하면 Github Acrions가 실행됩니다.

workflow 파일은 yml 확장자로 작성되고 .github/workflows 폴더 아래에 저장됩니다.

- Event

event는 `어떠한 이벤트가 발생했을 때` 자동화를 시켜줘라라는 의미입니다. 예를 들어 main 브랜치로 merge를 할 때 혹은 push를 할 때와 같이 언제 자동화를 발생시킬 건지를 event 라고 합니다.

즉, workflow를 실행하는 특정 활동이며 workflow는 event 기반으로 작동합니다.

- Job

job은 `수행이 될 작업`에 대해서 정의할 수 있습니다.

workflow 안에는 하나 혹은 다수의 job으로 구성됩니다.

다른 job에 의존 관계를 가질 수 있고 독립적으로 병렬 실행도 가능합니다.

지금까지의 내용을 정리해 보면

> `배고프다 라는 event`가 발생했으면 요리할 레시피를 보게 되는데 그 `레시피가 workflow`입니다. 레시피 안에는 면 삶기, 소스 만들기와 같은 작업들이 있는데 그 `하나의 작업 단위를 job`이라 부릅니다.

- Step

앞에서 말한 job 안에는 step으로 구성됩니다. step은 `해당 작업이 어떤 순서대로 진행`되어야 하는지를 명시합니다.

Task 들의 집합으로 커맨드를 날리거나 action을 실행할 수 있습니다.

- Action

action은 job 안에서 `수행이 되는 행동`을 의미합니다.

action을 작성하는 방법에는 두 가지가 있는데 본인이 직접 작성하는 방식과 이미 만들어진 걸 사용할 수 있습니다.

이미 만들어진 걸 사용하기 위해선 [action marketplace](https://github.com/marketplace?type=actions)을 보시면 됩니다. Github에서 공식 인증된 action들이 많은데 이렇게 공개적으로 오픈된 action들을 보고 자신의 프로젝트에 필요한 걸 갖다가 쓰시면 됩니다.

- Runner

Gihub Action Runner는 Workflow를 실행하는 서버입니다. 각각의 runner는 한 번에 하나의 job만 실행할 수 있습니다. `각각의 job들은 개별적인 독립적인 각각의 runner라는 컨테이너에서 실행`이 된다고 보시면 됩니다.

## 하는 법

먼저 github actions은

```
.github/workflows/~.yml
```

의 구조를 갖추어야 합니다.

프로젝트 최상단에 .github 폴더를 만들고 그 안에 workflows라는 폴더를 만들어야 하고 확장자는 .yml 을 해야 한다는 것을 알고 계시면 됩니다.

![스크린샷 2022-12-18 오후 3 45 42](https://user-images.githubusercontent.com/63100352/209947883-f1b38ec4-a661-479a-b6cd-ffcc87dc8a9c.png)

`name`을 통해 workflow의 이름을 지을 수 있습니다. 하나만 존재하는 것이 아닌 여러 개의 workflow가 있을 수 있기에 이름으로 구분할 수 있습니다.

다음으로 `on`을 통해 workflow가 언제 실행돼야 할지 명시할 수 있습니다. 앞에서 설명한 event를 on으로 표현할 수 있습니다.

![스크린샷 2022-12-18 오후 3 45 42 (2)](https://user-images.githubusercontent.com/63100352/209947958-4fd5b708-63c0-42ff-9142-607f84a7115a.png)

workflow는 하나 혹은 다수의 job들로 구성되기 때문에 `jobs`로 수행이 될 작업들을 정의합니다.

`runs-on`을 이용해 어떤 운영체제에서 실행이 될 건지 지정합니다.

`step`으로 job의 순서를 정의할 수 있습니다. name으로 step의 이름을 적고 `uses` 키워드를 이용해 `action`을 명시합니다. 이미 만들어진 action을 사용할 때에는 uses 키워드로 어떤 action을 사용할 것인 지 지정합니다.

직접 만든 action을 사용하기 위해선 [공식 문서](https://docs.github.com/ko/actions)를 참고해주시면 됩니다.

## 작동해보기

잘 작동되는지 확인을 하기 위해서는 자신이 작성한 event를 발생시키고 레포의 Actions에서 workflow가 잘 작동하는 지 확인할 수 있습니다.

<img width="952" alt="스크린샷 2022-12-29 오후 8 28 13" src="https://user-images.githubusercontent.com/63100352/209944851-d84b7d98-e5d2-4006-8c3a-ac3fedcf2b2e.png">

만약 문제가 생기면 x가 뜨게 되고 메일로 실패했다고 연락이 옵니다.

> 재밌죵 ? 🤭

## 마무리

GDSC라는 동아리의 코어 멤버로 활동하고 있는데 얼마 전 CI/CD를 주제로 세션을 진행하였습니다. [해당 링크](https://github.com/GDSC-SKHU/github-actions-practice)에서 github actions의 기초적인 실습을 진행한 걸 보실 수 있습니다.

설명하는 과정에서 혹시나 잘못된 부분이 있을 시 피드백 부탁드립니다.

글 읽어주셔서 감사합니다! 🙂
