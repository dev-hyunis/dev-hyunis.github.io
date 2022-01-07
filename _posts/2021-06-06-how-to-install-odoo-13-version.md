---
title: MacOS에 Odoo 버전 13 설치하기
author: Park Bohee
date: 2021-06-06 19:16:29 +0800
categories: [Odoo, docs]
tags: [odoo, ver 13.0]
---

[2편 - ‘파이참(Pycharm)에 Odoo 환경 설정하기’](/posts/how-to-configure-odoo-with-pycharm){:target="_blank"}

<br>

###### 이 글을 읽기 전!

⚠️ MacOS를 기준으로 작성된 글입니다.

<br>

회사에서 Odoo를 사용해 개발을 하게 되면서 처음 Odoo를 접하게 되었다.
Odoo는 사용자가 그리 많지 않기 떄문에 딱 맞는 설치 가이드를 찾기 어렵다.
때문에 나 또한 처음 설치 과정에서 많은 어려움을 겪었고, 🥲 &nbsp; 블로그에 정리해 놓으면 좋겠다는 생각이 들어 정리하게 되었다.

# 홈브루(Homebrew)

홈브루를 통해 Odoo를 실행하는데 필요한 데이터베이스와 파이썬 가상 환경 패키지들을 설치한다.
홈브루가 설치되어 있지 않다면, 아래 링크를 따라 설치 후 진행한다.

<br>

👉 [MacOS에서 홈브루(Homebrew) 설치하기](https://www.44bits.io/ko/keyword/homebrew#%EB%A7%A5os%EC%97%90%EC%84%9C-%ED%99%88%EB%B8%8C%EB%A5%98homebrew-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0){:target="_blank"}

## postgresql 설치

Odoo에서는 데이터베이스로 PostgreSQL을 사용한다.

⚠️ 필요에 따라 다른 버전을 사용해도 되지만, 10 버전 이후 버전을 사용해야 한다.

```bash
$ brew install postgresql@11
```

<br>

👉 [홈브루에 다른 postgresql 버전 보기](https://formulae.brew.sh/formula/postgresql){:target="_blank"}

## pyenv 설치

pyenv는 로컬에서 다양한 Python 버전을 사용할 수 있도록 해서 Python 버전에 대한 의존성을 해결할 수 있다.

```bash
$ brew install pyenv
```

### 환경 변수 설정

`bash`를 사용하는 경우, `~/.zshrc` 대신 `~/.bashrc`로 변경해 명령어를 실행한다.

```bash
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(pyenv init --path)"' >> ~/.zshrc
$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## pyenv-virtualenv

virtualenv는 로컬에서 다양한 Python 환경을 사용할 수 있도록 한다.

```bash
$ brew install pyenv-virtualenv
```

### 환경 변수 설정

`bash`를 사용하는 경우, `~/.zshrc` 대신 `~/.bashrc`로 변경해 명령어를 실행한다.

```bash
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
$ echo 'export PYENV_VIRTUALENV_DISABLE_PROMPT=1' >> ~/.zshrc
```

# Odoo 설치

## 소스 코드 다운로드

Odoo 버전 13에 소스 코드를 clone 받아, 헷갈리지 않도록 디렉토리 이름을 `odoo-13`으로 지정한다.

```bash
$ git clone -b 13.0 --single-branch https://github.com/odoo/odoo odoo-13
```

## 파이썬 세팅

파이썬 3.7.6 버전을 사용한다. 꼭 3.7.6 버전이 아닌 `3.7`대 버전을 사용하면 된다.

```bash
$ pyenv install 3.7.6
```

### 가상 환경 생성

clone 받은 odoo-13 디렉토리 경로로 이동해, `odoo-13-venv`라는 이름으로 파이썬 가상 환경을 생성한다.

```bash
$ pyenv virtualenv 3.7.6 {가상환경명}
$ pyenv virtualenv 3.7.6 odoo-13-venv
```

<br>

가상 환경이 생성되었다면, `odoo-13` 디렉토리 경로 접근 시에 `odoo-13-venv` 가상 환경을 사용하도록 `local` 명령어를 사용해 가상 환경을 지정한다.

```bash
$ pyenv local {가상환경명}
$ pyenv local odoo-13-venv
```

<br>

⚠️ 가상 환경 지정 후, 파이썬 버전을 확인해 가상 환경이 올바르게 생성되었는지 확인한다.
설정한 `3.7.6` 버전과 다른 버전이 출력된다면 pyenv 또는 pyenv-virtualenv 환경 변수가 잘못 설정된 것이로 수정해야 한다.

```bash
$ python -V
Python 3.7.6
```

### pip 설치

pip를 통해 Odoo를 실행하는데 필요한 패키지를 설치한다.

```bash
$ pip install -r requirements.txt
```

<br>

🚨 설치 도중 `Pillow` 패키지에서 오류가 난다면 pip 버전을 업그레이드한 후에 다시 진행한다.

```bash
$ pip install --upgrade pip
```

## Odoo 환경 설정

### .odoorc 생성

odoo에 관한 환경 설정은 `.odoorc` 파일에 정의해 사용한다.
아래 명령어를 실행하면 Home 디렉토리에 `.odoorc` 파일이 생성된다.

```bash
$ python ./odoo-bin --save
```

### .odoorc 가져오기

Home 디렉토리에 생성된 `.odoorc` 파일을 odoo-13 디렉토리에 config 디렉토리로 이동시킨다.
config 디렉토리가 없다면 생성한다.

```bash
$ mv ~/.odoorc ./config/
```

<br>

디렉토리 구조는 아래와 같이 된다.

```text
|-- odoo-13
|   ├── addons
|   ├── config
|   │   └── .odoorc
|   ├── debian
|   ├── doc
// 일부 생략
```


### .odoorc 수정

.odoorc 파일에서 아래 목록에 경로들이 odoo-13 디렉토리의 경로와 다르다면 지금 설치하고자 하는 odoo-13 디텍토리의 경로로 수정한다.

- `addons_path` Odoo 모듈이 담긴 경로
- `data_dir` session 등 데이터 저장 경로
- `logfile` log 파일 경로 → 디렉토리, 파일이 없다면 생성한다.

```
addons_path = {odoo-13 path}/odoo/addons
data_dir = {odoo-13 path}/config
logfile = {odoo-13 path}/config/log/odooserver.log
```

<br>

Community 버전일 경우, `addons_path`를 아래와 같이 수정한다.

```
addons_path = {odoo-13 path}/odoo/addons, {odoo-13 path}/addons
```

<br>

디렉토리 구조는 아래와 같이 된다.

```text
|-- odoo-13
|   ├── addons
|   ├── config
|   │   └── log
|   │   │   ├── odooserver.log
|   │   └── .odoorc
|   ├── debian
|   ├── doc
// 일부 생략
```

## Odoo 실행

### postgresql 실행

홈브루를 통해 설치한 postgresql을 실행시킨다. 🐘

```bash
$ brew services start postgresql@11
```

### Odoo 실행

아래와 같이 명령어를 입력하면 Odoo가 실행된다.

```bash
$ python ./odoo-bin --config=./config/.odoorc
```

<br>

🚨 실행 시 아래와 같이 오류가 나타난다면 `psycopg2-binary` 패키지를 설치한 후에 다시 진행한다.

```bash
/Users/parkbohee/.pyenv/versions/odoo-13-venv/lib/python3.7/site-packages/psycopg2/__init__.py:144: UserWarning: The psycopg2 wheel package will be renamed from release 2.8; in order to keep installing from binary please use "pip install psycopg2-binary" instead. For details see: <http://initd.org/psycopg/docs/install.html#binary-install-from-pypi>.
  """)
```

```bash
$ pip install psycopg2-binary
```

<br>

[localhost:8069](http://localhost:8069)에 접속했을 때, 아래와 같은 페이지가 나타나면 Odoo 설치 성공이다! ✌️

![Odoo 접속 시 나타나는 페이지](/assets/img/2021-06-06-how-to-install-odoo-13-version-on-mac/01.%20Odoo%20접속%20시%20나타나는%20페이지.png)

# 마치며, 🙇🏻

## 참고한 사이트

[https://www.odoo.com/documentation/13.0/setup/install.html#mac-os](https://www.odoo.com/documentation/13.0/setup/install.html#mac-os){:target="_blank"}
