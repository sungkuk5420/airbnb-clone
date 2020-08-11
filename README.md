# airbnb clone

## package.json같은역할
```
pipenv --three
```

## 가상환경구축
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

## 어플리케이션 생성
```
django-admin startapp <application name>
```

## 파일 설명
```
urls.py 에서 접근 url을 관리한다.
```