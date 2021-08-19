---
title:  "[Gatsby] Gatsby + Typescript로 Blog 만들기(1)"
date:   2021-08-09 08:19:00 +0900
categories: gatsby
---

Github Pages 를 사용하여 시범적으로 한달간 사용해본 결과 Jekyll을 통해 손쉽게 블로그를 만들수 있어 좋았다.
하지만 커스텀하기 위해 또 공부를 해야하고 Jekyll은 현업에서는 사용하지 않아 굳이 시간을 들여 배우고 싶다는 생각이 들지는 않았다.
위와 같은 이유로 찾다보니 Gatsby라는 녀석을 알게되었고, 생태계도 괜찮고 커스텀할 때 React와 Typescript를 사용할 수 있다는 점도 좋았다.
주로 Vuejs + Typescript를 사용하던 나에게 React를 접해볼 수 있는 기회도 되고, 매번 쓰던 기술에 요즘 제일 핫한 React만 추가로 공부하면 되니
일석이조인 샘이다. 이제 시작해보자.

##Gatsby

먼저 gatsby-cli가 필요하다. 아래 링크를 참조하여 설치하자.

[gatsby-cli](https://www.gatsbyjs.com/docs/reference/gatsby-cli#how-to-use-gatsby-cli)

```shell
npm install -g gatsby-cli
```
설치되었다면 아래 명령어를 통해 버전을 확인할 수 있다.
```shell
gatsby --version
```

starter 를 통해 간단하게 typescript를 사용하는 기본 프로젝트를 생성할 수 있다.

google 검색에서 제일 상단에 나오는 starter는 m1 맥북에서 오류가 발생하여 다른 starter를 찾아서 사용했다.

```shell
npx gatsby new starter-ts https://github.com/jpedroschmitz/gatsby-starter-ts
```

설치가 완료되면 해당 폴더로 진입하여 아래 명령을 수행하면 서버가 구동된다.
```shell
gatsby develop
```
