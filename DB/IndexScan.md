# 인데스 스캔의 정의

### 인덱스의 정의
인덱스는 각각의 인스턴스를 구별할 수 있게 하는 속서어을 의미한다. 기본적으로는 ROW_ID가 붙게 되며 MYSQL에서는 ID따로 만들어 AI로 올리는 것을 기본으로 한다.  
만약 인덱스에 중복되는 값이 존재한다면 Primary Key로서의 역할을 못한다. (애초에 안들어가진다.)  

### 복합키란 무엇인가?
복합키란 Index Column이 2개 이상일 때를 의미한다. Primary Key가 반드시 1개일 필요는 없다. 만약 중복된 Primary Key값을 Index로 쓰고 싶다면 다른 Column을 Index로 만들어서 2개의 튜플 형태의 Index Key로 만들면 된다. (복합키일 때도 고유성은 유지되야함)  

### 왜 고유의 Primary Key 1개가 아닌 복합키를 쓸까?
복합키를 쓰는 가장 큰 이유는 Index Scan시에 사용하기 때문이다. Index Scan은 말 그대로 Index를 기준으로 자료를 먼저 찾는 방법이기 때문에 훨씬 빠르다.

### Index Scan의 기본적인 원리
DB에서 데이터를 찾는 방법은 기본적으로 Index에서 수직으로 Scan한 후에 뒤의 Column을 수평으로 Searching하는 방법이다.  

예시) 복합키 (name, number) 일반 속성 (class) 일때  
name을 기준으로 수직 확인하고 그 뒤 number를 기준으로 수직확인함  
결론 : 중복도가 낮은 것을 무조건 앞에 세우고 Index Scan 시에 순서대로 넣어야 한다.

### Index가 너무 많으면 안되는 이유
1. Index Scan을 사용 시에 where절에서 Index 조건이 순서대로 들어가야하기 때문에 많아지게 되면 결국 의미가 없어짐
2. Index라는 것은 결국 기본 속성에서 Index Storage에 따로 저장하는 것이기 때문에 너무 많아지면 오히려 역효과를 불러올 수 있다.

### Index Scan의 종류
1. Index Range Scan
   1. Primary Key에서 Sorting을 통해 Sorting된 것으로 확인하는 방식 (도메인이 아닌 범위 개념)
   2. 전체 Index를 다 훑어보지 않으므로 빠르다.
   3. Sorting이 필요하므로 어떤 것이 더 효율적인지 확인해봐야 한다.
2. Index Full Scan
   1. 모든 Index를 확인하는 방법을 의미함
   2. 너무 대량의 데이터가 들어가 있는 것이 아니고 소수의 도메인을 확인할 때 유용하게 사용될 것 같다. 
3. Index Skip Scan
   1. CF일때 사용이 가능하며 Index Full Scan에서 가장 앞의 인스턴스만 확인한 후에 조건에 안맞으면 Skip하고 바로 다음 Cluster로 넘어가는 방식(도메인별로 CF되있을 때 유용하게 사용)

# 결론

1. Index는 최대한 고민을 해본 후에 추가해야 한다.
2. 복합키의 경우 Index Key의 순서가 중요하다.
3. MYSQL은 기본적으로 CF가 탑재되어 있기 때문에 Scan 부분에 있어서는 Index Range / Index Skip을 자동으로 사용하는 것으로 보인다.