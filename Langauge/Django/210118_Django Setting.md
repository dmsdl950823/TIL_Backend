- [1. Django](#1-django)
  - [1.1. 가상 디렉토리 구축(CentOS 기준)](#11-가상-디렉토리-구축centos-기준)
  - [1.2. 설치](#12-설치)
  - [1.3. GIT 설치](#13-git-설치)
  - [1.4. 동작 방식](#14-동작-방식)
  - [1.5. 프로젝트 제작](#15-프로젝트-제작)
  - [1.6. 설정 변경](#16-설정-변경)
  - [1.7. 데이터베이스 설정](#17-데이터베이스-설정)
- [여기 부터 연장 필요](#여기-부터-연장-필요)

---------------

# 1. Django
출처 : [장고걸스](https://tutorial.djangogirls.org/ko/)

## 1.1. 가상 디렉토리 구축(CentOS 기준)

``` bash
  $ mkdir djangogirls
  $ cd djangogirls
  $ python3 -m venv myvenv      # myvenv 이름(임의지정 가능)의 가상환경 구축
  $ source myvenv/bin/activate  # 가상환경 시작
```
## 1.2. 설치
``` bash
  $ python3 -m pip install --upgrade pip  # pip upgrade
  $ pip install django~=2.0.0             # Django 설치
```
## 1.3. GIT 설치    
``` sh
    # sudo yum install git 
```
## 1.4. 동작 방식
1. 웹 서버에 요청이 오면 장고로 전달됨.
2. 장고 urlresolver 는 전달된 웹 페이지의 주소 확인.
3. URL이 일치할 경우 `view` 함수에 전달.
4. `view` 함수는 권한을 확인, 수정, 웹 브라우저에 전달.

## 1.5. 프로젝트 제작
``` sh
  $ django-admin startproject mysite .  # . 은 현재 디렉토리에 설치하라는 의미

  # 생성된 django 디렉토리 내부
  djangogirls
  ├───manage.py           # 사이트 관리, 설치작업 없이 컴퓨터에서 웹 서버 시작 가능
  └───mysite
        settings.py     # 웹사이트 설정 파일
        urls.py         # urlresolver가 사용하는 패턴 목록 포함
        wsgi.py
        __init__.py
```
## 1.6. 설정 변경
``` sh
  # mysite/settings.py 설정 변경
  TIME_ZONE = 'Asia/Seoul' 
  
  # 앱 배포시 pythonanywhere 의 호스트 이름과 일치 하지 않으므로 설정 변경 필요
  ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']  
  STATIC_URL = '/static/'
  STATIC_ROOT = os.path.join(BASE_DIR, 'static')       #추가
```
## 1.7. 데이터베이스 설정
``` sh
    #  mysite/settings.py 설정 변경
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }
```
``` sh
    # commandline
    $ python manage.py migrate    // 데이터 베이스생성
    $ python manage.py runserver  // 웹 서버 실행 
```
이제 등록했던 서버 'http://127.0.0.1:8000' 에 접속하면'it worked!' 페이지가 보일것이다

-------------------

# [여기](https://tutorial.djangogirls.org/ko/django_models/) 부터 연장 필요




