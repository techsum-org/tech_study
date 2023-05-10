<div align="center">
  

<img width="445" alt="스크린샷 2023-05-02 오전 11 25 18" src="https://user-images.githubusercontent.com/81874493/235566260-55975eae-d712-45c0-b510-098a82392f1e.png">

<br>

<img src="https://img.shields.io/badge/OS-007396?style=for-the-badge&logo=pcgamingwiki&logoColor=white">
 <img src="https://img.shields.io/badge/CS-E34F26?style=for-the-badge&logo=readthedocs&Color=white"> <img src="https://img.shields.io/badge/Network-1572B6?style=for-the-badge&logo=dotnet&logoColor=white"> <img src="https://img.shields.io/badge/DB-7952B3?style=for-the-badge&logo=amazondynamodb&logoColor=white">

<img src="https://img.shields.io/badge/WebSystem-6DB33F?style=for-the-badge&logo=googlechrome&logoColor=white">


</div>



<br>

## 🎬 TechSum

 신입 개발자 전공 지식을 공부하고 기술 면접 대비 정리본을 위한 Repository 입니다.


<br>

## 👨🏻‍💻 Contributors

<a href="https://github.com/techsum-org/tech_study/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=techsum-org/tech_study" />
</a>

<br>

<br>

## 🗂 폴더 구조
```bash
└─ tech_study
    ├── JiYongKim
    |   └── OS
    |       └── OS_01
    ├── hobinLee
    └── suhaLee

└─  techSum
    ├── OS
    |   ├── os.md
    |   ├── process_thread.md
    |   └── ...etc
    ├── Network
    ├── CS
    └── DB
``` 
* tech_study
  * 각자 주차별 키워드 자료조사 및 정리
  * 각각의 폴더를 생성하여 사용하며 자신의 폴더가 아닌 폴더는 사용하지 않는다.

* techSUm
  * 발표 이후 피드백과 질문사항을 참고하여 각자 정해진 키워드별로 정리본을 추가한다.  
  
<br>

## 😸 Github 사용하기
[Git 연동 방법](https://www.notion.so/Git-3106b27169a346658c5139adb541830c?pvs=4)

[Git branch 만들기](https://www.notion.so/Git-branch-16b580f2b26344a8802e1cdea2e754f9?pvs=4)

[Git 기본 명령어](https://private-possum-5a6.notion.site/Git-8dd7e6646a72438783f281363ec91da5)

<br>

## 💻 commit 규칙

- Commit
    - Commit 규칙을 통해 각 branch 별 commit 사항을 관리한다.

    <br>
    
    - commit message
        - 형식
            
            ```markdown
            <type> (<scope>): <explain>          
            ```
            
            <br>
            
        - type
            - feat : 새로운 추가 파일에 대한 커밋
            - update : 수정에 대한 커밋
            - img : 이미지 파일 추가에 대한 커밋
            
        
        <br>
        
        ex) commit message example
        
          `feat (os1주차) : os1주차 md 파일 생성`
        
          `update(os1주차) : os1차 A내용 수정`
        
          `img(os1주차) : img파일 추가`
        


<br>

## 📽 진행 방식

1. 매주 정해진 키워드에 대해 자료조사 한다.
2. 자료조사 이후 md 파일으로 정리한다. 
    * 'A란 ~~~ 이다.' 약술형 정리 방식으로 작성한다.
    * 키워드에 대해 설명을 추가한다.
    * 키워드에 대한 장점과 단점을 추가한다.
3. 매주 각자 키워드를 선택하여 간단한 ppt를 만들어 발표한다.
4. 발표에서 나온 질문사항이나 피드백에 대해 issue에 정리하여 올린다.
5. issue에 달린 comment에 대해 답한 이후 issue를 닫는다.
6. 자신이 발표한 키워드를 종합 정리본에 md파일을 추가한다.



<br>
  


## 📺 스터디 키워드

 📍Operating System
  * 운영체제란
  * 프로세스 vs 스레드
  * 프로세스 주소 공간
  * 인터럽트(Interrupt)
  * 시스템 콜(System Call)
  * PCB와 Context Switching
  * IPC(Inter Process Communication)
  * CPU 스케줄링
  * 데드락(DeadLock)
  * Race Condition
  * 세마포어(Semaphore) & 뮤텍스(Mutex)
  * 페이징 & 세그먼테이션 (PDF)
  * 페이지 교체 알고리즘
  * 메모리(Memory)
  * 파일 시스템
<br>

 📍Network
  * OSI 7 계층
  * TCP 3 way handshake & 4 way handshake
  * TCP/IP 흐름제어 & 혼잡제어
  * UDP
  * HTTP & HTTPS
  * TLS/SSL handshake
  
<br>

 📍CS
  * 컴퓨터 구조 기초
  * 컴퓨터의 구성
  * 중앙처리장치(CPU) 작동 원리
  * 캐시 메모리
  * 고정 소수점 & 부동 소수점
  * 패리티 비트 & 해밍 코드
  * ARM 프로세서
  * 클린코드 & 리팩토링 / 클린코드 & 시큐어코딩
  * TDD(Test Driven Development)
  * 애자일(Agile) 정리1 / 애자일(Agile) 정리2
  * 객체 지향 프로그래밍(Object-Oriented Programming)
  * 함수형 프로그래밍(Fuctional Programming)
  * 데브옵스(DevOps)
  * 마이크로서비스 아키텍처(MSA)
 
 <br>
 
 📍DB
  * 인덱스
  * 테이블 설계와 정규화
  * 트랜잭션
  * 바이너리 로그
  * 트랜잭션 locking
 
 <br>
 
 📍Design Pattern
  * 디자인패턴 개요(Overview)
  * 어댑터 패턴
  * 싱글톤 패턴
  * 탬플릿 메소드 패턴
  * 팩토리 메소드 패턴
  * 옵저버 패턴
  * 스트레티지 패턴
  * 컴포지트 패턴
  * SOLID

  
 
 <br>
 
 📍Web System
  * 브라우저 동작 방법
  * 쿠키(Cookie) & 세션(Session)
  * HTTP Request Methods
  * HTTP Status Code
  * REST API
  * 웹 서버와 WAS의 차이점
  * JWT(JSON Web Token)
  * Authentication and Authorization
  * 로그 레벨
  * CSR & SSR
  * 네이티브 앱 & 웹 앱 & 하이브리드 앱
  







