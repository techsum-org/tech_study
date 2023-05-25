# 시스템 콜 (System Call)

<img src="https://velog.velcdn.com/images%2Fkakdark%2Fpost%2F679329c0-d8ef-4d7b-90b6-315ed9e17e5e%2F%EC%A0%9C%EB%AA%A9%20%EC%97%86%EC%9D%8C.png">

>  운영체제는 사용자 인터페이스를 제공한다

* 쉘 (Shell)

  사용자가 운영체제 기능과 서비스를 조작할 수 있도록 인터페이스를 제공하는 프로그램
  쉘은 터미널 환경 (CLI)과, GUI 환경 두 종류

> 운영체제는 응용 프로그램을 위해서도 인터페이스를 제공한다

* API(Application Programming Interface)

함수로 제공 ( 보통은 라이브러리 형태로 제공)

> 시스템 콜

* 시스템 콜 또는 시스템 호출 인터페이스
* 운영체제가 운영체제 각 기능들을 사용할 수 있도록 시스템 콜이라는 명령 또는 함수를 제공한다.
* API는 시스템콜을 호출하는 형태로 만들어지는 경우가 대부분이다.
* EX) POSIX API, 윈도우 API

> 운영체제를 만든다면?

1. 운영체제를 개발한다 (커널)
2. 시스템콜 개발
3. 언어별 API(library) 개발 (보통은 C언어)
4. Shell 프로그램 개발
5. 응용 프로그램 개발



