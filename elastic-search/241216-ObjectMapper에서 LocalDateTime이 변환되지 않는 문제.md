## ObjectMapper에서 LocalDateTime이 변환되지 않는 문제

## 목차

1. [문제](#문제)
1. [원인](#원인)
1. [문제 해결 방법](#문제-해결-방법)
1. [References](#references)

## 문제

- 직렬화/역직렬화 시 ObjectMapper를 사용중
- 이때 JSON에서 자바 객체로 역직렬화 시 LocalDateTime 필드가 정상적으로 변환되지 않고 오류가 발생

```bash
Java 8 date/time type `java.time.LocalDateTime` not supported by default: add Module "com.fasterxml.jackson.datatype:jackson-datatype-jsr310" to enable handling
```

## 원인

## 문제 해결 방법

ElasticSearch Client Configuration에 아래 코드 추가 

- before: `new JacksonJsonpMapper()`
- after: `new JacksonJsonpMapper(objectMapper())`

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper objectMapper = new ObjectMapper();
    objectMapper.registerModule(new JavaTimeModule());
    return objectMapper;
}

@Bean
public ElasticsearchTransport elasticsearchTransport() {
    return new RestClientTransport(elasticRestClient(), new JacksonJsonpMapper(objectMapper()));
}
```

- `build.gradle`에 의존성 추가

```groovy
implementation 'com.fasterxml.jackson.datatype:jackson-datatype-jsr310:2.14.0'
```




## References

- [[Spring] ObjectMapper에서 LocalDateTime이 변환되지 않는 문제](https://woo-chang.tistory.com/75)
