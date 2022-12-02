# Django 시작 및 구조 파악하기

### Django 설치 (아마 requirements에 깔려있을듯)
pip install django
pip install django-rest-framework

### Django 처음 설치 시 구조
* [프로젝트 파일]  
  * [프로젝트 파일] : 상위 폴더와 같은 폴더는 다른 template를 전부 연결하기 위한 수단(main)
  * asgi.py     : 크게 쓸 일 없음
  * settings.py : 전체적인 부분을 작성하는 곳
  * INSTALLED_APPS : 앱을 연결하거나 기능들을 해당 프로젝트(장고)에 연결할 때 사용
  * MIDDLEWARE     : 정확히 모르겠음
  * DATABASE       : DATABASE를 연결하는 곳
  * urls.py     : 다른 프로젝트의 template를 웹에 연결하기 위한 파일
  * urlpatterns : path('', include('[다른폴더].urls') # 보통 다른 파일에 urls.py를 만들기 때문에 해당 urls를 연결하는 것 => '' 대신 'a/' 면 local/a로 나옴
  * wsgi.py     :  
* [1번째 APP] : 장고 안에서 여러가지 페이지를 개별적으로 관리할 수 있음
  * admin :
  * template : 직접 폴더를 만들어야하며 해당 폴더 안에 html을 작성해서 넣어야함
  * models : 데이터베이스를 만드는 파일이다.
  * urls : 직접 만들어야하며 views에의 def를 들고와서 연결함
  * path('', views.[함수], name = 'index') # views.index => 여기에서 view 안에 있는 함수를 들고옴
  * views : 실직적으로 페이지 구현해야 하는것을 Rendering하는 곳 (forms, models를 import 해놓아야 편함)
  * serializers : Data를 json형태로 변환시킬 때 필요한 장소

### Django rest-framework가 돌아가는 기본적인 구조
1. Front에서 Axios를 통해서 어떤 urls로 Request를 보냄
2. DRF에서는 urls에 맞는 로직에 맞춰서 request로 데이터를 받음.
3. 로직 처리 후 seralizer.py에서 json 형태로 변환시킴
4. 변환시킨 데이터를 Response를 통해서 보내줌