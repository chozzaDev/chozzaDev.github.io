---
title:  "[Tip] Spring Rest API Parameter Convert"
date:   2021-08-09 08:19:00 +0900
categories: tip, spring
---

누구나 마찬가지겠지만 남이 만든 프로젝트를 손본다는 것은 고통스러운 일이다. 하지만 일을 가려서 할 수 도 없는 일이기에
어쩔수 없이 해야할 때가 많은데 이번에는 Spring Rest API에 날짜에 대한 변경이였다. 이미 Client에서 서버로 `yyyyMMddHHmmss`
String 형태로 전송중이였고, 전송받은 데이터를 다른
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
