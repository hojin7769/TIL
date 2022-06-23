## KeyHolder를 이용해 자동 생성 키 값 구하기

ID 값이 AUTO_INCREMENT 인 경우, Insert 쿼리 실행 시 ID 값을 value로 직접 지정해주지 않는다. (자동으로 생성되어 삽입되기 때문에)
하지만 어떠한 엔티티를 테이블에 삽입하고 나서 그 엔티티에게 할당된 아이디 값을 전달 받고 싶은 경우 어떻게 해야 할까?
JDBCTemplate은 자동으로 생성된 키 값을 구할 수 있는 방법을 제공한다, 그게 바로 KeyHolder다.

![image](https://user-images.githubusercontent.com/85658845/175209932-b365aa04-8ab2-42d5-a2ea-b7683cb7bbbc.png)

코드에 대한 설명을 추가한다
1.GeneratedKeyHolder 객체를 생성한다. 이 클래스는 자동 생성된 키 값을 구해주는 KeyHolder 구현 클래스 이다.
2. update() 메서드는 PreparedStatmentCreator 객체와 KeyHolder 객체를 파라미터로 갖는다.
3. . PreparedStatement 객체를 생성하는데 두번째 파라미터로 Statement의 DB상에 AUTO_INCREMENT로 인해 자동으로 생성되어진 key(=id)를 가져오는 쿼리 RETURN_GENERATED_KEYS를 사용한다
4. 그다음 가져온 값을 map 에 담아 놓는다.

> Number keyValue = keyHolder.getKey();

위 insert 메서드를 실행할 때 커넥션과 pstmt를 닫아줘야 하는가?


https://stackoverflow.com/questions/20419785/does-springs-jdbctemplate-close-the-connection-after-query-timeout

잘 모르겠다. 나중에 
