`at.favre.lib.bcrypt` 라이브러리를 사용하여 비밀번호 해싱을 수행하는 방법은 다음과 같습니다. 먼저, Gradle에 의존성을 추가해야 합니다. `build.gradle` 파일에 다음과 같은 의존성을 추가하면 됩니다:

```groovy
dependencies {
    implementation 'at.favre.lib:bcrypt:0.9.0'
}
```

이제 비밀번호를 해싱하고 해싱된 비밀번호를 검증하는 방법은 다음과 같습니다:

**비밀번호 해싱:**

```java
import at.favre.lib.crypto.bcrypt.BCrypt;

public class BcryptExample {

    public static void main(String[] args) {
        String originalPassword = "password123";

        // 'hashToString'는 Salt와 함께 해시를 생성합니다.
        String hashedPassword = BCrypt.withDefaults().hashToString(12, originalPassword.toCharArray());

        System.out.println(hashedPassword);
    }
}
```

**해시 검증:**

```java
import at.favre.lib.crypto.bcrypt.BCrypt;

public class BcryptExample {

    public static void main(String[] args) {
        String originalPassword = "password123";
        String hashedPassword = "$2a$12$TjIe1.Yv1eZbxKUG..OvQO.8Z7Yy6S7oUs06.7fZ5y9AIvGiIuNS.";

        // 'verifyer()'를 사용하여 해시를 검증합니다. 이 메서드는 'BCrypt.Result'를 반환합니다.
        BCrypt.Result result = BCrypt.verifyer().verify(originalPassword.toCharArray(), hashedPassword);

        // 'verified'는 해시가 원본 비밀번호와 일치하면 true를 반환합니다.
        boolean passwordVerified = result.verified;

        System.out.println(passwordVerified ? "Password is correct" : "Password is incorrect");
    }
}
```

위의 예제에서 `hashToString`의 첫 번째 인자는 원하는 해시의 strength(cost factor)를 정의합니다. 이 값은 4~31 사이의 값을 가질 수 있으며, 값이 클수록 해시 생성에 더 많은 시간이 소요되며, 이는 무차별 대입 공격에 대한 저항력을 높입니다. 일반적으로는 10~14 사이의 값이 권장되지만, 시스템의 성능과 보안 요구사항에 따라 조정해야 할 수도 있습니다.
