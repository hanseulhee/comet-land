---
title: 'vscode-styled-components 설치 후 auto complete 안되는 문제'
subtitle: ''
date: 2022-02-06
category: 'React'
---

![vscode-styled-components_auto_complete_적용안됨](https://user-images.githubusercontent.com/63100352/175525024-4987c0d9-355d-4580-8b08-350ebda73cca.png)

styled-component 사용 중 css 코드 작성 시 자동완성이 되지 않아 자동완성 기능을 해주는 <b>vscode-styled-components</b>를 설치하고자 하였다.

![](https://images.velog.io/images/seulhyi/post/ca11870e-8e17-49b5-a419-987787838f1a/image.png)

설치 후 css코드를 작성해 보았는데 자동완성 기능이 작동하지 않았다.
분명 이것만 설치하면 되는 건데 ..

다시 설치도 해보고 vscode도 지웠다가 설치해보았지만 여전히 문제는 해결되지 않았다.

나와 비슷한 문제를 겪고 있을 사람들을 위해 글을 쓰게 되었다.

## 해결

현재(2022.02.06) vscode의 최신 버전은 1.64.0이다. 내 vscode 버전 또한 1.64.0이었는데 [IntelliSense not working after updating vscode to 1.64](https://github.com/styled-components/vscode-styled-components/issues/354)를 보면 나와 같은 버전인 분도 자동완성 기능이 작동하지 않는다는 걸 볼 수 있었다.

vscode 버전을 <b>1.63.2</b>로 다시 설치하니 vscode-styled-components가 작동하였다.

[download in this link](https://code.visualstudio.com/updates/v1_63)
