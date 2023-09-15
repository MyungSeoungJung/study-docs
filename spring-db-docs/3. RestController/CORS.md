WebMvcConfigurer를 사용하여 CORS 설정을 하는 방법은 스프링 프레임워크에서 Cross-Origin Resource Sharing (CORS)를 구성하는데 도움을 줍니다. 원격 호스트(클라이언트)가 다른 오리진(Origin)에서 서버의 자원에 접근하는 것을 허용하도록 설정할 수 있습니다. 로컬 호스트 origin을 추가하여 모든 경로에 대해 모든 메서드를 허용하는 방법을 아래에 설명하겠습니다.

1. Java Config를 이용하는 방법:

```java
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
@EnableWebMvc
public class WebMvcConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**") // 모든 경로에 대해
                .allowedOrigins("http://localhost") // 로컬 호스트 origin 허용
                .allowedMethods("*"); // 모든 메서드 허용
    }
}
```

2. XML Config를 이용하는 방법:

```xml
<!-- XML Configuration에서는 <mvc:cors> 요소를 사용하여 CORS 설정을 추가합니다. -->
<mvc:cors>
    <mvc:mapping path="/**" allowedOrigins="http://localhost" />
</mvc:cors>
```

이렇게 설정하면 모든 경로(`/**`)에 대해 로컬 호스트(`http://localhost`) origin에서 오는 요청을 허용하며, 모든 메서드(`allowedMethods("*")`)를 허용합니다. 따라서 클라이언트가 로컬 호스트에서 스프링 서버의 자원에 자유롭게 접근할 수 있게 됩니다.
