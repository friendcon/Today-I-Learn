# MyBatis 의 동적 태그들

### <if>

test라는 속성과 함께 특정 조건이 true가 되었을 때 포함된 SQL을 사용하고자 할 때 사용한다. 

다음과 같이 사용하면 된다. 

```xml
<if test="type == 'T'.toString()">
	(title like '%'||#{keyword}||'%')
</if>
<if test="type == 'C'.toString()">
	(content like '%'||#{keyword}||'%')
</if>
<if test="type == 'W'.toString()">
	(writer like '%'||#{keyword}||'%')
</if>
```

### <choose>

여러 상황들 중 하나의 상황에서만 동작한다. if~else 나 jstl의 choose와 유사하다

```xml
<choose>
<when test="type == 'T'.toString()">
	(title like '%'||#{keyword}||'%')
</when>
<when test="type == 'C'.toString()">
	(content like '%'||#{keyword}||'%')
</when>
<when test="type == 'W'.toString()">
	(writer like '%'||#{keyword}||'%')
</when>
<otherwise>
	(title like '%'||#{keywork}||'%' OR content like '%'||#{keyword}||'%')
</otherwise>
</choose>
```

otherwise는 위으 모든 조건을 충족하지 않는 경우 실행된다. 

### <trim>, <where>, <set>

`**where`** 의 경우 태그 안쪽에서 SQL이 생성될 때 `**where`** 구문이 붙고 그렇지 않은 경우는 생성되지 않는다. 

- where  예제

```xml
select * from tbl_board
<where>
	<if test="bno != null">
		bno = #{bno}
	</if>
</where>
```

bno가 null이 아닌 경우 select * from tbl_board where bno = #{bno} 가 실행되고 bno가 null인 경우

select * from tbl_board 가 실행된다.

`**trim`** 의 경우 하위에서 만들어지는 SQL문을 조사해서 앞쪽에 추가적인 SQL을 넣을 수 있다.

```xml
select * from tbl_board
	<where>
		<if test="bno != null">
			bno = #{bno}
		</if>
		<trim prefix="and">
			rownum = 1
		</trim>
	<where>
```

bno가 존재하는 경우 select * from tbl_board where bno=#{bno} and rownum = 1이 실행된다.

bno가 존재하지 않는 경우 select * from tbl_board where rownum = 1이 실행된다.  

### <foreach>

List, 배열, 맵 등을 이용해서 루프를 처리할 수 있다. 주로 IN 조건에서 많이 사용하지만 복잡한 WHERE 조건을 만들 때에 사용한다.