## **📎 SQL**

관계형 DB에서 데이터 정의, 조작, 제어를 위해 사용하는 언어이다.

**SQL의 분류**

-   DDL (Data Define Language) : 데이터 정의어
-   DML (Data Manage Language) : 데이터 조작어
-   DCL (Data Controll Language) : 데이터 제어어
-   TCL (Transaction Control Language) : 트랜잭션 제어어

<br>
<br>

## **📎 DDL**

**DDL의 특징**

-   데이터 구조, 데이터 형식 등 DB를 구축하거나 수정할 목적으로 사용하는 언어이다.
-   스키마, 도메인, 테이블, 뷰, 인덱스를 정의, 변경, 삭제할 수 있다.
-   직접 데이터베이스에 영향을 미치므로 명령어 입력 순간 해당하는 작업이 즉시 커밋된다. (ROLLBACK 불가)

<br>

**명령어**

-   CREATE : 데이터베이스의 객체 생성
-   ALTER : 데이터베이스의 구조 변경
-   DROP : 데이터베이스의 객체 삭제
-   TRUNCATE : 테이블에 할당된 레코드 제거 및 메모리 해제

<br>

**명령어 사용 방법**

\[1\] CREATE

```
CREATE TABLE 테이블명 
	(속성명 데이터타입 [DEFAULT 기본값] [NOT NULL],
    [PRIMARY KEY (기본키_속성명, ...)],
    [UNIQUE KEY (대체키_속성명, ...)],
    [FOREIGN KEY (외래키_속성명, ...)]
    	REFERENCES 참조테이블 (기본키_속성명, ...)]
        [ON DELETE 옵션]
        [ON UPDATE 옵션],
    [CONSTRAINT 제약조건명][CHECK (조건식)]);
```

👉 옵션 종류

-   NO ACTION : 참조 테이블의 변화가 있어도 기본 테이블에는 영향 없음
-   CASCADE : 참조 테이블의 변화를 기본 테이블에 똑같이 적용
-   SET NULL : 참조 테이블에 변화 있을 시 기본 테이블에 NULL로 적용
-   SET DEFAULT : 참조 테이블에 변화 있을 시 기본 테이블은 DEFAULT 값으로 적용

<br>

\[2\] ALTER

```
ALTER TABLE 테이블명 ADD 속성명 데이터타입 [DEFAULT '기본값'];
ALTER TABLE 테이블명 ALTER 속성명 [SET DEFAULT '기본값'];
ALTER TABLE 테이블명 DROP COLUMN 속성명 [CASCADE];
```
<br>

\[3\] DROP

```
DROP TABLE 테이블명 [CASCADE | RESTRICTED];
```

👉 RESTRICTED : 다른 개체가 제거할 요소를 참조 중일 떄는 제거를 취소

<br>
<br>

## **📎 DML**

**DML의 특징**

-   DB의 데이터를 조회하거나 검색하기 위한 것으로,  
    데이터를 실질적으로 관리하는데 사용되는 언어이다. (DB 사용자와 DBMS간의 인터페이스 제공)
-   데이터 삽입, 수정, 삭제 등의 동작이 가능하다.
-   조작하려는 테이블을 메모리 버퍼에 올려놓고 작업하므로 자동 커밋되지 않는다. (ROLLBACK 가능)
-   처리한 DML 명령을 실제 테이블에 반영시키려면 COMMIT 명령을 실행해야 한다.

<br>

**명령어**

-   SELECT : 데이터 검색
-   INSERT : 데이터 삽입
-   UPDATE : 기존 데이터 수정
-   DELETE : 데이터 삭제

<br>

**명령어 사용 방법**

\[1\] SELECT

```
SELECT [PREDICATE] [테이블명] 속성명 [AS 별칭] [, [테이블명] [속성명], ...]
[, 그룹 함수 (속성명) [AS 별칭]]
[, WINDOW 함수 OVER (PARTITION BY 속성명1, 속성명2, ...
					ORDER BY 속성명3, 속성명4, ...)]
FROM 테이블명 [, 테이블명, ...]
[WHERE 조건]
[GROUP BY 속성명, 속성명, ...]
[HAVING 조건]
[ORDER BY 속성명 [ASC | DESC]];
```

👉 PREDICATE : 불러올 튜플 수를 제한

-   ALL : 모든 튜플 (보통은 생략)
-   DISTINCT : 중복된 튜플이 있을 경우 그 중 첫 번째 한 개만 검색
-   DISTINCTROW : 중복된 튜플을 제거하고 한 개만 검색하지만, 선택된 속성값이 아니라 전체 튜플을 대상으로 함

<br>

👉 그룹 함수 : GROUP BY 절에서 지정한 그룹별로 함수 적용

-   COUNT(속성명), SUM(속성명), AVG(속성명) : 개수, 합, 평균
-   MAX(속성명), MIN(속성명) : 최대, 최솟값

<br>

👉 WINDOW 함수 : GROUP BY 절을 이용하지 않고 함수의 인수로 지정한 속성을 범위로하여 집계

-   ROW NUMBER() : 1, 1, 3, 4, 4, 6과 같은 형식으로 순위 결정
-   RANK() : 1, 1, 2, 3, 3, 4와 같은 형식으로 순위 결정
-   DENSE RANK() : 1, 2, 3, 4, 5, 6과 같이 같은 값이어도 고유한 순위 부여

<br>

\[2\] INSERT

```
INSERT INTO 테이블명([속성명1, 속성명2, ...])
VALUES(데이터1, 데이터2, ...);
```
<br>

\[3\] UPDATE

```
UPDATE 테이블명
SET 속성명 = 데이터 [, 속성명 = 데이터, ...]
[WHERE 조건];
```

<br>

\[4\] DELETE

```
DELETE FROM 테이블명
[WHERE 조건];
```

<br>
<br>

## **📎 DCL**

**DCL의 특징**

-   DB에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 언어이다.
-   데이터의 보안, 무결성, 회복, 병행제어등을 정의할 수 있으며 데이터베이스관리자(DBA)가 사용한다.
-   직접 DB에 영향 미치므로, 명령어에 해당하는 작업이 즉시 자동 커밋된다. (ROLLBACK 불가)

<br>

**명령어**

-   GRANT : 권한 부여
-   REVOKE : 권한 취소

<br>

**명령어 사용 방법**

\[1\] 사용자 등급 지정/해제

```
GRANT 사용자등급 TO 시용자_ID_리스트 [IDENTIFIED BY 암호];
REVOKE 사용자등급 FROM 사용자_ID_리스트;
```

<br>

\[2\] 테이블 및 속성에 대한 권한 부여/취소

```
GRANT 권한_리스트 ON 개체 TO 사용자 [WITH GRANT OPTION];
REVOKE [GRANT OPTION FOR] 권한_리스트 ON 개체 FROM 사용자 [CASCADE];
```

👉 권한 종류 : ALL, SELECT, INSERT, DELETE, UPDATE, ALTER

<br>

👉 옵션 종류

-   WITH GRANT OPTION : 부여받은 권한을 또 다른 사용자에게 부여할 수 있도록 함 
-   GRANT OPTION FOR : 다른 사용자에게 권한을 부여할 수 있는 권한을 취소함

<br>
<br>

## **📎 TCL**

**TCL의 특징**

-   논리적인 작업 단위를 묶어서 DML에 의해 조작된 결과를 트랜잭션별로 제어한다.
-   DCL의 한 종류이지만, 이와 같이 분류 가능하다.

<br>

**명령어**

-   COMMIT : 변경된 내용을 DB에 반영
-   ROLLBACK : 아직 COMMIT되지 않은 내용을 취소 후 이전 상태로 되돌리기
-   SAVEPOINT : ROLLBACK할 위치 지정

<br>

**명령어 사용 방법**

```
COMMIT;
SAVEPOINT SAVEPOINT_이름;
ROLLBACK [TO SAVEPOINT_이름];
```

<br>
<br>

## **📎 DELETE, DROP, TRUNCATE 차이점**

|   | DELETE | DROP | TRUNCATE |
| --- | --- | --- | --- |
| 분류 | DML | DDL | DDL |
| ROLLBACK | COMMIT 이전 가능 | 불가 | 불가 |
| AUTO COMMIT | O | O | X |
| 메모리 | 메모리 자원 해제하지 않음 | 테이블이 사용했던   메모리 자원 모두 해제 | 최초로 테이블 생성 시 할당된 메모리 자원 제외 모두 해제 |
| 삭제 | 데이터만 삭제,   테이블 구조는 그대로 | 테이블의 정의 자체를   완전히 삭제 | 테이블을 최초 생성된   초기 상태로 되돌림 |
| 로그 | O | X | X |

👉 모든 행을 삭제하고 싶을 때는?  
TRUNCATE는 테이블을 DROP해버리고 다시 CREATE하는 것과 같으므로

모든 행을 삭제할 때는 TRUNCATE를 사용하는 것이 가장 효율적이다.

_(그러나 TRUNCATE는 ROLLBACK이 불가하므로 주의가 필요하다.)_

<br>

👉 세 명령의 차이점 그림 비교

![image](https://user-images.githubusercontent.com/59721896/190438998-40be5191-4e5c-4b74-abd1-ae0ca84db109.png)
---

참고

-   [https://iamfreeman.tistory.com/entry/DBMS-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%96%B8%EC%96%B4-DDL-DML-DCL-TCL-%EC%9D%98-%EC%A0%95%EC%9D%98](https://iamfreeman.tistory.com/entry/DBMS-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%96%B8%EC%96%B4-DDL-DML-DCL-TCL-%EC%9D%98-%EC%A0%95%EC%9D%98)
-   [https://jhnyang.tistory.com/56](https://jhnyang.tistory.com/56)
-   [https://for-my-wealthy-life.tistory.com/48](https://for-my-wealthy-life.tistory.com/48)
