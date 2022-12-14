# index

### 데이터 검색 시 속도 향상을 위한 객체

- 장점
    
    검색 속도 향상 → select문 고속화
    
    시스템 부하 감소
    
- 단점
    - 인덱스를 위한 추가 공간 필요
    - 생성 시에도 시간 소요
    - 데이터 변경이 많은 경우 오히려 성능 저하 발생
    
     → insert, update, delete시에 자동으로 인덱스가 갱신하기 때문에 오버헤드가 발생
    

### index를 사용하면 유리한 경우

- 크기가 큰 테이블
- 값의 범위가 넓은 컬럼 (카디널리티가 높은) - unique, primary 등
- join, where, select에서 자주 언급되는 컬럼 (검색 조건)
- 쿼리를 했을 때 보통 전체 데이터의 2~4% 이내의 데이터
    
    → 이 반대의 경우는 오히려 비효율적
    

### 불리한 경우

- 대용량의 데이터가 자주 입력되는 경우
- 데이터의 중복도가 높은 열은 인덱스 효과가 없다
    - ex) 성별 컬럼에 M / F 만 있는 경우는 안쓰는게 낫다.

### index 종류

- 사용자 정의 인덱스
    
    create index [index_name] on table_name(column_name1, 2, 3…);
    
    - 여러 컬럼으로 인덱스를 잡는다면 카디널리티가 높은순에서 낮은순으로 구성하는것이 성능이 더 뛰어나다. (MySql에서는 최대 15개)
    
    create unique index ~~~ (중복 값을 허용하지 않는 인덱스)
    
- 미리 정의된 키는 자동으로 인덱스 구성
    
    ex) primary, unique, foreign key
    

### index 문법

- 생성
    - 단일 인덱스
        
        create index 인덱스이름 on 테이블이름 (컬럼이름)
        
        alter table 테이블이름 add index 인덱스이름 (컬럼이름)
        
    - 다중 컬럼 인덱스
        
        create index 인덱스이름 on 테이블이름 (컬럼이름1, 컬럼이름2, …)
        
- 조회
    
    show index from 테이블이름
    
- 정렬 (인덱스 생성 시점에 필드의 정렬방식 설정)
    
    create index 인덱스이름 on 테이블이름 (컬럼이름 desc)
    
    create index 인덱스이름 on 테이블이름 (컬럼이름 asc)
    
- 삭제
    
    alter table 테이블이름 drop index 인덱스이름;
    
    drop index 인덱스이름 on 테이블이름
    
- 추가
    
    altere table 테이블이름 add index 인덱스이름 (컬럼이름)
    

### 단일 인덱스 / 다중 컬럼 인덱스 차이점

```sql
CREATE TABLE table1(
    uid INT(11) NOT NULL auto_increment,
    id VARCHAR(20) NOT NULL,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(100) NOT NULL,
    PRIMARY KEY('uid'),
    INDEX idx_name(name), -- 단일 인덱스
    INDEX idx_address(address) -- 단일 인덱스
)

CREATE TABLE table2(
    uid INT(11) NOT NULL auto_increment,
    id VARCHAR(20) NOT NULL,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(100) NOT NULL,
    PRIMARY KEY('uid'),
    INDEX idx_name(name, address) -- 다중 컬럼 인덱스 
)
```

```sql
SELECT * FROM table1 WHERE name='홍길동' AND address='경기도';
```

- table1의 경우에 name, address에 각각 단일 인덱스로 걸려있기 때문에 MySql은 두 컬럼중에 어떤 컬럼의 수가 더 빠르게 검색되는지 판단 후에 빠른쪽을 먼저 검색하고 그 다음 다른 컬럼을 검색한다.
- table2는 다중 컬럼 인덱스이기 때문에 name과 address를 같이 저정하기 때문에 이렇게 사용할 경우 table1보다 더 빠른 검색을 할 수 있다.

```sql
SELECT * FROM table2 WHERE address='경기도';
```

- 이 경우에 table2는 다중 컬럼 인덱스로 name이 함께 검색되지 않으므로 index의 효과를 볼 수가 없다.
