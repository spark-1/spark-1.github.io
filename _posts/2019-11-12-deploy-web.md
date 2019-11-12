---
title: "웹 배포하기"
date: 2019-11-12
categories: django, server
---

우리는 프로젝트 테스트를 위해 runserver를 사용해왔다. 실제로 runserver는 장고에서 제공하는 테스트용 웹서버이다. 하지만 만약 프로젝트를 고객에게 상용화할 때는 처리 능력이나 보안 문제 때문에 Apache나 Nginx 등의 상용 웹 서버를 사용해야 한다. Nginx와 WSGI 미들웨어 Gunicorn을 사용해 프로젝트를 AWS 인스턴스에 배포하는 방법에 대해 알아볼 것이다.


### 사전 필요 작업
AWS 인스턴스 생성 <br/>
Django 프로젝트 생성 <br/>


### Nginx 설치 및 실행
터미널에서 ssh를 통해 AWS 인스턴스에 접속한다. <br/>
```python
ssh -i .ssh/(나의 인스턴스 키) ubuntu@(aws 인스턴스 ip 주소)
```

AWS 인스턴스 초기 설정 <br/>
실제로 인스턴스에 서버를 구축하기 위해 AWS 인스턴스에 Nginx를 설치할 것이다. <br/>
다음 명령어로 Nginx 설치한다. <br/>
```python
sudo apt-get update
sudo apt-get install -y nginx
```
또한 character-set을 다음과 같이 설정한다. <br/>
```python
export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
```
그 뒤 Nginx와 프로젝트를 연동하기 위해 Nginx 설정 파일을 열어 다음과 같이 수정하자. <br/>
```python
sudo vi /etc/nginx/sites-available/default
```




### Django 앱 생성


```python
cd (Django 프로젝트 폴더)
django-admin startapp ratelweb
```


### 서버 구동하기

Django 프로젝트 폴더의 manage.py를 이용하여 서버를 구동시킨다.

```python
python manage.py runserver
```

실행 후 <http://127.0.0.1:8000>에 접속해 보면 다음과 같이 Django가 구동 된 화면을 볼 수 있다.


Check out the [github] for spark-1 other info. 

[github]:   https://github.com/spark-1
