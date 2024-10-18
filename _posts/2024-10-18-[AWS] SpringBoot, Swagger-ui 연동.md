---
title : "[AWS] SpringBoot, Swagger-ui 연동"
date : 2024-10-18 21:19:00 +0900
categories : [AWS, Deployment]
tags : [aws] #소문자만 가능
toc: true
toc_sticky: true
published : true
---
# [AWS] SpringBoot, Swagger-ui 연동

## 1. build.gradle 의존성 추가
```gradle
dependencies {
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.4'
}
```

## 2. application.yml 파일 수정
하단에 해당 부분을 추가하여준다.
```yml
springdoc:
  swagger-ui:
    groups-order: DESC
    tags-sorter: alpha
    operations-sorter: method
    disable-swagger-default-url: true
    display-request-duration: true
    defaultModelsExpandDepth: 2
    defaultModelExpandDepth: 2
    path: /swagger-ui/index.html
  api-docs:
    path: /api-docs
  show-actuator: true
  default-consumes-media-type: application/json
  default-produces-media-type: application/json
  writer-with-default-pretty-printer: true
  model-and-view-allowed: true
  paths-to-match:
    - /api/v1/**
```

## 3. SwaggerConfig 클래스 생성
```java
import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import org.springdoc.core.models.GroupedOpenApi;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SwaggerConfig {

    @Bean
    public GroupedOpenApi publicApi() {
        return GroupedOpenApi.builder()
                .group("springdoc-public")
                .pathsToMatch("/**")
                .build();
    }

    @Bean
    public OpenAPI openAPI() {
        Info info = new Info()
                .version("v1.0")
                .title("TEST")
                .description("Swagger-ui 테스트입니다.");
        return new OpenAPI()
                .info(info);
    }
}
```


![](2024-10-18-%5BAWS%5D%20SpringBoot,%20Swagger-ui%20%E1%84%8B%E1%85%A7%E1%86%AB%E1%84%83%E1%85%A9%E1%86%BC/image.png)

## ✨  접속 성공