# SQL - DDL

## DDL (Data Define Language, 데이터 정의어)
DB 를 구축하거나 수정할 목적으로 사용하는 언어
- `CREATE`, `ALTER`, `DROP`

``` sql
  # SCHEMA 정의
  CREATE <스키마명> SCHEMA <사용자_id>

  # DOMAIN 정의
  CREATE DOMAIN <도메인명> [AS] <데이터타입>
    [DEFAULT <기본값>]
    [CONTRAST <제약조건명> CHECK <범위값>]

  # TABLE 정의
  CREATE TABLE <테이블명>
    [, PRIMARY KEY (<기본키-속성명>, ...)]
    [, UNIQUE (<대체키_속성명>, ...)]
    [, FOREIGN KEY (<외래키_속성명>,...)]
          [REFERENCES <참조테이블>(<기본키 속성명>,...)]
          [ON DELETE <옵션>]
          [ON UPDATE <옵션>]
    [, CONSTRAINT <제약조건명>][CHECK <조건식>]

  - CONSTRAINT : 제약 조건 이름, CHECK : 제약 조건


  # VIEW 정의
  CREATE VIEW <뷰명> [(<속성명>[, <속성명>,...])]
  AS SELECT … (Select 문…)

  # INDEX 정의
  CREATE [UNIQUE] INDEX <인덱스명>
    ON <테이블명>
  (<속성명> [ASC|DESC][, <속성명>[ASC|DESC]])
  [CLUSTER]

  # TABLE 정의 변경
  ALTER TABLE <테이블명> ADD <속성명_데이터타입> [DEFAULT <기본값>]
  ALTER TABLE <테이블명> ALTER <속성명> [SET DEFAULT <기본값>]
  ALTER TABLE <테이블명> DROP COLUMN <속성명> [CASCADE]

  # DROP : 제거
  DROP SCHEMA <스키마명> [CASCADE | RESTRICT]
  DROP DOMAIN <도메인명> [CASCADE | RESTRICT]
  DROP TABLE <테이블명> [CASCADE | RESTRICT]
  DROP VIEW <뷰명> [CASCADE | RESTRICT]
  DROP INDEX <인덱스명> [CASCADE | RESTRICT]
  DROP CONSTRAINT <제약조건명>

  - CASCADE : 제거할 요소를 참조하는 모든 개체 삭제
  ex) 부모 삭제 → 자식 삭제
```


## DML (Data Manipulation Language, 데이터 조작어)
저장된 데이터를 실질적으로 관리하는데 사용되는 언어
- `SELECT`, `INSERT`, `DELETE`, `UPDATE`


``` sql
  # 새로운 튜플 삽입
  INSERT INTO <테이블명>([속성명1, 속성명2, … ])
    VALUES (데이터1, 데이터2, …)

  # 특정 튜플 삭제
  DELETE FROM <테이블명> [WHERE 조건]

  # 튜플 내용 갱신
  UPDATE <테이블명> SET 속성명 = 데이터
                        [,속성명=데이터, …] [WHERE 조건]
```

``` sql
  SELECT [DISTINCT] 속성명1, 속성명2, …
    [그룹 함수 [AS 별칭]]
    [WINDOW 함수]
  FROM <테이블명>[, <테이블명>]
    [WHERE 조건]
    [GROUP BY 속성명1, 속성명, … ]
    [HAVING 조건]
    [ORDER BY 속성명1 [ASC | DESC]]

  - 그룹함수 :: COUNT(), SUM(), AVG(), MAX, MIN, ...
  - WINDOW 함수 :: ROW_NUMBER(), RANK(), DENSE_RANK()
  - WHERE LIKE 연산자 ::
    % 모든 문자 대표, _ 문자 하나 대표, # 숫자 하나 대표

  # 집합 연산자
  SELECT 속성명1 FROM <테이블명>
    UNION | UNION ALL | INTERSECTION | EXCEPT
    SELECT 속성명1 FROM <테이블명>
  [ORDER BY 속성명 [ASC | DESC]]
```

## DCL (Data Control Language,  데이터 정의어
데이터의 보안, 무결성, 회복, 병행 제어 등을 정의하는데 사용하는 언어
- `COMMIT`, `ROLLBACK`, `GRANT`, `REVOKE`

``` sql
  # 사용자 등급 지정, 해제
  # GRANT : 권한 부여
  # REVOKE : 권한 취소
  GRANT <사용자등급> TO <사용자_ID_리스트>
                      [IDENTIFIED BY 암호]
  REVOKE <사용자등급> FROM <사용자_ID_리스트>


  # 속성에 대한 권한 부여, 취소
  GRANT <권한리스트> ON <개체> TO <사용자>
  [WITH GRANT OPTION]
  REVOKE [GRANT OPTION] <권한리스트> ON <개체>
  FROM <사용자> [CASCADE]

  # 트랜잭션이 수행한 내용 DB 에 반영
  COMMIT

  # 아직 COMMIT 되지 않은 내용 모두 취소 + 이전상태로 원복
  ROLLBACK

  # ROLLBACK 할 위치인 저장점 지정
  SAVEPOINT <저장점>
```
