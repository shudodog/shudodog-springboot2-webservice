# shudodog-springboot2-webservice
Spring boot, Java 8, Gradle 4.10.2, Mustache, Amazon Linux2 AMI
-게시판 기능 : 게시글 조회, 게시글 등록, 게시글 수정, 게시글 삭제
-회원 기능 : 구글/네이버 로그인, 로그인한 사용자 글 작성 권한, 본인작성 글에 대한 권한 관리
저장소 : mavenCenteral, jcenter


테스트 코드 작성법: 실패테스트(red) > 통과하는 프로덕션 코드(green) > 프로덕션 코드 리펙토링(refactor)
단위 테스트 코드 JUnit4
내장 WAS 사용 , 언제 어디서나 같은 환경에서 스프링 부트를 배포할수 있어서
모든 응답: dto패키지

JPA라는 자바 표준 ORM : 서로 짛ㅇ하는 바가 다른 2개 영역을 중간에서 패러다임 일치시킴시켜 SQL애 종속적인 개발을 하지 않아도 된다, 더 객체지향형
JPA < Hibernate < Spring Data JPA(구현체 교체의 용이성, 저장소 교체의 용이성)

ENtity클래스에서는 절대 Setter 메소드를 만들지 않는다.
H2

API:
Request 데이터를 바을 Dto
API 요청을 받을 Controller
트랜잭션, 도메인 기능 간의 순서를 보장하는 Service
비즈니스는 Domain

페이지 로딩속도를 높이기 위해 css는 header에, js는 footer에 두었다.

스프링 시큐리티와 OAuth2.0으로 로그인 기능 구현
로그인 기능을 직접 구현하면 배보다 배꼽이 더 커질수도 있기 때문이다.
어노테이션 기반으로 개선: 메소드 인자로 세션값을 바로 받을 수 있도록 함

MySQL 데이터베이스를 세션 저장소로 한다.

AWS-laas
ec2
aws-rds
MariaDB
어려웠던 점 : 데이터베이스와 rds연결하는 부분에서 database browser로 하면 안되서 intellij 버젼을 업그레이드하여 연결하였다.
database를 처음 연결해봐서 감을 잡는데 시간이 걸렸다.

Travis CI와 AWS S3, CodeDeploy연동
yml파일
버킷
EC2에 IAM역할 추가하기

nginx로 무중단 배포
엔진엑스와 스프링 부트 연동하기
profile API
real1, real2 profile로 무중단 배포
