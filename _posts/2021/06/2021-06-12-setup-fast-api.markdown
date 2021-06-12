---
title:  "Fast API 시작"
date:   2021-06-10 08:00:12 +0900
categories: python
---

##Python 환경설정이 먼저 ...

[이 링크를 보고 Python 설정을 먼저...](https://chozzadev.github.io/python/setup-python/ "python 환경설정")

## Fast Api
### 환경설정
[공식 홈페이지](https://fastapi.tiangolo.com/ko/ "공식홈페이지")

```shell
pip install fastapi
```

항상 새로운 프로젝트를 시작할 때 고려하는 것 중 하나가 프로젝트 구조이다.

최대한 기존에 여러 삽질하신 선배님들이 올려주신 구글 문서를 통해 best practice 를 검색하여 검토하고 반영한다.

이번에는 manage-fastapi 가 이미 잘되어 있어 해당 모듈을 이용하여 프로젝트를 생성한다.

```shell
pip install manage-fastapi
```
설치 후 아래 명령어를 입력하면 해당 프로젝트 이름으로 프로젝트 구조가 완성된다.

```shell
fastapi startproject [project_name]
```

만약 docker, database 설정등을 추가하려면 아래 명령어로 생성한다.
```shell
fastapi startproject [project_name] --interactive
```

생성된 폴더로 이동하여 아래 명령어를 사용하면 실행한다.
```shell
fastapi run
```

실행하면 아래와 같은 오류가 발생하는데...

ImportError: python-dotenv is not installed, run `pip install pydantic[dotenv]`

[pydantic 공식홈페이지](https://pydantic-docs.helpmanual.io/)

데이터 유효성 검증에 사용하는 것 같다.

```shell
pip install pydantic
```

에러메시지를 자세히보니 사실 진짜 필요한건 아래 모듈이였다.

환경설정 관련 라이브러리...

[python-dotenv Github](https://github.com/theskumar/python-dotenv)

```shell
pip install python-dotenv
```
그 이후 fastapi run 을 실행하면 잘 실행된다.

소심하게 main.py 에 Hello World api 하나 만들어본다.

```python
@app.get('/')
def read_root():
    return {'Hello': 'World'}
```

잘나온다...
![성공](/assets/images/2021/06/20210612_01.png)

