---
title: "웹 배포하기"
date: 2019-11-12
categories: server
---

우리는 프로젝트 테스트를 위해 runserver를 사용해왔다. <br>
실제로 runserver는 장고에서 제공하는 테스트용 웹서버이다. <br>
하지만 만약 프로젝트를 고객에게 상용화할 때는 처리 능력이나 보안 문제 때문에 Apache나 Nginx 등의 상용 웹 서버를 사용해야 한다. <br>
Nginx와 WSGI 미들웨어 Gunicorn을 사용해 프로젝트를 AWS 인스턴스에 배포하는 방법에 대해 알아볼 것이다. <br>
<br>

### 사전 필요 작업
AWS 인스턴스 생성 <br>
Django 프로젝트 생성 <br>
<br>

### Nginx 설치 및 실행
터미널에서 ssh를 통해 AWS 인스턴스에 접속한다. <br>
```bash
$ ssh -i .ssh/(나의 인스턴스 키) ubuntu@(aws 인스턴스 ip 주소)
```
AWS 인스턴스 초기 설정 <br>
실제로 인스턴스에 서버를 구축하기 위해 AWS 인스턴스에 Nginx를 설치할 것이다. <br>
다음 명령어로 Nginx 설치한다. <br>
```bash
$ sudo apt-get update
$ sudo apt-get install -y nginx
```
또한 character-set을 다음과 같이 설정한다. <br>
```bash
$ export LC_ALL="en_US.UTF-8"
$ export LC_CTYPE="en_US.UTF-8"
```
그 뒤 Nginx와 프로젝트를 연동하기 위해 Nginx 설정 파일을 열어 다음과 같이 수정하자. <br>
```bash
$ sudo vim /etc/nginx/sites-available/default
```
```
server { 
        listen 80; 
        location /static/ { 
                alias /home/ubuntu/.../staticfiles/; 
        } 
        location /site { 
                proxy_pass http://127.0.0.1:8000; 
                proxy_http_version 1.1; 
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade; 
        } 
}
```
그 뒤 다음 명령어로 Nginx를 재시작하면 설정이 적용된다. <br>
```bash
$ sudo service nginx restart
```
다음 명령어를 통해 nginx가 현재 실행되고 있는지 확인할 수 있다. <br>
```bash
$ sudo service --status-all | grep nginx
```
또한 크롬 등의 브라우저를 열어 인스턴스 주소로 접속 시 다음과 같은 화면이 나타나면 Nginx 서버가 정상적으로 작동된다는 의미이다. <br>
이제 인스턴스 시작 시 자동으로 Nginx 웹 서버가 실행되어, 80번 포트에서 요청을 기다리는 상태가 된다. <br>

* 참고 <br>
80번 포트는 디폴트 포트이므로, 포트를 입력하지 않으면 자동으로 80번 포트로 연결된다. <br>
위 설정에 따르면, 만약 내 인스턴스의 IP 주소가 13.209.97.110일 때, 사용자가 13.209.97.110:80/site 경로로 인스턴스에 접속하면 인스턴스 내 127.0.0.1:8000에서 실행 중인 장고 프로세스로 요청이 전송되고, 13.209.97.110:80/static로 들어오는 요청은 staticfiles 디렉토리의 절대 경로로 연결된다.  <br>
<br>

### 프로젝트 가져오고 환경설정 하기
이제 github에 올린 프로젝트를 가져와보자. <br>
```bash
$ git clone https://github.com/(owner 이름)/(레포지토리 이름).git
```
프로젝트 폴더로 들어가 해당 프로젝트를 위한 파이썬 가상환경을 만들고 가상환경을 실행해보자. <br>
```bash
$ cd (생성된 프로젝트)
$ virtualenv venv
$ source venv/bin/activate
```
쉘 왼쪽에 (venv)가 생기면 성공이다. <br>
가상환경을 나가고 싶으면 간단히 deactivate라고 명령하면 된다. <br>
<br>
잠시 로컬 개발 환경으로 돌아가보자 <br>
다음 명령어를 통해 설치한 모듈 목록을 requirements.txt에 저장해 둘 수 있다. <br>
```bash
$ pip freeze > (requirments 경로)/requirements.txt
```
다시 배포환경으로 돌아온다. <br>
이제 내가 사용하고자 하는 모듈을 가상환경에 맘대로 설치하면 된다. <br>
```bash
$ pip install -r (requirments 경로)/requirements.txt
```
<br>

### 서버 구동하기
Django 프로젝트 폴더의 manage.py를 이용하여 서버를 구동시킨다. <br>
runserver뒤에 0:8000을 꼭 붙여주어야 한다. <br>
```bash
$ python manage.py runserver 0:8000
```
실행 후 (aws public 주소):8000에 접속해 보면 프로젝트가 올라간것을 확인할 수 있다. <br>
<br>

**Check out the [github] for spark-1 other info.** 

[github]:   https://github.com/spark-1
