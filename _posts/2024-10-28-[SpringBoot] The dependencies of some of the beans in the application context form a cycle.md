---
title : "[SpringBoot] The dependencies of some of the beans in the application context form a cycle"
date : 2024-10-28 21:51:00 +0900
categories : [SpringBoot,backend]
tags : [springboot,backend] #소문자만 가능
toc: true
toc_sticky: true
published : true
---


백앤드 개발 중 의존성 순환 참조 문제를 겪었고 해결 방법을 공유하고자 한다.

```bash
***************************
APPLICATION FAILED TO START
***************************

Description:

The dependencies of some of the beans in the application context form a cycle:

┌─────┐
|  principalOauth2UserService defined in file [/Users/keem/git/fiveguys_backend/build/classes/java/main/com/precapstone/fiveguys_backend/auth/PrincipalOauth2UserService.class]
↑     ↓
|  securityConfig defined in file [/Users/keem/git/fiveguys_backend/build/classes/java/main/com/precapstone/fiveguys_backend/config/SecurityConfig.class]
└─────┘


Action:

Relying upon circular references is discouraged and they are prohibited by default. Update your application to remove the dependency cycle between beans. As a last resort, it may be possible to break the cycle automatically by setting spring.main.allow-circular-references to true.


Process finished with exit code 1

```


```java
@Service
@RequiredArgsConstructor
public class PrincipalOauth2UserService extends DefaultOAuth2UserService {

    private final BCryptPasswordEncoder passwordEncoder;
    private final MemberRepository memberRepository;
	...
}
```


### BCryptPasswordEncoder를 새로운 @Configuration으로 등록하여 순환 고리를 해결할 수 있다.

```java
@Configuration
@EnableWebSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    private final PrincipalOauth2UserService userService;
    @Bean
    public BCryptPasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
	...
}
```
