# Django

# 프로젝트 구조

![Image](https://github.com/couponApiServerEconovation/couponApiServerMtak/assets/48946398/b4f15dab-05c2-4b3c-97ba-82e2b2387f93)

```shell
$ django-admin startproject mysite
```

## 개발용 서버

spring과 다르게, 순수 python 으로 만든 갸벼운 서버가 내장되어 있다.  물론 운영할때는  아파치 같은 걸로 바꿔 사용한다.

```shell
$ python manage.py runserver
```

서버 어플리케이션을 배포할 때 두 가지 방식으로 배포할 수 있다. 

> [배경]
>
> 로기인이나 회원가입 요청 처럼 클라이언트의 요청이 동적으로 달라지면 순수 웹 서버에서는 이를 처리할 용병(웹 어플리케이션)을 그 때 그 그 때 고용할 수 밖에 없다. 
> 이 때 고용하는 형태가 용병마다 달라지면 불편하니까 공통의 인터페이스(cgi)를 제공 용병에게 제시할 수 밖에 없다. 
>
> [문제 상황]
>
> 문제는 요청이 들어올 때 마다 용병을 부르기에는(어플리케이션 프로세스를 실행하기에는)  요청이 많아질 때 성능이 떨어진다. 
>
> 특히, 파이썬 같이 인터프리터 언어의 프로그램은 더하다.
>
> [해결]
>
> 하나의 프로세스로 여러 요청을 처리하는 fastCGI등장.

* wsgi
  * 용병을 요청때 마다 고용하지 않고 용병을 상주시키고 부려먹는 방식으로 요청을 처리하는 파이썬 application  담당 매니저다.
  * 왜 fastCGI를 안쓰고 WSGI를 쓰냐면, 대부분의 서버가 JVM 기반이라 python을 모르기 때문이다..
  * 쨋든 동작하는 방식은 기존의 CGI는 요청마다 fork() 때려서 환경변수나 객체로 요청 정보를 넘겨 줬다면, WSGI 는 callback과 (cgi에서 넘겨주는 데이터)객체를 웹 어플리케이션에 넘겨준다. 
  * 참고로 callback의 매개변수는 http status와 response headers다.
* asgi
  * wsgi는 요청들을 동기적으로 밖에 처리 못해서 비동기적으로 처리할 수 있는 asgi가 등장했다.

> Ref
>
> * https://blog.neonkid.xyz/249
> * https://jellybeanz.medium.com/cgi-wsgi-asgi-%EB%9E%80-cgi-wsgi-asgi-bc0ba75fa5cd
> * https://kangbk0120.github.io/articles/2022-02/cgi-wcgi-asgi
> * https://nitro04.blogspot.com/2020/01/django-python-asgi-wsgi-analysis-of.html

