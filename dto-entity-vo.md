---
description: 헷갈리는뎅..
---

# DTO/ENTITY/VO

**DTO** - JSON 으로 매칭 되는 것으로 URL 화면과 소통하는 데이터\(화면 데이터 파라미터,또는 리턴\)

public class EmailRequest {

private String email;

protected EmailRequest\(\) {}

}

* RequestBody 로 데이터 받을때 기본생성자가 있어야 생성이 가능. protected 선언은 사용자가 직접 사용해서 선언하지 않게 하기 위해서.. 보통 DTO은 setter 가 없고 getter 만 사용 

@PostMapping\(path = "user/join"\) public ApiResult join\(@RequestBody JoinRequest joinRequest\) { User user = userService.join\(new Email\(joinRequest.getPrincipal\(\)\),joinRequest.getUsername\(\), joinRequest.getCredentials\(\)\); String apiToken = user.newApiToken\(jwt, new String\[\]{Role.USER.value\(\)}\); return OK\( new JoinResult\(apiToken, new UserDto\(user\)\) \); }

**ENTITY**

엔티티에는 테이블 쿼리하고 매칭이되며 로직이 들어감\(validation같은..\)?



**VO**

 불변성..**equals\(\)와 hashcode\(\)** 를 오버라이딩 ... 이것도 로직이 들어가는?

