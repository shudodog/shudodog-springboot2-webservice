# shudodog-springboot2-webservice
http://ec2-3-38-82-54.ap-northeast-2.compute.amazonaws.com/

![image](https://user-images.githubusercontent.com/76150392/130751151-463ce1e3-a4a2-43dc-ab37-05143f2c1ad0.png)
![image](https://user-images.githubusercontent.com/76150392/130751238-69c6ac1c-50af-4ef1-aa1f-e84fc81ffdca.png)
![image](https://user-images.githubusercontent.com/76150392/130751334-f48ef1c9-821c-4c07-9c9d-a6476bb482d2.png)
![image](https://user-images.githubusercontent.com/76150392/130751446-c7a9f660-b9d8-4422-87f7-688880e5cd3d.png)
![image](https://user-images.githubusercontent.com/76150392/130751490-4aad6284-8652-4748-bf6d-43a5605d8979.png)
![image](https://user-images.githubusercontent.com/76150392/130751763-c8074e00-43ef-4bc8-9e1a-a632b3b66827.png)



이 프로젝트를 진행한 이유?
-세연넷이라는 연세대학교 커뮤니티가 있는데 접속자 수가 적고 서울대의 스누라이프, 고려대의 고파스에 비해 사이트가 활발하지 못하였다.
또한 매번 같은 글들(로스쿨, 변호사, 의치한 등등) 만 올라오는데 남과의 비교만 하고 의사가 아니면 별로다 라는 글만 계속 올라와서 사이트를 아예
내가 새로운 연세대학교 커뮤니티를 만들어야겠다는 생각이 들었다.
고파스나 스누라이프 같은 커뮤니티를 만들기 위해서는 기존 세연넷에
1. 대학원생 유입을 허용
2. 앱개발 + 시간표 및 강의평가를 활성화
3. 앱을 통한 댓글 알림
4. 특정 유저 차단 허용
의 기능을 넣어야 한다.

하지만 이번 프로젝트에서 한번에 저것들을 다 할 수 없기 때문에 
-게시판 기능 : 게시글 조회, 게시글 등록, 게시글 수정, 게시글 삭제
-회원 기능 : 구글/네이버 로그인, 로그인한 사용자 글 작성 권한, 본인작성 글에 대한 권한 관리
를 할 수 있도록 웹사이트를 만들었다.

프로젝트를 하면서 어려움을 느낀 점
1. 테스트 코드를 작성하고 난 후 마지막 test를 돌릴때 오류가 떳는데 개별적으로 test할때는 오류가 안떳는데 gradle안에서 할때 오류가 뜸

2. 데이터베이스 연결 문제 : intellij의 database navigator plugins를 설치하고 DB Browser와 연결이 되지 않아서 intellij를 업그레이드 시키고 하였다.
3. Amazon Linux에서 vim사용법을 몰라 오류가 많이 떳는데 vim 사용법을 제대로 익혔다.
4. deploy.sh실행후 재실행하면  build 오류가 뜸 > jar파일이 중복되어서 있었던 문제(linux에 git연동부터 다시 하여서 알아내었다. git을 처음 clone한후 실행하면
잘 되었는데 2번째 부터 안된다느 ㄴ사실을 계속 다시 git연동부터 처음부터 다시 하니깐 깨달았다.) 먼저 깔려있던 jar이 8080포트를 이미 이용하고 있어서 톰캣이 실행이 안되었다. cmd창에서 이미
8080이 이용되고 있다는 사실을 알았고 그래서 처음 build를 할때 있던 jar파일을 다 삭제한 후 실행하였다.
5. travis연동후 배포했을때 travis에서 build는 다 됐다고 (서버 배포는 성공)되었다고 뜨지만 white label error가 떴다. 에러에 대해 구글링 하니
서버는 실행되어 배포되지만 database문제라고 하였다. 다시 에러를 천천히 읽어보니 sql result값을 가져오지 못한다는 것이었다.
그래서 내가 sql을 database navigator > DB Browser로 연결하지 않아서 에러가 뜨는 것이라 착각했다. 하지만 linux에서 nohup.out을 vim으로 열어
linux cmd창에 어떤 에러가 있는지 봣더니 sql table에 없는 값이라는 에러 메시지가 있었다. 내가 sql console창에 테이블 명을 등록할때 오타가 있었다는 걸 발견했고,
다시 수정해서 sql table을 만들었더니 정상적으로 웹페이지가 실행되었다. 여기서 나는 일단 에러가 나면 console창을 확인하는 것이 우선이라는 걸 배웠다.
평소에 뇌피셜로 어디가 잘못됐을까 추측하고 구글링하는데, 일단 정확히 어떤 부위에서 에러가 났는지 console창을 일일이 확인하는 것이 중요하다.

Spring boot, Java 8, Gradle 4.10.2, Mustache, Amazon Linux2 AMI, JUnit4
저장소 : mavenCenteral, jcenter


테스트 코드 작성법: 실패테스트(red) > 통과하는 프로덕션 코드(green) > 프로덕션 코드 리펙토링(refactor)
내장 WAS 사용 , 언제 어디서나 같은 환경에서 스프링 부트를 배포할수 있어서
모든 응답: dto패키지

JPA라는 자바 표준 ORM : 서로 지향하는 바가 다른 2개 영역을 중간에서 패러다임 일치시킴시켜 SQL애 종속적인 개발을 하지 않아도 된다, 더 객체지향형
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
