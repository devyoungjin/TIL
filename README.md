# TIL

![HitCount](http://hits.dwyl.io/youngjinmo/youngjinmo/TIL.svg)

*Today I learned.*

오늘 제가 배운 내용을 정리하는 공간입니다.

<Br>

## ToC

- [Programming Language](#language)
  - [Java](#)
    - [Wrapper Class](#wrapper-class)
  - [SQL](#sql)
    - [AND 조건 조회](#order-and)
    - [LIMIT](#limit)
    - [DISTINCT](#distinct)
    - [연산처리](#sql-math)
- [Backend](#backend)
  - [HTTP](#http)
    - [GET/POST](#get-n-post)
  - [Template Engines](#template-engines)
    - [Mustache](#mustache)
  - [JPA](#jpa)
    - [Hibernate](#hibernate)
- [Git](#git)
- [DevOps](#devops)
- [Linux](#linux)
  - [명령어](#command-of-linux)
- [Others](#others)

<br>

# <a name="java"></a> Java

<img src="https://cdn.vox-cdn.com/thumbor/FDD76YJZJFPyNUfT3ZBHcnMA0Ec=/43x0:593x367/1200x800/filters:focal(43x0:593x367)/cdn.vox-cdn.com/uploads/chorus_image/image/48667835/dbgxt2rvpd26udoyzcqn.0.0.jpg" width="400" />

## <a name="wrapper-class"></a>Wrapper Class

기본형 데이터타입의 객체화를 가능하게 도와주는 클래스. `java.lang` 패키지 안에 포함되어있다.

- 기본형 타입 : `int`
- 객체형 타입 : `Integer`



Wrapper Class는 다음과 같은 기능을 수행한다.

<img src="http://www.mediafire.com/convkey/e0bf/3kqk5j823suxigbzg.jpg" />

**오토 박싱 (Auto Boxing)**

기본 타입 데이터를 객체 타입의 데이터로 자동 형변환해주는 기능

**오토 언박싱 (Auto Unboxing)**

오토박싱과 반대로 객체 타입의 데이터를 기본형 타입 데이터로 자동 형변환



### References

- [프로그래머스 - [자바 중급] java.lang 패키지/오토박싱](https://youtu.be/Eofo8_xZbfk)

<br>

# <a name="sql"></a>SQL

### <a name="order-and"></a>AND 조건으로 조회할 때

이름(`NAME`) 순으로 조회할 때, 이름이 같을 경우, 생일(`BIRTH_DATE`)이 빠른 순으로 조회할 때 사용하는 쿼리이다.

```SQL
SELECT
  NAME, BIRTH_DATE
FROM
  ANIMAL_INS
ORDER BY
  NAME ASC,
  DATETIME DESC; 
```

위의 이미지처럼 작성하면 `ORDER BY` 에서 먼저 작성한 이름순(`ASC`)으로 정렬되고, 이름이 같을 경우 날짜(`DATETIME`)를 역순으로 정렬해서 조회하는 쿼리이다.

<br>

### <a name="limit"></a>LIMIT

조회하는 데이터의 갯수를 결정할 때 사용하는 쿼리이다.

```SQL
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATATIME ASC
LIMIT 1;
```

날짜(`DATETIME`)순으로 정렬했을 때, 데이터를 하나만 조회하는 쿼리이다. 즉 가장 최신 데이터를 조회한 것이다. `LIMIT`을 활용하면 최대값, 최소값도 구할 수 있다.

<br>

### <a name="distinct"></a>DISTINCT

조회 조건에서 중복을 제거하고 조회할 때 사용하는 쿼리이다.

```sql
SELECT DISTINCT NAME
FROM ANIMAL_INS;
```

`DISTINCT` 는 `SELECT` 에서 사용하는 쿼리이다. 중복을 제거해서 조회하고 싶은 컬럼 앞에 `DISTINCT` 를 붙이면 해당 컬럼은 중복이 제거되어 조회된다.

<br>

### <a name="sql-math"></a>연산 처리

현재까지 내가 알고있는 SQL에서 연산하는 방법은 세가지이다.

1) 컬럼을 연산해서 새로운 컬럼으로 조회하기

```sql
SELECT DATA1 * DATA2 AS NEW_DATA
FROM ANIMAL_INS
ORDER BY DATETIME ASC;
```

`DATA1`과 `DATA2`를 각각 곱해서 `NEW_DATA` 라는 새로운 컬럼명으로 조회하는 쿼리이다.



2) 조회되는 데이터의 수 조회

```sql
SELECT COUNT(NAME)
FROM ANIMAL_INS
ORDER BY DATETIME ASC;
```

`NAME` 컬럼의 데이터 수를 조회하는 쿼리이다.



3) 데이터 합계 구하기

```sql
SELECT SUM(WEIGHT)
FROM ANIMAL_INS;
```



4) 데이터 평균 조회하기

```sql
SELECT AVG(AGE)
FROM ANIMAL_INS;
```

<br>

# <a name="backend"></a>Backend

<br>

# <a name="http"></a>HTTP

HTTP는 클라이언트와 서버간의 통신을 위한 프로토콜이다. HyperText Transfer Protocol의 약자이다.

클라이언트와 서버가 request-response할 수 있도록 역할을 수행하는 프로토콜이다.

<br>

## GET/POST

GET은 전달하는 데이터를 url 주소에 붙여서 전달하는 HTTP 메서드이다. 반면에 POST는 url 주소에 붙이지 않고 전달할 수 있는 HTTP 메서드이다.

일반적으로 게시판의 id값을 통해 게시글 상세보기 할 때엔 url뒤에 ?을 붙여서 게시글 id값을 GET 메서드로 서버에 전달한다. 반면 사용자의 아이디나 비밀번호와 같은 민간한 정보는 POST 메서드로 서버에 전달한다.

Outsider님이 블로그에 정리하신 <a href="https://blog.outsider.ne.kr/312" target="_blank">글</a>을 보면, GET과 POST의 차이를 다음과 같이 설명한다.

> **GET은 가져오는 것**이고, **POST는 (서버)수행하는 것**입니다.
>
> GET은 Select적인 성향을 가지고 있으며, POST는 서버의 값이나 상태를 바꾸기 위해서 사용한다.

w3school에서도 GET 메서드에 대해 *"GET is used to request data from a specified resource"* 라고 설명한다. POST 메서드에 대해선 *"POST is used to send data to a server to create/update a resource"* 정리했다. Outsider님의 정리와 정확히 일치한다.



w3scool에서는 다음처럼 GET/POST를 비교하였다.

| HTTP Methods | requests                                                     |
| ------------ | ------------------------------------------------------------ |
| GET          | GET 메서드의 요청은 캐싱될 수 있다.<br />GET 메서드의 요청은 브라우저 히스토리에 기록된다.<br />민감한 데이터를 다룰땐 이용해서는 안된다.<br />GET 메서드의 요청은 길이 제한을 받는다. 긴 데이터는 GET 메서드로 요청할 수 없다. |
| POST         | POST 메서드의 요청은 캐싱되지 않는다.<br />또한 브라우저 히스토리에도 기록되지 않는다.<br />POST 메서드의 요청은 GET 메서드 요청과 달리 길이에 제한을 받지 않는다. |

<br>**References**

- [Outsider - GET과 POST의 차이](https://blog.outsider.ne.kr/312)
- [w3school - HTTP Request Methods](https://www.w3schools.com/tags/ref_httpmethods.asp)

<br>

# <a name="template-engines"></a>Template Engines

[템플릿 엔진](https://en.wikipedia.org/wiki/Web_template_system)이란, 데이터 모델에 따른 문서를 합성하여 웹 문서를 만들어주는 소프트웨어라고 한다. 

템플릿 엔진은 목적에 따라 다양한 템플릿 엔진을 사용할 수 있다. `include` 코드를 이용하여 html의 중복 코드를 제외하고 싶을 때에는 Apache Tiles와 같은 레이아웃 템플릿 엔진을 사용할 수 있다.

또 View에서 데이터를 출력하고 싶을 때는 Thymeleaf, JSP 같은 텍스트 템플릿 엔진을 쓸 수 있다. 

위 두 템플릿은 서로 베타적이지 않고, 동시에 사용이 가능하다.

<br>

**Reference**

- [gmlwjd9405 - [Template Engine] 템플릿엔진이란](https://gmlwjd9405.github.io/2018/12/21/template-engine.html)

<br>

## <a name="mustache"></a>Mustache

JSP도 있고, Spring Boot에서는 Thymeleaf를 미는것도 같은데 왜 Mustache를 알아야 할까.

우선 JSP는 오래된 기술이다. 오래되었다는 이유만으로 배척할 필요는 없으나 향후 지원이 안될 가능성이 높기 때문에 실무에서 가장 많이 쓰이고 있거나 앞으로 많이 쓰일 소프트웨어를 배울 필요가 있다고 생각했다.

Thymeleaf는 잘 모르지만, 느리다는 성능 상의 이슈가 있는 편이다.

**Mustache는 템플릿 엔진중 가장 많은 언어를 지원한다.** [위키](https://en.wikipedia.org/wiki/Web_template_system#Server-side_systems)를 열어보면, C++, 커피스크립트, Go, 자바, .NET, PHP, Pyhton중 내가 아는 프로그래밍언어는 거의 다 지원되는듯하다.

또 Mustache는 [심플한 문법](https://mustache.github.io/mustache.5.html)을 갖고 있다고 한다. 이 부분은 직접 경험해야 알 수 있을 것 같다.

일단 대략적으로 이정도만 알고 있는데, 향후 써보면서 계속 업데이트 해보겠다.

<br>

**Reference**

- [Baeldung - Spring Boot Mustache](https://www.baeldung.com/spring-boot-mustache)

<br>

# <a name="jpa"></a>JPA

Hibernate를 알기 앞서 JPA와 ORM에 대해 정리하려고 한다.

<b>JPA(Java Persistent API)</b>는 자바 진영의 ORM 기술 표준 명세라고 한다.

<b>ORM(Object Relational Mapping)</b>은 객체 관계형 매핑을 돕는데, 객체를 DB 테이블이 되도록 매핑시켜주는 것을 의미한다.

객체는 객체대로 설계를 하고, 관계형 데이터베이스는 DB대로 설계하면 ORM 프레임워크가 중간에서 매핑하는 구조이다.

<a name="structure-of-jpa"></a><img src="http://www.mediafire.com/convkey/76fe/4uc9nqw8rls40b7zg.jpg" />

Java 애플리케이션에서 DB를 통신하려면 JDBC API를 사용해야하는데, JPA가 중간에 개입하는 구조이다. JPA는 Java 애플리케이션의 DAO 영역에서 전달받은 객체를 분석해서 SQL을 생성하고, JDBC API를 사용해서 쿼리를 DB에 전송하는 역할을 한다.

*객체를 자바 컬렉션에 저장하듯이 DB에 객체를 저장할수는 없을까?*

JPA 탄생 이전까지는 데이터 중심의 모델링을 우선시 했다고 한다. 객체지향의 특징보다는 단순히 데이터의 전달 목적으로 객체(VO, DTO)를 사용했다고 한다. 그러나 이는 심각한 비효율을 발생시켰다. 객체에 데이터를 추가할 때 반복적인 CRUD 작업을 해야했기 때문이다.  **ORM은 SQL 쿼리 대신 코드로 데이터를 조작함으로써 개발자 입장에서 생산성을 높힐 수 있는 도구**이다.

예를들면, `SELECT * FROM users;` 라는 SQL 쿼리를 `users.findAll()` 로 대체할 수 있는 것이다. 이렇게 하면 중복을 제거할 수 있으며, 객체지향의 장점을 살려 데이터를 제어할 수 있다.

<br>

**Reference**

- [김영한 - JPA 소개](https://youtu.be/U2s2JhzPZf4)

<br>

## <a name="hibernate"></a>Hibernate

EJB(Entity Java Beans)이 있었는데, 이게 너무 불편하고 성능이 떨어지는 단점이 있었다. 그런데 이를 답답해 여긴 어느 한 개발자가 이를 대체할 수 있는 Hibernate를 개발해서 오픈소스로 공개했다. 이후 자바 진영에서 새로운 표준을 개정하면서 Hibernate 개발자를 모셔가서 [JPA](#jpa)가 개발되었다고 한다.

Hibernate는 JPA를 구현한 프레임워크이다. 국내에선 Hibernate보다 [MyBatis](https://sjh836.tistory.com/127)를 더 많이 사용하고 있으나 한국, 일본, 중국을 제외한 전 세계에서 Hibernate를 더 많이 사용한다고 한다.

<br>**Hibernate의 장점**

- **생산성**
  - SQL 쿼리를 직접 사용하지 않고, 객체를 사용할 수 있으므로 생산성이 높아진다.
- **유지보수 용이**
  - MyBatis에서는 DB 테이블의 컬럼이 변경되면, 데이터를 제어하는 DAO에서 개발자가 일일히 전부 수정해야했지만, JPA는 그런 일을 개발자 대신 처리해준다.
- **DB 벤더(MySQL, Oracle..)에 종속되지 않음**
  - JPA는 어느 벤더에 종속되는 형태가 아니므로 유연하게 DBMS를 바꿀 수 있다.

<br>**Hinernate의 단점**

- **성능 이슈**
  - 직접 SQL을 작성하지 않고 객체로 쿼리를 수행하는 것은 [JPA](#structure-of-jpa)의 구조에서도 알 수 있듯이 중간에 과정을 하나 더 거치는 작업을 수행하기 때문에 아무래도 성능에 영향을 미치는 것 같다.
    ORM 초기엔 성능 이슈가 많았지만, 이후 계속 발전하여 지금은 나아졌지만 여전히 직접 SQL 쿼리를 작성하는 것보다는 성능 이슈가 존재할 수 있다고 한다.
  - 국내 시장이 Hibernate와 같은 JPA 대신 MyBatis를 많이 쓰는 이유도 성능 때문일 수 있다고 한다. 국내 시장의 특성상 금융/SI가 많은데 이들 영역에서는 성능이 떨어지고, 세밀한 제어가 어려운 JPA대신 SQL 쿼리를 직접 작성하는 것으로 보인다.
- **세밀한 제어의 어려움**
  - 객체(메서드 호출)로 DB를 제어하는 것이기 때문에 세밀한 부분의 제어가 힘들다고 한다. 
  - 쿼리가 복잡해질수록 JPA를 통한 쿼리제어의 세밀함은 떨어질 수 있다.
- **높은 러닝커브**
  - SQL 쿼리를 직접 작성하는 MyBatis 대비 JPA는 SQL 외 추가로 학습을 해야하기 때문에 러닝커브가 높다고 한다. 

<br>

**Reference**

- [victolee93 - [Spring JPA] ORM과 JPA 그리고 Hibernate](https://victorydntmd.tistory.com/195)

<br>

# <a name="git"></a>Git



<br>

# <a name="devops"></a>DevOps



<br>

## <a name="aws"></a>AWS

**우분투 EC2 인스턴스에 jdk 설치하기**

- `sudo apt install default-jdk`

  - 구버전 설치할 경우, [Oracle Java Archive](https://www.oracle.com/technetwork/java/archive-139210.html)에서 버전을 찾아서 설치.

- `ssh -i [aws-public-key].pem ubuntu@[ip-port@aws]`

  - AWS 서버를 실행할 때마다 ip주소가 바뀐다. 바뀐 ip주소를 입력해야 정상적으로 AWS 웹서버에 접속할 수 있다.

    

<br>

# <a name="linux"></a>Linux

리눅스는 <a href="https://github.com/torvalds" target="_blank">리누스 토발스</a>가 개발한 컴퓨터 운영체제(OS)이다. <a href="https://github.com/torvalds/linux" target="_blank">오픈소스 운영체제</a>이며, 다중 사용자, 다중 작업(멀티태스킹), 다중 스레드를 지원하는 네트워크 운영체제라고 한다.

리눅스를 운영체제라고 했지만, 정확히는 운영체제라기보다 리눅스 커널이라고 하는게 맞다. 그러나 통상적으로 리눅스 커널과 우분투, 페도라와 같은 운영체제들도 리눅스라고 칭하고 있다.

리눅스의 역사나 배경에 대해서도 차후 더 알아보고 정리해야 할 것 같다.

<br>

## <a name="command-of-linux"></a>명령어

- **find**

**리눅스에서 파일이나 디렉토리를 검색**할 때 사용하는 명령어이다.

경로 Desktop/test 에서 용량 3mb 미만의 파일을 콘솔에 출력할 때 다음과 같이 명령한다.

`$ find Desktop/test -size -3M -type f`

경로 Desktop/test 에서 용량 10mb이상의 디렉토리를 `ls -l` 형태로 출력할 때 다음과 같이 명령한다.

`$ find Desktop/test -size +10M -type d -exec ls -l {} \;`

<br>

- **심볼릭 링크 생성/사용하기**

심볼릭 링크는 디렉토리 또는 파일에 더 빠르게 접근하기 위한 별명을 설정하는 일과 같다. `디렉토리 --심볼릭링크`

`ln -s [target] [symbolic_link_name]`

<img src="http://www.mediafire.com/convkey/1fa6/at0glqvdxyrry4czg.jpg" width="700" />