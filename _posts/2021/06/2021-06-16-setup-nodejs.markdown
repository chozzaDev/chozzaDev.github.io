---
title:  "[Vue.js] Vue + Quasar + TypeScript"
date:   2021-06-16 08:04:00 +0900
categories: vue, typescript
---

만약 근무하는 회사가 서비스 회사라면 어디든지 백오피스가 존재할 것이다.

회사마다 백오피스를 허접하게 관리하는 곳도 있고, 멋지게 관리하는 곳도 있는데

결국 밖에서 보이는 서비스 만큼이나 중요한게 백오피스 되겠다.

요즘에 가장 비싼건 하드웨어나 소프트웨어가 아닌 바로 `인건비` 라고 생각하기 때문에

백오피스는 적어도 나의 기준에서는 다음과 같은 기준을 만족해야한다.

1. 실 사용자가 편하고 빠르게 이용할 수 있어야 한다.
2. 별도의 교육없이도 직관적으로 이해하고 바로 사용할 수 있어야 한다.
3. 개발속도가 빠른 Framework을 선정해야한다. (개발자 인건비가 제일 비싸다.)
4. CI/CD 구성이 용이해야 한다.

위 4가지가 필요한 이유는 결국 `돈` 때문이다. 4가지를 만족하면 할 수록 인건비는 감소한다.

나만 그렇게 느끼는지 모르겠지만 요즘에 최신기술만 따라가려하는데 정작 왜 필요한지 모르고 쓰거나

공부하시는 분들이 많은데 이런 기준으로 선정할 수도 있구나... 라고 생각해주시면 될 것 같다.

사설이 길었는데 결국 위의 이유로 화면구성은 Vue + Quasar + TypeScript 를 사용하기로 했다.

##NVM 설치

먼저 nvm(Node Version Manager)를 설치하는데 본인이 여러환경의 node 버전이 필요하다면 필수로 설치해야한다.

[공식 홈페이지](https://github.com/nvm-sh/nvm "공식홈페이지")

`아니더라도 어려운거 아니니까 나중을 위해서 설치하자..`
```shell
brew install nvm
```
nvm 을 설지하면 아래와 같은 메시지가 나온다. 따라해주면 되겠다.
```
You should create NVM's working directory if it doesn't exist:

  mkdir ~/.nvm

Add the following to ~/.zshrc or your desired shell
configuration file:

  export NVM_DIR="$HOME/.nvm"
  [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion

```

```shell
mkdir ~/.nvm
sudo vi ~/.zshrc
```
편집창에서 아래 내용을 넣어주면된다.

`편집창에서 나오는 내용으로 복사해서 넣어라... 설치할때마다 경로가 다를수 있다.`
```shell
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && . "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```

## Node.js 설치
[공식 홈페이지](https://nodejs.org/ko/ "공식홈페이지")

글 작성일 기준 홈페이지 안정적 버전 14.17.1

```shell
nvm install 14
```

생각보다 오래걸린다...

```shell
node --version
```

v14.17.1 을 보았다.

## Vue.js

[공식 홈페이지](https://kr.vuejs.org/v2/guide/index.html "공식홈페이지")

자세한 설명은 생략하겠다. 글작성 기준 대한민국에서 React or Vue 둘중 하나 쓴다고 말해도 과언이 아니며, Vue가 SI시장에서는 더 선호하는 편이다.

개인적으로 React와 Vue 둘다 가능하지만 React의 Jsx 보다는 Vue 의 template 방식이 더 좋다고 생각하기 때문에 Vue를 선정하였다.

## Quasar

[공식 홈페이지](https://quasar.dev/ "공식홈페이지")

Vue.js 를 사용하여 UI Framework 을 제공한다. SPA, SSR, PWA 등을 제공하고 정리가 잘되어 있고 굉장히 깔끔하다.

## quasar-typescript-admin-template

[공식 홈페이지](https://github.com/dirkhe1051931999/quasar-typescript-admin-template)

위에 설명한 기술을 사용하여 Admin Template 제공한다. 이미 되어 있는 것이 있는데 새로 만드는건 바보같은 일이다.

물론 만들어진 것이 썩 만족스럽지 않을 수 있지만 리소스 부족에 시달리는 스타트업은 선택의 여지가 없다.



