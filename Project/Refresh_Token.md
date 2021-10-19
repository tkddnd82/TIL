## Refresh Token
개념: Access Token이 만료되었을 때, Refresh Token을 이용해 재인증의 과정없이 Access Tokne을 새로 발급해준다.
Access Token의 유효기간을 길게하면 보안에 취약해진다.(탈취 당하기 쉬움)
그래서 Access Token의 유효기간은 짧게하여 공격 면적을 줄이고, Refresh Token의 유효기간을 길게 설정해 보안의 취약점을 보완한다.
Refresh Token은 서버 상에서 관리한다.(서버상에서 삭제, 재발급 가능)

## 장단점
장점
- Acess Token과 Refresh Token의 유효시간을 달리해서 보안성을 높일수 있다.
단점
- 구현이 복잡하며, Access Token을 새로 발급하는 과정에서 Http 요청 횟수가 늘어나 자원 낭비가 발생한다.

## 전체 Flow
1.사용자가 로그인을 한다. 
2.서버는 사용자에 대한 검증을 통해서 올바른 유저라면 Access Token과 Refresh Token을 발급한다, 이때 Refresh Token 은 서버에 저장한다.
3.사용자는 Access Token 을 이용해 데이터를 요청한다.
4. 서버에서 Acess Token에대한 유효성을 검증하고 유효한 토큰이라면 데이터를 제공한다.
만약 만료된 Access TOken이라면 Refresh Token을 자동적으로 발급하게되어서 사용자는 Refresh Token을 
이용해서 데이터를 요청한다 (이때 서버에 저장된 Refreshe Token과 일치여부 확인)
최종적으로 유효하다면 데이터를 제공한다.
