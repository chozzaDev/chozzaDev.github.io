---
title:  "M1 Mac Python 개발 환경 설정"
date:   2021-06-10 08:00:12 +0900
categories: python
---

Fast API를 사용하여 회사에서 서비스하는 API서버를 구축하려 합니다.

지금까지 14년간 Java를 써온 나에게는 새로운 도전이며 즐거움 될 것 같아요.

지금 쓰는 장비가 Macbook Pro 13 M1 이기에 M1 기준으로 진행합니다.

## Python 설치에 앞서...
### Homebrew
[공식 홈페이지](https://brew.sh/index_ko "Homebrew 공식홈페이지")

![버전확인](/assets/images/2021/06/20210610_01.png "버전확인 결과")

설치를 하지 않았다면 설치 스크립트
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### pyenv

파이썬에는 무수히 많은 버전이 있고, 그에 상응하는 라이브러리들이 있기 때문에 버전충돌문제가 빈번하게 발생한다고 합니다.

pyenv 는 파이썬 버전을 관리하는 툴 입니다.

[Github 홈페이지](https://github.com/pyenv/pyenv)

```sh
brew install pyenv
```

오류 발생
![오류발생](/assets/images/2021/06/20210610_02.png "이런...")

Cannot install under Rosetta 2 in ARM default prefix

ARM이 기본인 로제타2에서는 설치할수 없다는군요. 뭐라는...

__응용프로그램 > 터미널 > 정보가져오기 > `Rosetta를 사용하여 열기` 풀고 실행하니까 잘되었습니다.__

![설치 성공](/assets/images/2021/06/20210610_03.png "pyenv 성공")

## 드디어 python 설치
[공식 홈페이지](https://www.python.org/)

글작성일 기준 공식홈페이지의 가장 최신버전은 3.9.5

```shell
pyenv install 3.9.5
```

![설치 성공](/assets/images/2021/06/20210610_04.png "python 성공")

__머선 일이고...__

난 3.9.5를 설치하였는데... 2.7.16 이란다.

![머선 일이고...](/assets/images/2021/06/20210610_05.png "이런")

이럴때! __pyenv_ 사용!

```shell
pyenv global 3.9.5
```