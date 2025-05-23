---
aliases:
  - JWT
tags:
  - JWT
author: Min Jo
created: 2025-05-02
---
---
### JWT(Json Web Token) 방식 인증의 일반적인 흐름

#### 1.토큰 요청 
- 먼저 POST 요청을 통해 로그인 또는 인증을 수행하고, 인증 정보를 제공하여 JWT 토큰을 받습니다.
#### 2.토큰을 이용한 인증
- 이후 이 토큰을 HTTP 요청의 Authorization 헤더에 담아서 서버에 요청을 보낸다. (권한을 달라는건가 ?)
- Authorization: Bearer (Bearer은 무슨뜻인거지?)
#### 3.검증
- 서버는 요청이 들어올 때마다 JWT 토큰을 검증하고, 토큰이 유효하다면 요청을 처리한다.
- JWT 토큰은 보통 **만료 시간**이 포함되어 있기 때문에 만약 만료되었거나, 서버에서 검증이 실패하면 **401 Unauthorized** 에러가 발생할 수 있습니다.

### 🔒 장점

- **아이디/비밀번호 노출 위험 감소**: 매 요청에 민감 정보를 보내지 않아 보안이 향상됩니다.
- **토큰 기반 인증이므로 무상태(stateless)**: 서버가 세션을 관리할 필요 없이, 토큰 자체에 사용자 정보가 포함됨.
- **API Gateway, Microservice 구조에서 유리**: 한 번 받은 토큰으로 여러 서비스에서 인증 처리 가능.

---
### ✅ 비교: 세션 방식 vs JWT 방식

| 구분           | 세션 기반 인증                                       | JWT 기반 인증                                           |
| ------------ | ---------------------------------------------- | --------------------------------------------------- |
| **서버 상태 유지** | 사용자마다 세션 정보를 **서버 메모리나 DB에 저장**해야 함 (stateful) | 서버는 사용자 정보를 **보관하지 않음**, 토큰 자체가 정보를 포함함 (stateless) |
| **스케일링**     | 서버 간 세션 동기화 필요 → 복잡                            | 어느 서버든 동일한 JWT만 있으면 인증 가능                           |
| **속도/부하**    | 세션 확인을 위해 서버 리소스 사용                            | 서버는 JWT 서명만 검증하면 됨 (빠름)                             |
| **보안**       | 세션 탈취 시 위험 (HTTPS 필요)                          | 토큰 탈취 시 위험, 만료 시간 설정 필요                             |
| **관리 포인트**   | 로그아웃/세션만료 따로 관리                                | 토큰에 **만료 시간**이 포함되어 자체 관리 가능                        |

---

### 🔐 SSO에서 어떻게 가능한가?

SSO는 “한 번 로그인하면 여러 서비스에서 인증된 것처럼 동작”하게 해주는데, 이게 가능한 이유는:

1. **중앙 인증 서버(Identity Provider, 줄여서 IdP)**가 존재하고
2. 사용자가 로그인하면, IdP가 **토큰(JWT 또는 SAML, OAuth 토큰 등)**을 발급
3. 이 토큰을 각 웹 서비스(서비스 제공자, SP)가 받아 인증된 사용자로 인정
    
---
### ✅ 어떤 기술들이 쓰이냐면:

|프로토콜|설명|토큰 형식|
|---|---|---|
|**SAML**|기업용 SSO에서 전통적으로 많이 사용됨|XML 기반|
|**OAuth2.0 + OpenID Connect**|현대적인 웹, 모바일 앱에서 많이 사용|JWT 기반|
|**JWT (JSON Web Token)**|자체적으로도 인증에 쓰일 수 있고, 위 프로토콜에서 내부적으로 사용됨|JSON 기반|

## 🔐 왜 Refresh Token과 Access Token을 나눴을까?

|구분|역할|
|---|---|
|**Refresh Token**|오랫동안 유효함. Access Token을 재발급받기 위한 용도로만 사용|
|**Access Token**|짧은 시간 동안 유효함. 실제 API 요청 시 사용|z
