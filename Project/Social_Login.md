## Front Flow
- Front에서 카카오 로그인을 통해서 토큰을 받을수 있는 코드를 받고 이 코드를 통해서 API를 호출할수 있는 사용자 토큰(Acess Token, Refresh Token)을 카카오로 부터 받아온다.
- 카카오로 부터 받은 사용자 토큰을 headers에 담아서 Back-end에 보내준다.


## Back-end Flow
### 사용자 정보 Request
![](https://images.velog.io/images/tkddnd82/post/a3dba65d-d67b-4068-95e6-d20dc6a2f744/image.png)![](https://images.velog.io/images/tkddnd82/post/24c1353b-725c-426c-8e68-e29cedc54e94/image.png)
- Requet: Front에서 headers에 토큰을 담아서 주면 {Authorizat
ion: bearer+access_token}의 양식으로 kakao에 사용자 정보 reqeust를 보낸다.
(1):Fron트에서 토큰 받기
(2):headers에 토큰 담아 요청 보내기
(3):kakao_id 가져오기
(4):kakao_account 가져오기
(5):nickname 가져오기
```
access_token = request.headers.get("Authorization")				 -->(1)
			
if not access_token:
	return JsonResponse({"message" : "INVALID_TOKEN"}, status = 400)
response = requests.get(										-->(2)
	"https://kapi.kakao.com/v2/user/me", 
	headers = {"Authorization" : f"Bearer {access_token}"
	)
if not response:
	return JsonResponse({"message" : "NOT_FOUND_IN_KAKAO"}, status = 404)

	profile_json  = response.json()
       
	kakao_id      = profile_json.get("id")						-->(3)
	kakao_account = profile_json.get("kakao_account")-			-->(4)
	nickname          = kakao_account["profile"]["nickname"]	-->(5)

```

- 카카오로부터 받는 Response 객체 받은 정보를 json으로 변환 결과
카카오 정보 가져옴(해체버전)
```
{
 'id': 1855599935, 
 'connected_at': '2021-08-18T08:54:05Z', 
 'properties': 
    {
        'nickname': '한효주'
    }, 
 'kakao_account': 
        {'profile_nickname_needs_agreement': False, 
         'profile': 
            {'nickname': '한효주'}, 
         'has_email': True, 
         'email_needs_agreement': False, 
         'is_email_valid': True, 
         'is_email_verified': True, 
         'email': 'hyojoo@gmail.com'
        }
    }
```


- 받은 정보를 바탕으로 험블버그 시스템에 적용
```
if not User.objects.filter(kakao = kakao_id).exists():  -->(1)
	User.objects.create(
				kakao     = kakao_id,
				nickname      = name,
	)

user           = User.objects.get(kakao = kakao_id)
user.name      = name
user.save()

token = jwt.encode({"id" : user.id}, SECRET_KEY, algorithm = "HS256")
			
		return JsonResponse({"message" : "SUCCESS", "acess_token" : token}, status = 200)
		except KeyError:
		return JsonResponse({"message" : "KEY_ERROR"}, status = 400)
```
(1):험블버그 데이터베이스와 유저정보 비교(존재여부 확인)후 존재하지 않으면 새로운 유저정보 생성후 저장하꼬 토큰 발행

위의 Flow를 통해서 잘 했다면, 로그인 후에 success메시지와 함께 access_token 반환.
![](https://images.velog.io/images/tkddnd82/post/ef656193-1db8-4dce-8a0c-b5e8a58ac0a9/%EC%86%8C%EC%85%9C%EB%A1%9C%EA%B7%B8%EC%9D%B8%20%EC%97%91%EC%84%B8%EC%8A%A4%20%ED%86%A0%ED%81%B0.jpg)

The end!!!!

>- Comment
>
>프,백 모두 소셜로그인이 처음이다 보니 맞춰가는 과정에서 사소한 bloker들이 발생했었다.
조그만한 인적 요소들의 오류였지만 그래도 실수를 반복하지 않자는 의미에서 아래에 간다하게 
정리하겠음.

>- blocker 
>1. 프런트로 부터 인증토큰 받기 실패
해결: 인가코드를 받고 인증토큰을 발급받고 백엔드가 해당 인증토크을 받으면 되는데 Flow가 처음  이다 보니 인가코드를 인증토큰으로 이해해서 백엔드에 넘기려다보니 오류발생.
>
>
2. 1번 blocker해결후 인증토큰을 받는 과정에서 평소 자주 만나는 404오류와 만남
해결: 프런트 headers에 토큰을 담아야하는데 header에 담아서 오류생김, 본인도 헤더와 헤더스에 구별을 정확히 생각하지 못함.
>
>
3. 2번 blocker해결후 가끔 만나는 500오류와 만남
해결: 본인이 name을 nickname으로 수정후 해결. 










