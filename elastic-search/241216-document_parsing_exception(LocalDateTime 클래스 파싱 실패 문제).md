## [es/index] failed: [document_parsing_exception]

## 목차

1. [에러 메시지](#에러-메시지)
1. [문제 요약](#문제-요약)
1. [기존에 문제가 발생했던 매핑 정보](#기존에-문제가-발생했던-매핑-정보)
1. [Elasticsearch의 날짜 타입](#elasticsearch의-날짜-타입)
1. [문제 해결 방법](#문제-해결-방법)
    - [인덱스 새로 생성하며 매핑 정보 변경](#인덱스-새로-생성하며-매핑-정보-변경)
1. [References](#references)

## 에러 메시지

```bash
[es/index] failed: [document_parsing_exception] [1:66] failed to parse field [createdAt] of type [date] in document with id '262175'.    
Preview of field's value: '2024-12-16T16:13:12Z'
```

## 문제 요약

- 위 에러가 발생한 이유는 `createdAt` 필드의 `LocalDateTime`가 Elasticsearch 매핑에 정의된 `date` 필드 유형과 호환되지 않기 때문

```java
@Document(indexName = "post", createIndex = false)
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor
@Builder
public class PostDocument {
    @Field(type = FieldType.Date, format = DateFormat.date_hour_minute_second)
    private LocalDateTime createdAt;

    @Field(type = FieldType.Date, format = DateFormat.date_hour_minute_second)
    private LocalDateTime updatedAt;
```

## 기존에 문제가 발생했던 매핑 정보

- SpringBoot에서 `@Document(indexName = "post")`으로 생성
- `dynamic mapping`으로 index를 생성하였더니 아래와 같이 생성됨

```json
{
  "post" : {
    "mappings" : {
      "properties" : {
        "createdAt" : {
          "type" : "date",
          "format" : "date_hour_minute_second"
        },
         "updatedAt" : {
          "type" : "date",
          "format" : "date_hour_minute_second"
        }
      }
    }
  }
}
```

## Elasticsearch의 날짜 타입

- Elasticsearch 에서 날짜 타입은 ISO8601 형식을 따라 입력을 합니다.
- 일반적으로 다음과 같은 형태로 입력된 경우 자동으로 날짜 타입으로 인식이 됩니다.
 
## 문제 해결 방법

1. 매핑을 확인하여 createdAt 필드가 올바른 date 유형인지 확인
1. 매핑이 잘못되었다면 새로운 인덱스를 생성하고 올바른 매핑을 설정
1. 데이터가 `ISO 8601` 형식이나 epoch_millis와 같은 매핑에서 지원하는 형식으로 저장되었는지 확인
1. 문제 해결 후 데이터를 재색인하거나, 잘못된 데이터 포맷을 수정하여 다시 삽입

### 인덱스 새로 생성하며 매핑 정보 변경

- 만약 매핑이 잘못되었다면, 아래처럼 새로운 매핑을 정의해야 합니다.
- 매핑은 기존 인덱스에 수정할 수 없으므로 새로운 인덱스를 생성하거나 [Reindex API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-reindex.html)를 사용해야 합니다.

```http
PUT /{{new-index-name}}
{
  "mappings": {
    "properties": {
      "createdAt": {
        "type": "date",
        "format": "strict_date_optional_time||epoch_millis"
      }
    }
  }
}
```

- `LocalDateTime` <=> `date`의 호환을 위해서는 `ES 매핑`에서 `createdAt` 필드가 다음과 같이 정의되어야 합니다.

```json
"createdAt": {
  "type": "date",
  "format": "strict_date_optional_time||epoch_millis"
}
```

- `strict_date_optional_time`은 `2024-12-16T16:13:12Z`와 같은 ISO 8601 형식을 지원합니다.
- `epoch_millis`는 Unix timestamp(밀리초)를 지원합니다.

이후 기존 데이터는 `Reindex API`를 통해 새 인덱스로 복사합니다.

```json
POST _reindex
{
  "source": {
    "index": "{{old-index-name}}"
  },
  "dest": {
    "index": "{{new-index-name}}"
  }
}
```


## References

- [7.2.3 날짜 - date](https://esbook.kimjmin.net/07-settings-and-mappings/7.2-mappings/7.2.3-date)
