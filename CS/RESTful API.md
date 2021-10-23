## REST란?
### REST정의
“Representational State Transfer” 의 약자
자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.
REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
### REST의 구체적인 개념
HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
- CRUD Operation
Create : 생성(POST)
Read : 조회(GET)
Update : 수정(PUT)
Delete : 삭제(DELETE)
HEAD: header 정보 조회(HEAD)
### REST 특징
- Server-Client(서버-클라이언트 구조)
자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
서로 간 의존성이 줄어든다.
- Stateless(무상태)
HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
Client의 context를 Server에 저장하지 않는다.
즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
각 API 서버는 Client의 요청만을 단순 처리한다.
즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.
- Cacheable(캐시 처리 가능)
웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.

##REST API란?
- 정의: REST 기반으로 서비스 API를 구현한 것을 말한다.
- API(Application Programming Interface): 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것
- RESTful 특징: API 이해에 따른 일관성 유지, 컨벤션 유지를 위한 것이며 이해하기 쉽고 사용하기 편하다.
