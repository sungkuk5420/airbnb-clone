# airbnb clone


## pip 설치
```
pip install --user pipenv
```

### pip error cmd를 절대로 관리자모드로 실행할것
```
pip install --user pipenv
설치가 끝난후에 제대로 설치가 되어있는지 확인을 하려면

pipenv
라고 치시면되는데 만약에라도 pipenv 가 인식이 안되시는분이 계신다면

기존에 virtualenv 를 삭제를 해줘야됩니다.

기존 virtualenv 를 삭제

pip uninstall virtualenv
방금 설치했던 pipenv 도 삭제

pip uninstall pipenv
다시 설치 !

pip install pipenv
```

## package.json같은역할 버블을 만듬!!
파이썬 기반 버전3 가상환경을 구축해야함.
```
pipenv --three
```

## 가상환경구축후 가상환경 안으로 들어가기
```
pipenv shell
```

## 로컬환경 장고설치
```
pipenv install Django==2.2.5
```

## 장고 프로젝트설정
```
django-admin startproject config
이후 config 파일을 루트로 빼고 폴더 제거
```

## 확장프로그램에서 python 설치하기.
## Djaneiro
## code spell checker

## pip install pep8 pylint pylint_django

## 이후 린트, 포멧터등 환경설정 이어감.

## linter
```
파이썬 파일 누르고 왼쪽아래 설정누른상태에서 명령 팔렛트열고
안에서 linter검색하면 flake8 선택가능

pipenv install black --dev --pre
```

## 장고실행
```
pipenv shell
python manage.py runserver
python manage.py migrate
```

## 장고 도큐멘트
```
https://docs.djangoproject.com/en/2.2/ref/settings/#auth-password-validators
```

## 어드민페이지 진입
```
유저생성
python manage.py createsuperuser

링크뒤에 /admin붙이면 어드민페이지
```

## 데이터 마이그레이션
```
python manage.py makemigrations
python manage.py migrate
```

## 어플리케이션 생성 (반드시 복수형으로 만들것)
```
django-admin startapp <application name>
```

## 파일 설명
```
urls.py 에서 접근 url을 관리한다.
```

## 모든 생성된 파일에 대해서는 변경,삭제를 추천하지않지만 추가는 가능하다.
 ex) users 어플리케이션 내에 urls.py를 만들어서 users상세 url을 만드는것이 가능하다. users/edit users/delete 등등

 ## user 테이블의 확장
 ```
 어드민에서 사용되는 user 테이블 이외의 필드가 필요한 어플리케이션이 많으므로 확장이 필요하다.

https://docs.djangoproject.com/en/2.2/topics/auth/customizing/

1.users에서 models.py 파일에서 유저에 AbstractUser 모델을 상속하도록 지정한다.
class User(AbstractUser):

 2.config에 가서 settings파일을 연다

3.DJANGO_APPS에 INSTALLED_APPS앱을 넣는다.
4.PROJECT_APPS에 새로 추가한 앱을 넣는다. ["users.apps.UsersConfig"]

5.INSTALLED_APPS = DJANGO_APPS + PROJECT_APPS 인스톨앱에 병합
6.추가한 유저 모델을 맨밑에 적어준다.

AUTH_USER_MODEL = "users.User"

7.데이터파일 db.sqlite3을 지운다.
8.데이터 마이그레이션 한다.
python manage.py makemigrations
python manage.py migrate

9. Done!
 ```
