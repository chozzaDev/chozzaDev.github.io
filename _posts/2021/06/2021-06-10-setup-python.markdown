---
title:  "M1 Mac Python 개발 환경 설정"
date:   2021-06-10 08:00:12 +0900
categories: python
---

Fast API를 사용하여 회사에서 서비스하는 API서버를 구축하려 한다.

지금까지 14년간 Java를 써온 나에게는 새로운 도전이며 즐거움 될 것 이다.

지금 쓰는 장비가 Macbook Pro 13 M1 이기에 M1 기준으로 진행한다.

## Python 설치에 앞서...
### Homebrew
[공식 홈페이지](https://brew.sh/index_ko "Homebrew 공식홈페이지")

![버전확인](/assets/images/2021/06/20210610_01.png "버전확인 결과")

설치를 하지 않았다면 설치 스크립트
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### pyenv

파이썬에는 무수히 많은 버전이 있고, 그에 상응하는 라이브러리들이 있기 때문에 버전충돌문제가 빈번하게 발생한다고 한다

pyenv 는 파이썬 버전을 관리하는 툴

[Github 홈페이지](https://github.com/pyenv/pyenv)

```sh
brew install pyenv
```

오류 발생
![오류발생](/assets/images/2021/06/20210610_02.png "이런...")

Cannot install under Rosetta 2 in ARM default prefix

ARM이 기본인 로제타2에서는 설치할수 없다. 뭐라는...

__응용프로그램 > 터미널 > 정보가져오기 > `Rosetta를 사용하여 열기` 풀고 실행하니까 잘 됨__

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

만약 위와 같이 해도 버전이 변경되지 않는다면 Path 설정이 필요하다.
```shell
sudo vi ~/.zshrc
```

```shell
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init --path)"
fi
```

## virtualenv

[virtualenv 홈페이지](https://pypi.org/project/virtualenv/)

격리된 파이썬 환경을 만들기위해 필요하다고 한다.

```shell
pip install virtualenv
```

```shell
virtualenv venv
```
venv 폴더를 생성하고 가상환경에 필요한 파일을 복사한다.

```shell
source venv/bin/activate
```
가상환경 활성화 실행하면 아래와같이 출력

```shell
(venv) chozza@jeongtaejun-ui-MacBookPro notification-api-master %
```

파이썬 프로젝트를 하나 만들고 가상환경 sdk 설정은

File > Project Structure > SDKs > `+` > 파이썬 sdk를 선택하고 프로젝트 폴더의 venv 지정하면 된다.

![파이썬가상환경설정](/assets/images/2021/06/20210617_01.png)

설정하고 프로젝트 root에 requirements.txt 를 작성하면 종속성 관리를 할 수 있는데

마치 maven 같이 사용하는 라이브러리를 적어 놓으면 한번에 편하게 설치 가능하다.


