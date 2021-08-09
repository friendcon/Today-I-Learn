# 인덱스(index)와 실행계획

데이터가 많은 상태에서 정렬 작업을 하게되면 시간이 오래걸리게 된다. 이를 해결하기 위해 `**인덱스(index)**` 가 등장하였다. 인덱스를 이용하면 `**인덱스 자체가 정렬된 구조**`이기 때문에 정렬을 생략할 수 있다. 

### 인덱스 사용 예

```sql
select /*+ INDEX_DESC(tbl_board pk_board) */ 
* from tbl_board where bno > 0;
```

`pk_board` 를 이용해서 `tbl_board`에 접근한다.

`range scan descending` 과 `by index rowid` 를 이용해서 접근한다.

primary key를 생성하면 자동으로 인덱스를 만들어준다. 

데이터베이스에서 PK는 `**식별자`** 와 `**인덱스`** 의 의미를 갖는다. 

### 인덱스와 ROWID

인덱스에와 실제 테이블을 연결하는 것은 `**ROWID`** 이다. ROWID는 데이터베이스 내의 주소이고 모든 데이터들은 자신만의 주소를 가지고 있다. 

### 인덱스를 이용하는 정렬

인덱스는 정렬이 되어있다는 점이다. 

### 인덱스와 오라클 힌트

웹페이지 목록은 주로 시간의 역순으로 정렬된 결과를 보여준다. 최신 데이터가 가장 중요하기 때문이다. 

`**힌트`** 는 **내가 전달한 select문을 이렇게 실행**해 주면 좋겠습니다 라는 힌트다. 

게시글 목록은 반드시 시간의 역순으로 나와야 하기 때문에 SQL문에서 `**order by bno desc**` 와 같은 구문을 추가해야한다. 이러한 방식을 사용하면 모든 데이터를 정렬해야한다.

`**힌트**` 를 사용하면 개발자가 데이터베이스에 어떤 방식으로 실행해줘야 하는지 명시하기 때문에 강제성이 부여된다.

- 힌트 사용 전

```sql
select * from tbl_board order by bno desc;
```

- 힌트 사용 후

```sql
select /*+ INDEX_DESC(tbl_board pk_board) */ 
* from tbl_board;
```

힌트를 사용했을 때 `order by` 가 없어도 동일한 결과가 나왔다. 

### 힌트의 문법

힌트는 `/*+ */` 키워드를 사용하면 된다.  

### FULL 힌트

select 문을 실행할 때 테이블 전체를 스캔할 것을 명시하는 FULL 힌트다.

```sql
SELECT /*+ FULL(tbl_board) */ from tbl_board order by bno desc;
```

### INDEX_ASC, INDEX_DESC 힌트

목록 페이지에서 가장 많이 사용하는 힌트다. `INDEX_ASC, INDEX_DESC` 힌트다. 이 힌트는 `ORDER BY` 를 위해 사용된다. 인덱스 자체가 정렬을 해 둔 상태이므로 SORT 과정을 거치지 않는다. 

```sql
select /*+ INDEX_ASC(tbl_board pk_board) */ 
* from tbl_board WHERE BNO > 0;
```

### ROWNUM과 인라인뷰

필요한 데이터만 가져오기 위해 ROWNUM이라는 키워드를 사용해서 데이터에 순번을 붙여 사용한다. SQL이 실행된 결과에 넘버링을 해준다. 

ROWNUM은 테이블에는 존재하지 않고 테이블에서 가져온 데이터를 이용해서 번호를 붙이는 방식이다. 테이블에서 가장 먼저 가져올 수 있는 데이터들을 꺼내서 번호를 붙여준다.

ROWNUM은 데이터를 가져올 때 적용되는 것이고 정렬되는 과정에서 ROWNUM이 변경되지 않는다. 즉 정렬은 나중에 처리된다는 뜻이다. 

### 인덱스를 이용한 접근 시 ROWNUM

테이블에 어떤 순서로 접근하는가에 따라 ROWNUM이 달라진다. 최신글을 가장 앞에 오게하기 위해서는 다음과 같이 SQL문을 작성하면 된다.

```sql
SELECT /*+ INDEX_DESC(tbl_board pk_board) */ rownum rn, bno, title, content
from tbl_board where bno > 0;
```

가장 최근의 글을 내림차순으로 정렬 후 rownum 을 부여해준다.