---
title: "장고 뼈대 만들기"
date: 2019-11-17
categories: django
---
[장고의 첫걸음]을 끝냈다면 웹사이트의 뼈대를 생성하는 법을 알아보자.

[장고의 첫걸음]: https://spark-1.github.io/django/django-first/

### Django 프로젝트 구조
![1](/img/django-skeleton/1.png)

```
Ratel/           # 파이참 프로젝트 명
  ratel/         # 웹사이트 폴더 (created using django-admin)
    ratel/       # 프로젝트 폴더 (created using django-admin)
    ratelweb/    # 어플리케이션 폴더 (created using manage.py)
    manage.py    # 장고 툴을 실행시키기 위한 스크립트 (created using django-admin)
```

* \_\_init__.py 는 빈 파일입니다. 이 파일은 Python에게 이 디렉토리를 하나의 Python 패키지로 다루도록 지시합니다. <br/>
* settings.py 는 웹사이트의 모든 설정을 포함하고 있습니다. 이 곳에는 우리가 만드는 어떤 application이라도 등록이 되는 곳이며,  static files의 위치, database 세부 설정 등이 들어갑니다. <br/>
* urls.py 는 사이트의 url - view의 연결을 지정해줍니다. 여기에는 모든 url 매핑 코드가 포함될 수 있지만, 특정한 어플리케이션에 매핑의 일부를 할당해주는 것이 일반적입니다. <br/>
* wsgi.py 는 당신의 장고 어플리케이션이 웹서버와 연결 및 소통하는 것을 돕습니다. 당신은 이것을 표준 형식(boilerplate)으로 다뤄도 무방합니다. <br/>
* manage.py 는 어플리케이션을 생성하고, 데이터베이스와 작업하고, 그리고 개발 웹 서버를 시작하기 위해 사용됩니다. 

**주의: 사진속에 있는 url mappings(ratelweb/urls.py), templates(ratelweb/templates/), static files(ratelweb/static/)과 연관된 파일은 자동 생성해주지 않으므로 따로 생성해줘야 한다.**


### Django 프로젝트 생성






### Django 앱 생성



### 서버 구동하기



실행 후 <http://127.0.0.1:8000>에 접속해 보면 다음과 같이 Django가 구동 된 화면을 볼 수 있다.


Check out the [github] for spark-1 other info. 

[github]:   https://github.com/spark-1
