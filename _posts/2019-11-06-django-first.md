---
title: "장고 첫걸음"
date: 2019-11-06
categories: django
---

서비스하기 전까지는 Linux가 아닌 Windows 또는 Mac 환경에서 작업하는 것이 편하다.
윈도우에서 편하게 개발하기 위한 Back-End 환경을 조성하는 방법을 포스트한다.


### 개발환경
OS: Windows 10 <br/>
Language: Python 3.6 <br/>
IDE: Pycharm community <br/>
Framework: Django

Python과 Pycharm은 설치되어있는 것으로 간주한다.


### Django 프로젝트 생성
PyCharm 터미널(단축키: Alt + F12)을 띄운 뒤 다음과 같은 명령어로 Django 프로젝트를 생성한다.

```python
django-admin startproject (프로젝트명)
```

![1](/img/django-first/1.png)

최상 루트 폴더 (프로젝트 생성 이름)/: 프로젝트 폴더를 담고 있는 단순한 컨테이너이다. 이 디렉터리의 이름은 장고 어플리케이션에게는 아무 상관이 없으며 어떤 이름으로도 변경 가능하다.

manage.py: 장고 프로젝트와 다양한 방법으로 커뮤니케이션 할 수 있는 커맨드라인 유틸리티 이다. 

두번째 단의 FirstProject/ 폴더는 실제 프로젝트의 파이썬 패키지이다. 폴더의 이름이 파이썬 코드를 임포트할 때 사용할 실제 파이썬 패키지 이름 이다. (e.g. FirstProject.urls)

mysite/__init__.py: 아무것도 들어 있지 않은 빈 파일이며 파이썬 에게 현재 폴더가 파이썬 패키지임을 알려 준다. 

mysite/settings.py: 장고 프로젝트의 셋팅과 설정이 포함된 파일이다.

mysite/urls.py: 장고 프로젝트 안의 URL을 선언하는 곳 입니다. 장고 사이트의 컨텐츠 목록이다.

mysite/wsgi.py: WSGI 프로토콜을 사용하는 웹서버가 프로젝트의 페이지를 보여주기 위하여 가장 먼저 사용하는 파일이다. 


### Django 앱 생성

여기서 "ratelweb"라는 앱을 생성 했다.

```python
cd (Django 프로젝트 폴더)
django-admin startapp ratelweb
```


### 서버 구동하기

Django 프로젝트 폴더의 manage.py를 이용하여 서버를 구동시킨다.

```python
python manage.py runserver
```

실행 후 http://127.0.0.1:8000에 접속해 보면 다음과 같이 Django가 구동 된 화면을 볼 수 있다.


Check out the [github] for spark-1 other info. 

[github]:   https://github.com/spark-1
