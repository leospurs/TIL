# Optional
자바8부터 제공하며 Optional<T> 클래스를 사용하여 NPE를 방지할 수 있도록 도와준다. 
Optional<T>는 Wrapper 클래스로 null 값이 들어와도 NPE가 발생하지 않는다.

# Optioanl의 orElse, orEsleThrow
Optional API가 제공하는 함수 중에는 orElse와 orElseThrow가 있다.
orElse는 앞의 인자가 null일 때 안에 있는 내용을 실행시키고, 
orElseThrow는 앞의 인자가 null일 때 예외처리를 시킨다.

주로 Spring Data JPA에서 return 값에 대한 처리를 하는데 적극 활용된다.

[Spring Data JPA에서의 활용 예시]

```java
private void saveRfToken(Long userId, String newRfToken) {
        RfToken rfToken = rfTokenRepository.findByUserId(userId)
                .map(entity -> entity.update(newRefreshToken))
                .orElse(new RfToken(userId, newRefreshToken)); // findByUserID에서 반환한 값이 null이면 RfToken 객체 생성하여 rfToken값에 할당
        refreshTokenRepository.save(refreshToken);
    }

public User findById(Long userId) {
        return userRepository.findById(userId)
                .orElseThrow(() -> new IllegalArgumentException("unexpected User!!")); // findById에서 반환한 값이 null이라면 IllegalArgumentException 발생
    }
```



