---
title: "장고 뼈대 만들기"
date: 2019-11-17
categories: django
---
[장고의 첫걸음]을 끝냈다면 웹사이트의 뼈대를 생성하는 법을 알아봅시다. <br>

[장고의 첫걸음]: https://spark-1.github.io/django/django-first/
<br>

### Django 프로젝트 구조
![1](/img/django-skeleton/1.png)
```
Ratel/           # 파이참 프로젝트 명
  ratel/         # 웹사이트 폴더 (created using django-admin)
    ratel/       # 프로젝트 폴더 (created using django-admin)
    ratelweb/    # 어플리케이션 폴더 (created using manage.py)
    manage.py    # 장고 툴을 실행시키기 위한 스크립트 (created using django-admin)
```
* \_\_init__.py 는 빈 파일입니다. 이 파일은 Python에게 이 디렉토리를 하나의 Python 패키지로 다루도록 지시합니다. <br><br>
* settings.py 는 웹사이트의 모든 설정을 포함하고 있습니다. 이 곳에는 우리가 만드는 어떤 application이라도 등록이 되는 곳이며,  static files의 위치, database 세부 설정 등이 들어갑니다. <br><br>
* urls.py 는 사이트의 url - view의 연결을 지정해줍니다. 여기에는 모든 url 매핑 코드가 포함될 수 있지만, 특정한 어플리케이션에 매핑의 일부를 할당해주는 것이 일반적입니다. <br><br>
* wsgi.py 는 당신의 장고 어플리케이션이 웹서버와 연결 및 소통하는 것을 돕습니다. 당신은 이것을 표준 형식(boilerplate)으로 다뤄도 무방합니다. <br><br>
* manage.py 는 어플리케이션을 생성하고, 데이터베이스와 작업하고, 그리고 개발 웹 서버를 시작하기 위해 사용됩니다. <br><br>
**주의: 사진속에 있는 url mappings(ratelweb/urls.py), templates(ratelweb/templates/), static files(ratelweb/static/)과 연관된 파일은 자동 생성해주지 않으므로 따로 생성해줘야 합니다.** <br>
<br>

### application 등록하기
어플리케이션을 생성하였으면 프로젝트에 등록해야합니다. <br>
어플리케이션들은 프로젝트 설정 안 `INSTALLED_APPS` 리스트에 추가함으로써 등록 할 수 있습니다. <br>
등록하면 실행될 때 프로젝트에 포함시키게 됩니다. <br>
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'catalog.apps.RatelConfig',     # 등록되는 어플리케이션
]
```
새로운 행은 어플리케이션 구성 객체(application configuration object) (RatelConfig)를 지정하게 됩니다. <br>
이것은 어플리케이션을 생성할 때 `/ratel/ratelweb/apps.py` 안에 생성됩니다. <br>
<br>

### 프로젝트의 다른 설정
**settings.py** 에서 다른 설정들을 확인할 수 있습니다. <br>
Database 관련 설정 <br>
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
* SECRET_KEY. 이것은 장고의 웹사이트 보안 전략의 일부로 사용되는 비밀 키 입니다. 만약 이 코드를 개발 과정에서 보호하지 않는다면 제품화(production) 과정에서 다른 코드(아마 환경 변수나 파일에서 읽어오는)를 사용해야 할 것입니다. <br>
* DEBUG. 이것은 에러가 발생했을 때 HTTP 상태 코드 응답 대신 디버깅 로그가 표시되게 합니다. 디버깅 정보는 공격자에게 유용하기 때문에 제품화된(production) 환경에서는 False 로 설정해야 합니다. 하지만, 지금은 True로 설정합시다. <br>
<br>

### URL 매퍼 연결하기

 
<br>

**Check out the [github] for spark-1 other info.** 

[github]:   https://github.com/spark-1
