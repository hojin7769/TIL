# 마이바티스 설정

> ## 개발툴
>   1. sts4
>   2. JDK11
>   3. MSSQL
>   4. Gradle

## 1.
처음으로 appilcation.yml 에 마이바티스 관련 설정 추가하기

![image](https://user-images.githubusercontent.com/85658845/174263068-c4e84df2-ebfb-4d41-a96d-d23b2559ebbf.png)

위와 같이 mapper를 넣을 곳을 설정해 준다
mapper/** 로 설정한 이유는

yml이 빌드 될때 리소스 파일 부터 읽기 때문에 src/main/resource/mapper 같이 안적어도 가능하다

## 2. 

두번째로 할 작업은 기존에 만들었던 dao 파일을 제거 하고 그 자리에 mapper 패키지와 인터페이스 파일 생성

![image](https://user-images.githubusercontent.com/85658845/174263652-662b5d82-1614-48d9-bf3f-41040986bd09.png)

***생성후 @Mapper 어노테이션 꼭 붙여야 한다***

## 3.

세번째 할 작업은 리소스 파일에 xml 파일 생성 이때 mapper라는 패키지 안에다가 생성해야 한다.

![image](https://user-images.githubusercontent.com/85658845/174264046-5166dc55-4d3f-49a5-9f2a-92dcb5a616f9.png)

## 4.

마지막으로 xml파일 안에 마이바티스에서 쓰는 쿼리문 생성


```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.demo.mapper.BoardMapper">
    <select id="list" resultType="java.util.LinkedHashMap">
        select * from BT_BOARD order by DT_INSERT desc
    </select>
    
    <select id="detail" resultType="java.util.LinkedHashMap">
    	select * from BT_BOARD where NO_SEQ = #{NO_SEQ}
    </select>
    
    <insert id="insert" useGeneratedKeys="true" keyProperty="NO_SEQ">
    	insert into BT_BOARD (ID_USER, DS_TITLE, DS_CONTENT) values (#{ID_USER}, #{DS_TITLE}, #{DS_CONTENT})
    </insert>
    
    <update id="update">
    	update BT_BOARD set ID_USER = #{ID_USER}, DS_TITLE = #{DS_TITLE}, DS_CONTENT = #{DS_CONTENT}, DT_UPDATE = getdate() where NO_SEQ = #{NO_SEQ}
    </update>
    
    <delete id="delete">
    	delete from BT_BOARD where NO_SEQ = #{NO_SEQ}
    </delete>
    
</mapper>
```
필자는 이렇게 작성 하였다.

***!!!중요!!! 이 쿼리 아이디와 인터페이스 메서드 이름과 같아야 한다***

