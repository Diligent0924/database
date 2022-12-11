# Clustering

### Clustering란 무엇인가?
Cluster Factor란 Index에서 군집화가 되어있지 않으면 조건문이 걸릴 경우 전체를 확인해야하는 불필요한 일이 발생한다.
따라서 Index의 도메인별로 구분해서 둔다면 해당 조건이 걸릴 때 테이블 전체를 확인할 필요가 없으므로 Index별로 군집화하는 것을 의미한다.
=> 데이터베이스를 논리적 구조로 봤을 때 동일한 블록에 저장하는 것을 의미함(데이터 블록)

### MYSQL에서 Clustering는 어떻게 작용하는가?
MYSQL(Innodb)에서 Cluster Factor는 해당 Column을 Index로 변경하게 되면 자동으로 해준다.

### Clustering의 단점은 무엇인가?
테이블에 데이터가 들어오게 되었을 때 None Clustering의 경우에는 그냥 아래줄에 넣는 방식이지만 Clustering의 경우에는 해당 데이터의 인덱스를 확인한 후 같은 데이터블록에 저장해야하기 때문에 CRUD 부분에서 성능이 저하된다.
=> MYSQL의 단점이라고 생각할 수 있을 것 같다.
