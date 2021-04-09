# airbnb clone


## 다시들어야할것같은강의
```
#4.5 Meta Class and Photos Model (09:43)
#7.2 Many to Many _sets (02:50)
#8.5 Photo Admin (09:07)
```

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

## TimeStampedModel(core) 모델의 활용
```
공통으로 사용되는 필드를 자꾸 생성할 필요가 없다.
예를들면 
created = models.DateTimeField()
updated = models.DateTimeField()

이런것들은 클래스로 정의하여 재사용하는데 이때 사용하는것이 추상 모델이다

이것은 데이터베이스에 추가되지않고 소스내에서만 사용된다는것인데.

abstract = True
로 설정할 수 있다.
```

## 서드 파트 앱 추가

```
pipenv install django-countries
```

## Rooms 어플리케이션에서 중요한것
```
모델과 모델을 연결하기도함 host에 유저 모델을 연동 models.models.ForeignKey(user_models.User, on_delete=models.CASCADE)
```

## 관계 모델의 on_delete 이벤트 (오직 ForeignKey에만 사용가능.)
```
삭제될때의 관계모델의 행동을 정의할 수 있다.
CASCADE : 폭포수효과 위에서부터 순차적으로 삭제됌.
PROTECT : 연결된 관계형태가 있으면 삭제를 못하게 막음.
SET_NULL : 연결된 관계형태가 삭제되면 연결값이 없는 NULL로 설정함.
```

## 6강 Room Admin 부터는 어드민 패널의 화면 커스텀

## search_fields
```
객체 내부검색을 위해선 객체명__객체필드명으로 검색한다
ex) host__username

=city 일치하는단어 대소문자 구분없이
@search
None icontains =>~에 포함되다 대소문자 구분없이
^  startwith 로 시작하다.

필터에는 관계모델의 필드로도 가능하다.
호스트의 슈퍼호스트인가를 보기위해서는 "host__superhost"
```

## filter_horizontal
```
여러개의 복수 릴레이션에 관해 검색기능을 달수 있다.
filter_horizontal = ("amenities", "facilities", "house_rules")
```

## "classes": ("collapse",),
```
상세화면에서 접을 수 있는 섹션 생성.
아코디언처럼 접기, 펴기
```

## custom admin functions

```
리스트에 실제로 모델에 있는 필드가 아니라 커스텀 필드를 출력하고 싶을때 사용한다.

ex) count_amenities


def count_amenities(self, obj):
        return obj.amenities.count()

표시되는 컬럼명을 바꾸고 싶을때엔
count_amenities.short_description = "Hello sexy!"
```

## 커멘드창에서 장고 직접 통신하여 데이터 확인하는법

```
일단 장고 커멘드 셀에 진입
python manage.py shell

유저 모델에 진입
from users.models import User

이후
User 등으로 모델명 검색하면 클래스명 확인가능.
<class 'users.models.User'>

dir(User) 
이렇게 입력하면 유저의 필드names가 나온다.

vars(User)
이렇게 입력하면 유저의 구조 딕셔너리가 나온다.

User.objects 
-> user manager 는 파이썬을 이용해서 sql을 쓰지않고 데이터를 가져올 수 있다.

User.objects.all() 
유저의 모든 목록을 취득함

all_user = User.objects.all()
all_user.filter(superhost=True)
등등가능


itnico = User.objects.get(username="itnico.las.me")
print(itnico)

```

## 사이트와 어드민 패널 양쪽에서 사용되는 함수는 models.py에 정의한다

```
```

## 파일 업로드할때마다 프로젝트 루트에 저장이 됌. 저장루트를 변경하려면
```
MEDIA_ROOT = os.path.join(BASE_DIR, "uploads")
라고 config/settings.py에 추가한다.

이후 파일이 저장되는 모델에서 imageField 값을 변경해준다
avatar = models.ImageField(upload_to="avatars", blank=True)
file = models.ImageField(upload_to="room_photos")

파일접근권한추가

settings에 

MEDIA_URL = "/media/"
```

## 장고 어드민 내부에서 다른 어드민 접근 쉽게 하기.
```
#8.6 raw_ids and Inline Admin (07:59)


raw_id_fields를 추가하면 호스트 등 관계형 모델을 연결할때 작은 팝업으로 검색할 수 있게 해준다.

인라인 모델 어드민은.
어드민 안에 또 다른 어드민을 넣는것이다.
룸안에서 다시 포토화면으로 이동해서 포토를 추가하긴 너무 번거롭기때문에.

PhotoInline을 만들고 이것을 룸 어드민에 추가해준다.

class PhotoInline(admin.TabularInline):

    model = models.Photo

class RoomAdmin(admin.ModelAdmin):

    """ Room Admin Definition """

    inlines = (PhotoInline,)


admin.TabularInline
admin.StackedInline

이 두개의 옵션 변경으로 인라인 모델의 보여주는 형태를 변경할 수 있다.
```

## 장고 내부이벤트를 캐치하여 커스텀하기

```
여기서 오브젝트형 프로그래밍에선 슈퍼형식으로 상속한다.

class Dog:
    def __init__(self):
        print("woof woof")
    def pee(self):
        print("I will pee")

class Puppy(Dog):
    def pee(self):
        print("go to the park")
        super().pee()

p = Puppy()

p.pee()

->>
"woof woof"
"I will pee"

슈퍼까지 실행하면

->>
"woof woof"
"go to the park"
"I will pee"
```

## 위의 커스텀은 모든 모델 변경에 대해 일어나는 이벤트인데 반대로 어드민패널에서의 변경사항에 대해서만 수정할때에는
```
def save_model(self, request, obj, form, change):
    obj.user = request.user
    super().save_model(request, obj, form, change)

로 정의해줘야한다.
```

## 테스트용 데이터, 더미데이터 만들기. custom manage py commands django-seed
```

장고 시드는 가짜데이터를 위한것. faker를 사용하는데 이것이 하는 역할은
장ㅈ고내의 모델들을 보고 각 데이터 타입별로 데이터를 넣어준다.

장고 시드 설치.
pipenv install django-seed
```

## 시드 실행명령어 순서
```

python manage.py seed_amenities
python manage.py seed_facilities
python manage.py seed_users --number 50
룸추가하기전에 룸 타입 추가 
Hotel room
Share room
Private room
Entire place 

python manage.py seed_rooms --number 100
python manage.py seed_reviews --number 200
python manage.py seed_list --number 50
python manage.py seed_reservations --number 40
```