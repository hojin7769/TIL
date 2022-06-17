# NamedParameterJdbcTemplate 
기존 사용하던 JdbcTemplate 같은 경우 우리가 데이터를 넣을 부분에 ?를 이용하여 처리를 한다.

이러한 방식은 인자 위치에 대한 순서가 강제되는데 이러한 방식은 가독성을 떨어뜨린다.

그래서 나온것이 NamedParameterJdbcTemplate 이다.

NamedParameterJdbcTemplate 는? 대신 :변수명을 이용하여 처리합으로써 순서에 강제를 받지 않는다.

```
public Map<String, Object> detail(String seq) {
		try {
			String sql = "select * from BT_BOARD where NO_SEQ = :NO_SEQ";
     SqlParameterSource namedParameters = new MapSqlParameterSource("NO_SEQ", seq);
			return jdbcTemplate.queryForObject(sql, namedParameters,Integer.class);
		} catch (EmptyResultDataAccessException ex) {
			return null;
		}
	}

```
위와 같이 입력을 하거나

```
public Map<String, Object> detail(Map<String, Object> map) {
		try {
			String sql = "select * from BT_BOARD where NO_SEQ = :NO_SEQ";
			return jdbcTemplate.queryForMap(sql, map);
		} catch (EmptyResultDataAccessException ex) {
			return null;
		}
	}
```
맵을 이용한 방법도 있다.

또한 객체를 이용한 방법도 있다.
