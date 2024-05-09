## SQLAlchemy vs psycopg2

## 목차

1. [SQLAlchemy](#sqlalchemy)
1. [psycopg2](#psycopg2)

## SQLAlchemy

- SQLAlchemy은 `ORM`임
- SQLAlchemy는 psycopg2 또는 기타 데이터베이스 드라이버에 의존하여 데이터베이스와 통신함

```bash
SQLAlchemy와 같은 ORM을 사용하면 낮은 수준의 데이터베이스 상호 작용이 추상화되어 개발자 친화적이 됩니다.
SQLAlchemy는 데이터베이스와 상호 작용하고 연결 관리를 자동으로 처리하는 Python 인터페이스를 제공하여 데이터베이스 작업을 단순화합니다.
이는 데이터 관계가 복잡하고 더 높은 수준의 추상화가 필요한 애플리케이션에 유용합니다.
```

+ 추가 ORM의 특징

```
ORM은 특정 데이터베이스의 표준에 종속되지 않고 코드를 작성할 수 있도록 유연성을 제공합니다.
ORM은 프로그래머에게 데이터베이스 독립성을 제공합니다.
예시) ORM에 object.save를 작성하면 어떤 데이터베이스가 해당 개체와 연결되어 있는지 확인하고 백엔드 데이터베이스에 따라 삽입 쿼리를 생성합니다.
```

## psycopg2

- psycopg2은 `Database Driver`임

```bash
psycopg2를 사용한 연결 풀링은 데이터베이스 쿼리 및 성능 최적화를 직접 제어해야 하는 애플리케이션에 이상적입니다.
원시 SQL 쿼리를 실행하고 연결을 세밀하게 제어해야 하는 시나리오에 적합합니다.
```

## References

- [SQLAlchemy or psycopg2?](https://stackoverflow.com/questions/8588126/sqlalchemy-or-psycopg2)
- [Optimizing Database Interaction in Web Applications: Connection Pooling with psycopg2 and SQLAlchemy ORM](https://medium.com/datauniverse/optimizing-database-interaction-in-web-applications-connection-pooling-with-psycopg2-and-c56b37d155f8)
