# 프로시저(Procedure)
SQL 을 사용하여 작성한 일련의 작업을 저장해두고 호출을 통해 원할때마다 저장한 작업을 수행하도록 하는 절차형 SQL

## 프로시저 생성
``` sql
  CREATE [OR REPLACE] PROCEDURE <프로시저명> 
    [지역변수 선언]
    BEGIN <프로시저 BODY>;   # 프로시저 시작
  END;   # 프로시저 종료
```
## 프로시저 실행
``` sql
EXECUTE <프로시저명>;
EXEC <프로시저명>;
CALL <프로시저명>;
```
## 프로시저 제거
``` sql
DROP PROCEDURE <프로시저명>;
```

# 트리거 (Trigger)
이벤트가 발생할 때 관련 작업이 자동으로 수행되게하는 절차형 SQL

## 트리거생성
``` sql
CREATE [OR REPLACE] TRIGGER <트리거명(파라미터)> 
 [동작시기 옵션][동작 옵션] ON <테이블명> 
 REFERENCING [NEW | OLD] AS <테이블명>
 FOR EACH ROW
 [WHEN 조건] 
 BEGIN <트리거 BODY>;   # 트리거 시작
 END;   # 트리거 종료
```
## 트리거 제거
``` sql
DROP TRIGGER <트리거명>;
```

# 사용자 정의 함수
종료시 처리 결과로 단일값 만을 반환하는 절차형 SQL

## 사용자정의 함수 생성
``` sql
CREATE [OR REPLACE] FUNCTION <사용자 정의 함수명(파라미터)> 
 [지역변수 선언]
 BEGIN
  <사용자 정의 함수 BODY>;   # 함수 시작
  RETURN <반환값>;
 END;   # 함수 종료
```

## 함수 제거
``` sql
DROP FUNCTION <함수명>;
```


# 제어문
절차형 SQL 의 진행순서 변경을 위해 사용하는 명령문

## IF 문
``` sql
IF 조건 THEN
 실행 문장 1;
 실행 문장 2; …
END IF;

IF 조건 THEN
 실행 문장 1;
ELSE
 실행 문장 2; …
END IF;
```
## LOOP : 반복 수행
``` sql
LOOP
 실행 문장;
 EXIT WHEN 조건;
END LOOP;
```

# 커서(Cursor)
쿼리문의 처리 결과가 저장되어있는 메모리 공간을 가리키는 포인터

## 묵시적 커서 (Implicit Cursor)
내부에서 자동으로 생성되어 사용되는 커서
수행된 쿼리문의 정상적인 수행여부 확인하기 위해 사용

|              | 결과로 패치 (Fetch) 된 튜플 수가                       |
| ------------ | ------------------------------------------------------ |
| SQL%FOUND    | 1 개 이상이면 TRUE                                     |
| SQL%NOTFOUND | 0 개 이면 TRUE                                         |
| SQL%ROWCOUNT | 튜플 수를 반환                                         |
| SQL%ISOPEN   | - 묵시적 커서는 생성된 후 자동으로 닫힘  :: 항상 FALSE |


## 명시적 커서 (Explicit Cursor)
사용자가 직접 정의해서 사용하는 커서
쿼리문의 결과를 저장하여 사용함으로써 자원 낭비 방지

### 선언 형식 - Declare
``` sql
CURSOR <커서명(매개변수)> IS
  <SELECT 문>;
```

### 열기 형식 - Open
``` sql
OPEN <커서명(매개변수)>;
```

### 패치 형식 - Fetch
``` sql
FETCH <커서명> INTO 변수1, 변수2, …;
```

### 닫기 형식 - Close
``` sql
CLOSE  <커서명>;
```

