---
description: Optional<>
---

# optional

1. Optional Null 처리를 할때 사용.
2. Optional.of  - value 가 null 인경우 예외를 던진다 \( 반드시 값이 필요한 객체인 경우 사용\)
3. Optional.ofNullable - value가 null인경우 빈값의 Optional을 뱉는다.

```text
public Optional<User> findbyId(Long seq) {
		
		StringBuilder sql = new StringBuilder();
		
		sql.append("select seq");
		sql.append("	  ,email");
		sql.append("	  ,passwd");
		sql.append("	  ,login_count");
		sql.append("	  ,last_login_at");
		sql.append("	 ,create_at");
		sql.append(" from users");
		sql.append(" where seq = ?");
		
		try {
			// 회원이 존재 하지 않을때의 예외처리 Optional.of( 값이 존재하면 값을 감싸는 Optional 반환 , 값이 null 이면 NullPointerException 반환)
			return Optional.of(jdbc.queryForObject(sql.toString(), this::mapRowToUser, seq));
		}catch (Exception e) {
			return Optional.empty();
		}
	}
	
	
	userRepo.findbyId(seq)
		        .orElseThrow(() -> 
                     new IllegalStateException("존재하지 않는 회원입니다."));
```

4. orElse : 옵셔널 객체가 비어있다면 기본값으로 제공할 객체를 지정 

5.orElsethrow : 옵셔널 객체가 비어 있다 예 외 공급자 함수를 통해 예외 발

