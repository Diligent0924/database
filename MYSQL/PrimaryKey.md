# Primary Key 추가/수정/삭제/조회하는 방법

### primary key 확인
show indexes in [테이블]

### primary key 추가
alter [table명] add primary key([컬럼명], ..) # 다중으로 넣고자 할 때도 사용 가능하다.

### primary key 삭제
alter [table명] drop primary key

### 수정 => 삭제/추가를 그냥 같이하면 됨
alter [table명] drop primary key, add primary key([컬럼명]...)