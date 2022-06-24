 히카리풀 사용시 나타나는 오류가 있다.

그것은 바로 

***hikari-pool - Failed to validate connection***

![image](https://user-images.githubusercontent.com/85658845/175467438-e1eabf8e-ed0e-4bc5-b621-6e7056651962.png)

로그의 내용을 의역하면 아래와 같습니다.

- Hikari pool의 connection을 validate하는데 실패 했다.
- 이미 close된 connection에 어떤 operation을 하는것은 안된다.
- HikariPool의 maxLifetime 값을 짧게 하는 것을 생각해봐라

### 무슨의미 일까?
요약하자면, connection을 갱신하고자 하는데 이미 닫힌 커넥션이라 어떤 행위도 할 수 없다. 입니다.
여기서 중요한건 HikariConfig의 MaxLifetime과 MySQL의 wait_timeout의 상관관계를 알아야 합니다.

## Hikari Pool의 MaxLifetime

>This property controls the maximum lifetime of a connection in the pool.  
>An in-use connection will never be retired, only when it is closed will it then be removed.  
>On a connection-by-connection basis, minor negative attenuation is applied to avoid mass-extinction in the pool.  
>We strongly recommend setting this value, and it should be several seconds shorter than any  
>database or infrastructure imposed connection time limit.   
>A value of 0 indicates no maximum lifetime (infinite lifetime),  
>subject of course to the idleTimeout setting. Default: 1800000 (30 minutes)

구글번역기로 대충 돌려보면..

- MaxLifetime은 Hikari pool에서 Connection이 살아 있을 수 있는 시간
- 현재 사용중인 Connection은 종료하지 않고 이미 닫혀 있는 경우에만 제거
- Connection을 한번에 대량으로 종료하고 생성하면 비용이 많이 듬 (실제로 2.5%의 유격으로 maxLifetime이 Connection에 설정됨)
- Database에 설정된 Connection time limit 보다 짧아야 한다.
- 0으로 설정하면 무한으로 Connection이 살아있음
- default 180000ms (= 30분)

Hikari Pool 내부적으로 Connection의 life time을 관리하는 속성입니다.

maxLifetime은 최소 30초 이상으로 설정하여야 합니다. (안그러면 180000ms로 설정)

이다.

당황하지 말고 기다리자 그럼 다시 연결될것이다.
