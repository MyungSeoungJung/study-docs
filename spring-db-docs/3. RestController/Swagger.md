### 공식문서

https://springdoc.org/

### Gradle에 의존성 추가

```groovy

// https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-starter-webmvc-ui
implementation group: 'org.springdoc', name: 'springdoc-openapi-starter-webmvc-ui', version: '2.2.0'

```

### URL 테스트

http://localhost:8080/swagger-ui/index.html

### 버전 및 설명 추가

@Configuration
class OpenApiConfig {

    @Bean
    public OpenAPI openAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("MYAPP application API")
                        .version("v1.0")
                        .description("MYAPP application API"));
    }

}

### API별 설명 추가

-- 컨트롤러 클래스에 추가한다.

```java
@Tag(name="연락처 관리 처리 API")
```

-- 컨트롤러 메서드 마다 설명을 추가한다.

```java
@Operation(summary = "연락처 목록 페이징 조회")
```

### Swagger에 인증처리 추가

- OpenApiConfig에 설정 추가

```java
        return new OpenAPI()
                .info(new Info()
                        .title("MYAPP application API")
                        .version("v1.0")
                        .description("MYAPP application API"))
                .components(
                        new Components().addSecuritySchemes("bearer-key",
                                new SecurityScheme().type(SecurityScheme.Type.HTTP).scheme("bearer").bearerFormat("JWT"))
                        );
```

- 컨트롤러의 인증처리가 필요한 메서드에 추가

```java

@Operation(security = { @SecurityRequirement(name = "bearer-key") })

```
