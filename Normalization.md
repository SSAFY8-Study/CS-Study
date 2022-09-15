# DB - 정규화(Normalization)
- 테이블 간에 중복된 데이터를 최소화하기 위한 구조화 작업
- 장점
    - 무결성 유지
    - DB 저장 용량 최소화
    - 데이터의 구성을 논리적으로 변경하여 삽입, 갱신, 삭제 시 발생할 수 있는 이상현상 방지
- 정규화 단계에 따라 분류
    - 제 1 정규화
    - 제 2 정규화
    - 제 3 정규화
    - 제 4 정규화 - 실무에 잘 쓰이지 않음. 설명 X
    - 제 5 정규화 - 실무에 잘 쓰이지 않음. 설명 X
    - BCNF 정규화

### 제 1 정규화

**모든 속성에 하나의 데이터만 들어가야함 ⇒ 데이터의 원자성**

*원자값:더 이상 쪼개질 수 없는 단위

- 아래와 같이 id가  2022002인 club컬럼처럼, 컬러에는 두 개 이상의 값이 들어갈 수 없다.
- student에서 club을 분리시켜줘야 함

**student**

| student_id | student_name | department | subject_id | grade | club | 등록금 |
| --- | --- | --- | --- | --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 | AAA000 | A | 봉사부 | 400 |
| 2022002 | kim | 수학과 | BBB000 | B | 운동부, 댄스부 | 300 |
| 2022003 | lee | 기계공학과 | CCC000 | C | 연극부 | 500 |

**제 1 정규화 진행 후**

**student**

| student_id | student_name | department | subject_id | grade |
| --- | --- | --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 | AAA000 | A |
| 2022002 | kim | 수학과 | BBB000 | B |
| 2022003 | lee | 기계공학과 | CCC000 | C |

**student_club_relation**

| student_id | club_id |
| --- | --- |
| 2022001 | 1 |
| 2022002 | 2 |
| 2022002 | 3 |
| 2022003 | 4 |

**club**

| club_id | club_name |
| --- | --- |
| 1 | 봉사부 |
| 2 | 운동부 |
| 3 | 댄스부 |
| 4 | 연극부 |

**제 1 정규화 진행 후 발생하는 이상현상**

- 삽입 이상 : 학생이 새로운 과목 수강 시, department와 등록금과 student_name을 알아야함(불필요한 정보)
- 삭제 이상 : 학생 id가 2022002인 학생이 BBB000 과목을 취소하면 해당 과목 정보 사라짐
- 갱신 이상 : 학생 id가 2022001인 학생이 전과할 경우, 모든 해당학생의 모든 row의 department를 변경시켜주어야 함

### 제 2 정규화

**제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블 분해**

***완전 함수 종속이란?** 

**기본키의 부분집합이 결정자가 되면 안 됨.**

- 아래 테이블의 기본키가 student_id+subject_id 로 복합키로 이루어지고, 해당 기본키는 grade와 department, 등록금을 결정함
- 여기서 기본키의 부분집합인 student_id가 student_name과 department, 등록금을 결정함
- 추가적으로 department 는 등록금을 결정함
- 위와 같은 함수의 종속성을 가진다면, student_name과 department, 등록금은 부분 함수 종속성을 가지고 있음
- student_id⇒department로 볼 때, student_id 하나만으로  department를 결정 가능하지만, 현재는 기본키가 복합키(student_id+subject_id)로 이루어져있으므로 의미가 없음
- 이 종속성을 의미있게 하기 위해 제 2정규화를 통해 테이블을 나누면서 부분 함수 종속성을 제거하는 것!

**student**

| student_id | student_name | department | subject_id | grade | 등록금 |
| --- | --- | --- | --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 | AAA000 | A | 400 |
| 2022001 | park | 컴퓨터공학과 | AAA001 | B | 400 |
| 2022002 | kim | 수학과 | BBB000 | B | 300 |
| 2022003 | lee | 기계공학과 | CCC000 | C | 500 |

**제 2 정규화 후**

**student**

| student_id | student_name | department | 등록금 |
| --- | --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 | 400 |
| 2022002 | kim | 수학과 | 300 |

**grade**

| student_id | subject_id | grade |
| --- | --- | --- |
| 2022001 | AAA000 | A |
| 2022001 | AAA001 | B |
| 2022002 | BBB000 | B |
| 2022003 | CCC000 | C |
| 2022003 | CCC001 | A |

**제 2 정규화 진행 후 발생하는 이상현상**

- 삽입 이상 : 특정 department에 등록금을 추가하고싶을 때 학생의 정보가 있어야 함(불필요한 정보)
- 삭제 이상 : id가 2022001인 학생이 자퇴하면 컴퓨터공학과와 등록금 정보는 사라짐
- 갱신 이상 : 특정 학과의 등록비가 변경되었을 경우, 해당 학과의 모든 row의 등록금을 변경시켜주어야 함(동일한 학과를 가진 학생이 여러 명 일 경우)

### 제 3정규화

**제2 정규화를 진행한 테이블에 대해 모든 속성이 기본키에만 의족하도록 테이블을 구성 ⇒ 이행적 함수 종속이 불가능하도록 구성**

- 아래 테이블의 student_id ⇒ student_name, department, 등록금 결정
- department ⇒ 등록금을 결정함
- 해당 테이블은 **student_id⇒department** , **department ⇒등록금**의 함수적 종속 관계로 인해  **student_id⇒ 등록금**이라는 이행적 함수 종속 관계가 나타남
- 이러한 함수 종속 관계가 나타나면 테이블을 **student_id, department**와 **department,등록금**으로 분리!

**student**

| student_id | student_name | department | 등록금 |
| --- | --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 | 400 |
| 2022002 | kim | 수학과 | 300 |

**제 3정규화 진행 후**

**student**

| student_id | student_name | department |
| --- | --- | --- |
| 2022001 | park | 컴퓨터공학과 |
| 2022002 | kim | 수학과 |

**department**

| department | 등록금 |
| --- | --- |
| 컴퓨터공학과 | 400 |
| 수학과 | 300 |

### BCNF 정규화

**제 3 정규화를 진행한 테이블에 대해 컬럼에 대한 모든 결정자가 후보키가 되도록 테이블을 구성**

- student_id+subject_id로 기본키를 가진 테이블에서 기본키가 담당교수를 결정
- 담당교수는 subject_id를 결정
- 해당 테이블은 제 3정규화를 만족키신 테이블이지만 이상현상 발생
- 삽입 이상 : 새로운 교수가 과목을 추가할 시, 적어도 한 명의 수강 학생 필요
- 삭제 이상 : id가 2022001인 학생이 AAA000 과목을 취소한다면, p1일 AAA000과목의 담당 교수라는 정보 사라짐
- 갱신 이상 : p1의 subject_id가 변경될 경우, p1의 모든 row를 찾아 subject_id를 변경시켜주어야 함
- 하지만 테이블의 후보키가 아닌 담당교수가 subject_id결정하고 있음
- BCNF 정규화로 테이블을 두개로 분해

**student**

| student_id | subject_id | 담당교수 |
| --- | --- | --- |
| 2022001 | AAA000 | p1 |
| 2022002 | BBB000 | p2 |
| 2022003 | CCC000 | p3 |

**BCNF 정규화 진행 후**

**student**

| student_id | 담당교수 |
| --- | --- |
| 2022001 | p1 |
| 2022002 | p2 |
| 2022003 | p3 |

**subject**

| 담당교수 | subject_id |
| --- | --- |
| p1 | AAA000 |
| p2 | BBB000 |
| p3 | CCC000 |

### * 이상현상

- 갱신 이상
    - 중복된 데이터 중 일부를 갱신할 때 발생하는 데이터 불일치
    
- 삽입 이상
    - 새로운 데이터를 삽입하기 위해 불필요한 데이터가 삽입되면서 생기는 데이터 불일치
- 삭제 이상
    - 데이터 삭제 시 의도치 않은 데이터가 삭제되면서 생기는 데이터의 불일치
    

**[Reference]**

[https://yaboong.github.io/database/2018/03/09/database-normalization-1/](https://yaboong.github.io/database/2018/03/09/database-normalization-1/)

[https://rebro.kr/160](https://rebro.kr/160)
