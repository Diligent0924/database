# Cluster Factor

### Cluster Factor란 무엇인가?
Cluster Factor란 Index에서 군집화가 되어있지 않으면 조건문이 걸릴 경우 전체를 확인해야하는 불필요한 일이 발생한다.
따라서 Index의 도메인별로 구분해서 둔다면 해당 조건이 걸릴 때 테이블 전체를 확인할 필요가 없으므로 Index별로 군집화하는 것을 의미한다.

### MYSQL에서 Cluster Factor는 어떻게 작용하는가?
MYSQL(Innodb)에서 Cluster Factor는 해당 Column을 Index로 변경하게 되면 자동으로 해준다.